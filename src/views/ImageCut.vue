<template>
  <div class="container">
    <el-dialog
      v-model="showModal"
      :width="dialogWidth"
      :height="dialogHeight"
      :before-close="handleClose"
      class="myDialog"
    >
      <!-- 右上角的按钮 -->
      <template v-slot:header>
        <span>脑部图像信息</span>
        <el-button
          type="link"
          icon="el-icon-minus"
          @click="minimize"
          class="icon-button"
          ><el-icon class="el-icon-zoom-in"><ZoomOut /></el-icon
        ></el-button>
        <el-button
          type="link"
          icon="el-icon-zoom-in"
          @click="maximize"
          class="icon-button"
          ><el-icon class="el-icon-zoom-in"><ZoomIn /></el-icon
        ></el-button>
      </template>

      <!-- 弹窗内容放在这里 -->
      <div class="mySlot" :style="dialogStyle">
        <slot>
          <img src="../assets/mind.jpg" class="dialogImg" />
          <button @click="cut" class="cutBtn">进行分割</button>
        </slot>
      </div>
    </el-dialog>
    <el-scrollbar class="myScrollbar" style="height: 100vh">
      <el-row :gutter="20" class="navbar">
        <el-col :span="4">
          <div class="ep-bg-purple title">
            <text class="titleText">智医科技</text>
          </div>
          <div class="ep-bg-purple eng">Medical Intelligence</div>
        </el-col>
        <el-col :span="8">
          <div class="grid-content ep-bg-purple" />
        </el-col>
        <el-col :span="1.5">
          <div class="grid-content ep-bg-purple nav" @click="navigateToHome">
            首页
          </div>
        </el-col>
        <el-col :span="1.5">
          <div
            class="grid-content ep-bg-purple nav"
            @click="navigateToPatientInfo"
          >
            病人信息
          </div>
        </el-col>
        <el-col :span="1.5">
          <div class="grid-content ep-bg-purple nav" @click="navigateToChat">
            在线答诊
          </div>
        </el-col>
        <el-col :span="1.5">
          <div
            class="grid-content ep-bg-purple nav"
            @click="navigateToClassicalCase"
          >
            经典案例
          </div>
        </el-col>
        <el-col :span="1.5">
          <div
            class="grid-content ep-bg-purple nav"
            @click="navigateToImageCut"
          >
            图像分割
          </div>
        </el-col>
        <el-col :span="1.5">
          <div
            class="grid-content ep-bg-purple nav"
            @click="navigateToAboutView"
          >
            关于我们
          </div>
        </el-col>
        <div class="middleTitle">
          <div class="bigTitle">图像分割</div>
          <div class="bigTranslate">
            对不同类型的医学影像数据进行高质量的分割，确定目标之间的关系
          </div>
        </div>
      </el-row>
      <div class="algorithm">
        <div class="left">
          <img src="../assets/algorithmImg.jpg" class="leftImg" />
        </div>
        <div class="right">
          <h2>算法特色</h2>
          <p>
            使用人工智能算法，平台将采用深度学习和Transformer模型和神
            经网络等先进的人工智能算法，用于医学图像分割。这些中引入
            了自注意力机制，该算法经过训练和优化，能够对不同类型的医学影像数据进行高质量的分割。
          </p>
          <div class="advantage">
            <span
              ><el-icon color="#15b7fd"><SuccessFilled /></el-icon
              >本产品算法将利用transformer算法中的自注意力机制，使其不同于传统的神经网络，可
              以更好的采取和利用对于全局信息的利用。
            </span>
            <span
              ><el-icon color="#15b7fd"><SuccessFilled /></el-icon
              >本产品所提出的算法可以更好的应对在不稳定状态下的医学图像分制问题，充分考虑到不
              稳定状态对于医学图像分割的影响，可以在准确程度上进行-定进步，
              实现更精确的准确率。
            </span>
            <span
              ><el-icon color="#15b7fd"><SuccessFilled /></el-icon
              >该算法具有较强的解释性，可以通过一系列可视化方法，直观、明确的看到该算法展示的
              分割效果，该算法在可以与之前算法进行相应比较，更好的展示它在设计上的优越性。
            </span>
          </div>
        </div>
      </div>
      <div class="show">
        <div class="left">
          <span class="demonstration">分割前</span>
          <img class="showImg" src="../assets/behindCut.jpg" />
        </div>
        <div class="right">
          <span class="demonstration">分割后</span>
          <img class="showImg" src="../assets/afterCut.jpg" />
        </div>
      </div>
      <div class="describe">
        <div class="left">
          <h2>肝癌分割</h2>
          <h4>背景和重要性：</h4>
          <p>
            肝癌是一种常见的癌症类型，早期诊断对于患者的生存率至关重要。医学图像分割技术可以帮助医生更好地理解肝脏中的肿瘤位置和大小，从而制定更有效的治疗计划。
          </p>
          <h4>医学影像类型:</h4>
          <p>
            肝癌图像分割通常涉及到多种医学影像类型，包括计算机断层扫描（CT）和磁共振成像（MRI）。这些影像提供了不同的解剖和功能信息，可以用于更精确地定位和分割肿瘤。
          </p>
          <h4>分割方法:</h4>
          <p>
            肝癌图像分割方法通常包括传统的图像处理技术和深度学习方法。传统方法包括阈值分割、边缘检测和区域生长等技术，而深度学习方法如卷积神经网络（CNN）和
            U-Net 等已经在此领域取得了巨大的成功。
          </p>
          <!-- <div class="advantage">
            <span
              ><el-icon color="#15b7fd"><SuccessFilled /></el-icon
              >Transformer算法的核心思想是利用自注意力(Self
              Attention)机制来处理输入
              序列中的不同位置之间的关系，而不是传统的循环神经网络(RNN)
              或卷积神经网络 (CNN)。
            </span>
            <span
              ><el-icon color="#15b7fd"><SuccessFilled /></el-icon
              >自注意力机制允许模型在处理输入时，对输入序列中的所有位置进行加权处理，
              从而能够同时考虑全局和局部的上下文信息。
            </span>
          </div> -->
        </div>
        <div class="right">
          <img
            src="../assets/gan1.jpg"
            alt=""
            style="width: 300px; height: 300px"
          />
          <img
            src="../assets/gan2.jpg"
            alt=""
            style="width: 300px; height: 300px"
          />
        </div>
      </div>
      <div class="describe">
        <div class="right1">
          <img
            src="../assets/fei.jpg"
            alt=""
            style="width: 600px; height: 300px"
          />
        </div>
        <div class="left1">
          <h2>肺癌分割</h2>
          <h4>背景和重要性：</h4>
          <p>
            肺癌是全球最常见的癌症之一，早期诊断对于提高生存率至关重要。医学图像分割技术可以在肺部CT扫描、X射线或其他影像中精确定位和分割肺部肿瘤，有助于早期发现和治疗计划。
          </p>
          <h4>医学影像类型:</h4>
          <p>
            肺癌图像分割通常涉及肺部的多模态医学图像，最常见的是CT扫描。这些图像提供了关于肺部结构和组织的详细信息，可用于诊断和疾病监测。
          </p>
          <h4>分割方法:</h4>
          <p>
            肺癌图像分割使用各种技术，包括传统图像处理方法和深度学习方法。传统方法包括边缘检测、阈值分割和区域生长。然而，深度学习技术，如卷积神经网络（CNN）和
            U-Net，已经在肺癌图像分割中取得了显著的成功。
          </p>
        </div>
      </div>
      <div class="upLoad" v-loading="loading">
        <h3 style="color: #a38334; margin-bottom: 30px">
          若对我们的技术有兴趣，欢迎在此试用！
        </h3>
        <div class="scan" @click="openFileInput">
          <el-icon size="80"><Plus /></el-icon>
          <input
            ref="fileInput"
            type="file"
            accept="image/*"
            class="go-upload-input"
            style="display: none"
            @change="handleFileChange"
          />
        </div>
        <div class="load" @click="upLoad" :disabled="!selectedFile">
          <h1>上传图像</h1>
        </div>
        <p v-if="selectedFile">已选择文件: {{ selectedFile.name }}</p>
        <el-button
          v-if="selectedFile"
          @click="startSeg"
          type="primary"
          size="large"
          >开始分割</el-button
        >
        <div v-if="uploadProgress !== null">
          <progress :value="uploadProgress" max="100">
            {{ uploadProgress }}%
          </progress>
        </div>
        <div v-if="uploadError">{{ uploadError }}</div>
        <div v-if="uploadSuccess">{{ uploadSuccess }}</div>
      </div>
      <contact-us></contact-us>
    </el-scrollbar>
  </div>
  <!--展示分割之后的弹窗-->
  <el-dialog v-model="showresult" title="分割图像结果">
    <div style="display: flex; flex-direction: column; align-items: center">
      <img :src="segresult" alt="result" style="margin-bottom: 10px" />
    </div>
  </el-dialog>
