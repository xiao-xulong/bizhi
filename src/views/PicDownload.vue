<template>
  <div class="root">
    <page-top></page-top>

    <img class="title_img" src="../assets/wallPicBackGround.png">
    <img class="pic" ref="Vimg" style="position: absolute; z-index: -100; visibility: hidden;" :src="picAddress">
    <div class="fcan">
      <!-- <canvas ref="canva" class="can" id="myCanvas" style="background:transparent;">您的浏览器不支持Canvas!</canvas> -->

    </div>

    <a id="bottom-1" class="downLoadBtn" :href="picAddress + '?response-content-type=application/octet-stream'"
      download>

      壁纸下载</a>


  </div>
</template>

<script>
import pageTop from '../components/pageTop'
import { ImagePreview } from 'vant';
import { useRoute } from 'vue-router'
import { onMounted, ref } from 'vue'
export default {
  name: 'PicDownload',
  components: {
    pageTop
  },
  setup() {
    let route = useRoute();
    let picAddress = ref('')
    let fileList = ref([])
    let actHeight = ref({ height: '100px', top: '500px' })
    picAddress.value = route.query.url
    const Vimg = ref()
    const canva = ref()
    onMounted(() => {
      console.log('Vimg')
      console.log(Vimg)
      // let canvas = document.getElementById("myCanvas");

      // imageToCanvas(canvas, picAddress.value);
    })
    const imageToCanvas = function (canvas, url) {
      let img = new Image();
      img.src = url;
      // canva.value.clientHeight = Vimg.value.clientHeight
      img.onload = function () {
        let ctx = canvas.getContext("2d");
        canvas.height = Vimg.value.clientHeight

        ctx.drawImage(img, 0, 0, canvas.width, Vimg.value.clientHeight);
        actHeight.value.height = Vimg.value.clientHeight + 'px'

        // let scale = window.devicePixelRatio;
        // ctx.scale(scale, scale);
        // console.log(Vimg);
        console.log(Vimg.value.clientHeight);
        console.log(canva.value.clientHeight);
        console.log(actHeight.value.height);
        console.log(canvas.height);
      }
    }


    // let preView = function () {
    //   ImagePreview([
    //     route.query.url
    //   ]);

    // }




    return {
      fileList, picAddress, imageToCanvas, Vimg, canva, actHeight
    }
  }
}
</script>

<style scoped lang="less">
.root {
  background-color: #10171A;
  width: 100%;

  .title_img {
    margin-top: 10px;
    width: 150px;
    height: 70px;
    position: relative;
    left: 50%;
    transform: translateX(-50%);
  }

  .fcan {
    // position: relative;
    // width: 90%;
    // margin-top: 20px;

    // margin-left: 5%; 
    // .can {
    //   width: 100%;
    //   height: v-bind('actHeight.height');
    // }
  }



  .pic {
    width: 90%;

    height: auto;
  }
}

.downLoadBtn {
  display: inline-block;
  text-align: center;
  margin-top: 10Px;
  margin-left: 5%;
  width: 45%;
  height: 40Px;
  color: #40D7F7;
  border: #01e7ff solid 1px;
  line-height: 40Px;
  font-size: 22Px;
  margin-bottom: 10px;
}

.downLoadBtn::before {
  content: "";
  display: inline-block;
  width: 24Px;
  height: 22Px;
  background: url("../assets/download.png") no-repeat;
  background-size: 24Px 22Px;
  background-position: center;
  position: relative;
  top: 4Px;
  margin-right: 10px;


}
</style>
