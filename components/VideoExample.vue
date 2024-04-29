<script>
import Hls from 'hls.js';
import dashjs from 'dashjs';
import flvJs from 'flv.js';

import OpenPlayerJS from 'openplayerjs';
import 'openplayerjs/dist/openplayer.css';
export default {
  data() {
    return {
      stream: {},
      constraints: {},
      mediaSource: new MediaSource(),


    }
  },
  async mounted () {
    this.$player =  new OpenPlayerJS('player', {
            controls: {
              left: ['play', 'time', 'volume'],
              middle: ['progress'], // Semantically speaking, progress bar is in the middle
              right: ['levels', 'captions', 'settings', 'fullscreen'],
          },
            showLoaderOnInit: false,
            pauseOthers: false,
        })
    await this.$player.init()


    this.constraints = await navigator.mediaDevices.getSupportedConstraints()
    console.log(this.constraints)
  },
  methods: {
    sourceOpen() {
      const sourceBuffer = this.mediaSource.addSourceBuffer('video/webm;codecs=vp9')

        sourceBuffer.addEventListener("updateend", () => {
          this.mediaSource.endOfStream();
          this.$player.play();
          console.log(this.mediaSource.readyState); // ended
        });
        sourceBuffer.appendBuffer(this.stream);

    },
    async getMedia() {
      try {
        this.stream = await navigator.mediaDevices.getUserMedia({
          audio: {
            autoGainControl: true,
            noiseSuppression: true

          },
          video: {
            width: 1280,
            height: 720
        }});
        this.mediaSource.addEventListener("sourceopen", this.sourceOpen);

        this.$player.src = URL.createObjectURL(this.mediaSource)
        this.$player.load();


       //

      } catch (error) {
        alert(error)
      }
    }
  }
}

</script>
<template>
    <UContainer>
      <UPage>
        <template #left>
          <UAside>
            <template #top>
              <UContentSearchButton
                class="rounded-md"
                size="sm"
              />
            </template>

            </UAside>
        </template>
        <video id="player" ref="player" class="op-player__media" controls playsInline>
         </video>
        <UButtonGroup>
          <UButton @click="getMedia">Stream Camera</UButton>
        </UButtonGroup>

      </UPage>
    </UContainer>
</template>