</template>

<script>
import ContactUs from "@/components/ContactUs.vue";
import CaseInfo from "@/components/CaseInfo.vue";
import { useRoute, useRouter } from "vue-router";
import { ref, watch } from "vue";
import { post } from "@/utils";
import common from "../common/common";
import axios from "axios";
import { ElMessage } from "element-plus";
export default {
  name: "ImageCut",
  components: { ContactUs, CaseInfo },
  props: {
    name: { type: String, default: "file" },
    action: {
      type: String,
      required: true,
    },
  },
  setup() {
    //flag为上传

    const route = useRoute(); // 使用 useRoute 获取当前路由对象
    const router = useRouter(); // 使用 useRouter 获取路由实例
    const navigateToLogin = () => {
      router.push("/login");
    };
    const navigateToPatientInfo = () => {
      router.push("/patientInfo");
    };
    const navigateToClassicalCase = () => {
      router.push("/classicalCase");
    };
    const navigateToImageCut = () => {
      router.push("/imageCut");
    };
    const navigateToAboutView = () => {
      router.push("/aboutView");
    };
    const navigateToHome = () => {
      router.push("/");
    };
    const navigateToChat = () => {
      router.push("/chatView");
    };
    const selectedFile = ref(null);
    const uploadProgress = ref(null);
    const uploadError = ref(null);
    const uploadSuccess = ref(null);
    const showModal = ref(false);
    const dialogWidth = ref("60%"); // 初始宽度
    const dialogHeight = ref("80%"); // 初始高度
    //打开分割后的图片详情
    const showresult = ref(false);
    const flag = ref(false);
    const loading = ref(false);
    const segresult = ref("");
    const text = ref("");
    const user = ref("");

    const openFileInput = () => {
      const fileInput = document.querySelector('input[type="file"]');
      if (fileInput) {
        fileInput.click();
      }
    };

    const handleFileChange = (event) => {
      selectedFile.value = event.target.files[0];
    };

    const startSeg = async () => {
      flag.value = true;
      upLoad();
    };

    const apiUrl = "";
    const requestData = "";

    const upLoad = async () => {
      const formData = new FormData();
      showModal.value = true;
}

      if (selectedFile.value) {
        console.log("selectedFile.value", selectedFile.value.name);
        formData.append("image", selectedFile.value);
        const username = localStorage.getItem("username");
        console.log("这里的username是" + username);
        //设置匿名用户使用的用户名
        if (username === null) {
          user.value = "null";
        } else {
          user.value = username;
        }

        formData.append("username", user.value);
      }
      if(flag.value == true){
        console.log("前端调用分割功能")
         try{
            loading.value = true
            const res = await axios.post(common.backend_prefix+"/pubfunc",formData,{responseType:'blob'})
            
            if(res.data.status == 'fail'){
              loading.value = false
              ElMessage.error(res.data.message)
            }else{
              loading.value = false
              let blob  = new Blob([res.data],{type:res.data.type})
              const url = URL.createObjectURL(blob)
              segresult.value = url
              console.log("结果:"+segresult.value)
              ElMessage.success("分割成功")
              showresult.value = true
            }
          }catch(error){
            console.log(error)
            loading.value = false
          }finally{
            loading.value = false
          }
      }
    };
    const minimize = () => {
      // 实现最小化逻辑
      dialogWidth.value = "30%";
      dialogHeight.value = "30%";
    };
    const maximize = () => {
      // 实现最大化逻辑
      dialogWidth.value = "100%";
      dialogHeight.value = "100%";
    };
    const close = () => {
      showModal.value = false;
      dialogWidth.value = "50%"; // 关闭时恢复默认宽度
      dialogHeight.value = "80%"; // 关闭时恢复默认高度
    };

        return {
        navigateToLogin,
        navigateToPatientInfo,
        navigateToClassicalCase,
        navigateToImageCut,
        navigateToAboutView,
        navigateToHome,
        navigateToChat,
        handleFileChange,
        upLoad,
        openFileInput,
        minimize,
        maximize,
        close,
        startSeg,
        showModal,
        dialogWidth,
        dialogHeight,
        selectedFile,
        uploadProgress,
        uploadError,
        uploadSuccess,
        showresult,
        loading,
        segresult,
        text,
        user,
        }; 
    }
  }
}
</script>

