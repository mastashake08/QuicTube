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
            showLoaderOnInit: false,
            pauseOthers: false,
        })
    await this.$player.init()

    this.constraints = await navigator.mediaDevices.getSupportedConstraints()
    console.log(this.constraints)
  },
  methods: {
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
        this.$player.getElement().srcObj = this.stream



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