<style lang='less' scoped>
*,
html,
body {
  margin: 0;
  padding: 0;
}
.myScrollbar {
  &::-webkit-scrollbar {
    width: 6px; /* 滚动条宽度 */
    height: 6px; /* 滚动条高度 */
  }

  &::-webkit-scrollbar-thumb {
    background-color: #888; /* 滑块的背景色 */
    border-radius: 3px; /* 滑块的圆角 */
  }
}
.navbar {
  width: 100%;
  height: 400px;
  background-image: url("../assets/bgcCut.jpg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  .nav:hover {
    color: #1246a0;
    cursor: pointer;
  }

  .title {
    font-size: 30px;
    color: #fff;
    margin-top: 20px;
    margin-left: 20px;

    .titleText {
      font-weight: bold;
      text-shadow: 0 0 1px black, 0 0 1px black, 0 0 1px black;
    }
  }

  .eng {
    font-size: 15px;
    color: #fff;
    margin-left: 20px;
  }

  .nav {
    font-size: 20px;
    color: #fff;
    margin-left: 20px;
    cursor: pointer;
    /* height: 100%; */
    display: flex;
    align-items: center;
    margin-top: 35px;
  }

  .item {
    background-color: purple !important;
  }
  .middleTitle {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    width: 500px;
    height: 200px;
    text-align: center;
    margin: 0 auto;
    .bigTitle {
      font-size: 45px;
      color: #fff;
      font-weight: bold;
      /* 黑色阴影 */
      text-shadow: 0 0 1px black, 0 0 1px black, 0 0 1px black;
    }
    .bigTranslate {
      font-size: 16px;
      color: #fff;
      margin-top: 10px;
      font-weight: bold;
    }
  }
}
.container {
  .algorithm {
    padding-top: 50px;
    display: flex;
    width: 1200px;
    height: auto;
    margin: 0 auto;
    text-align: left;

    .leftImg {
      width: 629px;
      height: 403px;
      margin-right: 30px;
    }
    p {
      margin: 22px 0 8px 0;
      color: #71798d;
      font-size: 16px;
      line-height: 24px;
    }
    .advantage {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      color: #9ba0b7;
      font-size: 14px;
      span {
        margin-top: 30px;
      }
    }
  }
  .show {
    display: flex;
    background-color: #efefef;
    justify-content: center;
    align-items: center;
    span {
      font-size: 20px;
      color: black;
      margin-bottom: 20px;
    }
    .left,
    .right {
      display: flex;
      flex-direction: column;
      padding: 10px 20px 10px 40px;
    }
    .left {
      margin-left: 90px;
    }
    .showImg {
      width: 629px;
    }
  }
  .describe {
    display: flex;
    background-color: #fbfbfb;
    position: relative;
    overflow: hidden; /* 隐藏溢出的内容 */
    margin-bottom: 10px;
    justify-content: center;
    .left {
      padding-top: 50px;
      display: flex;
      flex-direction: column;
      height: auto;
      text-align: left;
      z-index: 2;
      margin-left: 160px;
      width: 619px;
    }
    .right {
      padding-top: 50px;
      z-index: 2;
      margin-left: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .left1 {
      padding-top: 50px;
      display: flex;
      flex-direction: column;
      height: auto;
      text-align: left;
      z-index: 2;
      width: 619px;
      margin-left: 50px;
    }
    .right1 {
      padding-top: 50px;
      z-index: 2;
      display: flex;
      justify-content: center;
      align-items: center;
      margin-left: 160px;
    }
    h4 {
      margin-top: 10px;
    }
    p {
      margin: 22px 0 8px 0;
      color: #71798d;
      font-size: 16px;
      line-height: 24px;
    }
    .advantage {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      color: #9ba0b7;
      font-size: 14px;
      span {
        margin-top: 30px;
      }
    }
  }
  .describe::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: linear-gradient(#efefef 1px, transparent 1px),
      linear-gradient(90deg, #efefef 1px, transparent 1px); /* 交替设置田字格格子颜色和透明间隔 */
    background-size: 20px 20px; /* 调整格子大小 */
  }
  .upLoad {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #efefef;
    height: 600px;
    .scan {
      width: 500px;
      height: 200px;
      border: 3px dashed #333333;
      display: flex;
      justify-content: center;
      align-items: center;
      .iconPlus {
        width: 80px;
        height: 80px;
      }
    }
    .load {
      margin-top: 20px;
      margin-bottom: 20px;
      font-size: 20px;
      color: #333333;
    }
  }
}
</style>