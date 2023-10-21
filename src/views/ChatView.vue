<template>
  <div class="container">
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
      </el-row>
      <div class="infoBox">
        <div class="left">
          <div
            class="card"
            v-for="(item, index) in MesList"
            :key="index"
            @click="selectChat(index)"
          >
            <img :src="item.headUrl" alt="" srcset="" />
            <img
              src="../assets/patient.jpg"
              alt=""
              srcset=""
              class="card-image"
            />
            <div class="card-content">
              <div class="mid">
                <div class="top">
                  <div class="card-title">{{ item.name }}</div>
                  <div class="card-title">{{ item.sex }}</div>
                  <div class="card-title">{{ item.age }}</div>
                </div>
                <div class="card-text">
                  {{ item.info }}
                </div>
              </div>
              <button class="card-button">
                {{ item.status }}
              </button>
            </div>
          </div>
        </div>
        <div class="right">
          <div class="top">
            <div class="des">
              <h3>病人描述:</h3>
              <text>{{ MesList[id].info }}</text>
            </div>
            <div class="info">
              <h3>病人信息:</h3>
              <text
                >{{ MesList[id].name }} {{ MesList[id].sex }}
                {{ MesList[id].age }}岁</text
              >
            </div>
          </div>
          <div class="mid">
            <div v-for="chat in chatList[id]" :key="chat.id" class="mes">
              <div :class="{ doctor: chat.isDoctor, patient: !chat.isDoctor }">
                <img
                  v-if="!chat.isDoctor"
                  src="../assets/patient.jpg"
                  alt=""
                  srcset=""
                  class="avatar"
                />
                <div class="mes">
                  <text>{{ chat.info }}</text>
                </div>
                <img
                  v-if="chat.isDoctor"
                  src="../assets/doctor.png"
                  alt=""
                  srcset=""
                  class="avatar"
                />
              </div>
            </div>
          </div>
          <div class="bottom">
            <input type="text" class="chat-input" placeholder="输入消息" />
            <button class="send-button">发送</button>
          </div>
        </div>
      </div>
      <contact-us></contact-us>
    </el-scrollbar>
  </div>
</template>
<script lang="ts">
import Vue, { ref } from "vue";
import { useRouter } from "vue-router";
export default {
  name: "ChatView",
  setup() {
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
    const MesList = ref([
      {
        name: "王白白",
        sex: "男",
        age: "20",
        info: "天天头疼,掉头发，睡不好觉，持续很久了，是什么怎么回事呢? ?",
        status: "已回复",
        headUrl: "../assets/patient.jpg",
      },
      {
        name: "李德",
        sex: "男",
        age: "60",
        info: "发烧,而且还伴有流涕的症状",
        status: "已回复",
        headUrl: "../assets/patient.jpg",
      },
      {
        name: "刘东",
        sex: "男",
        age: "20",
        info: "失眠，无法入睡 ",
        status: "未读",
        headUrl: "../assets/patient.jpg",
      },
    ]);
    const chatList = [
      [
        {
          id: 0,
          info: "这种症状是什么时候开始的呢? 想服用一些药物吗?",
          isDoctor: true,
        },
        {
          id: 1,
          info: "大概已经有两周左右的时间了，期间自己吃够一些药，但是作用不是很大...",
          isDoctor: false,
        },
        {
          id: 2,
          info: "你好，你的掉发和头痛考虑还是失眠不好失眠导致的。失眠多跟长期过度用脑，起居无规律，脏腑失调，情志郁结等因素有关可在医生的指导下使用可以口服;谷维素片+维生素B1片+安神补脑液养血安神丸或者枣仁安神颗粒进行治疗，入睡困难建议口服地西洋片,建议要平时要多吃坚果类食物，例如核桃，葵花籽等，合理安排自己的作息时间，避免劳累，保持心情舒畅也是很重要的，另外养成良好的休息习惯,避免劳累,缓解自己的压力,保持愉快的心情.祝您早日康复!",
          isDoctor: true,
        },
      ],
      [
        {
          id: 0,
          info: "发烧流鼻涕首先应该补充大量的水分，摄入适量的瓜果蔬菜，同时要测量一下体温，如果体温过高，可以在医生的指导下口服退烧药。发烧流鼻涕应该是感冒引起的，一般不需要太过担心，保证良好的睡眠质量有利于身体的康复。",
          isDoctor: true,
        },
        {
          id: 1,
          info: "我这个可能是什么原因造成的呢？",
          isDoctor: false,
        },
        {
          id: 2,
          info: "发热一直流鼻涕可能是因为病毒性感冒、细菌性感冒、支气管炎等原因所引起，要对症处理，可以用解热镇痛药物、抗过敏药物进行局部的处理，比如选用氨加黄敏胶囊或者氯苯那敏等药物，都能起到不错的效果。其次，对症处理发烧，如果体温过高，超过38.5摄氏度以上，可以选择适当的退烧药物进行治疗，可以选用非甾体类抗炎药，比如牛黄安宫丸、布洛芬、芬必得等。",
          isDoctor: true,
        },
      ],
    ];
    const id = ref(0);
    const selectChat = (index: any) => {
      id.value = index;
      console.log(index);
    };

    return {
      MesList,
      id,
      chatList,
      navigateToLogin,
      selectChat,
      navigateToPatientInfo,
      navigateToClassicalCase,
      navigateToImageCut,
      navigateToAboutView,
      navigateToHome,
      navigateToChat,
    };
  },
};
</script>
<style lang="less" scoped>
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
  height: 90px;
  background-color: #2b86f1;

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
    height: 100%;
    display: flex;
    align-items: center;
  }

  .item {
    background-color: purple !important;
  }
}
.card {
  display: flex;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 40vw;
}
.card-image {
  margin-right: 10px;
  width: 40px;
  height: 40px;
}
.card-content {
  display: flex;
  justify-content: space-between;
}
.mid {
  width: 400px;
}
.card-title {
  font-weight: bold;
  font-size: 18px;
  margin-right: 6px;
}
.card-subtitle {
  color: #555;
  font-size: 14px;
}
.card-text {
  margin-top: 8px;
  text-align: left;
  margin-left: 15px;
  font-size: 13px;
  color: #888;
}
.card-button {
  width: 60px;
  height: 20px;
  margin-top: 10px;
  background-color: #93d2f3;
  border: none;
  border-radius: 20px;
}
.top {
  display: flex;
  align-items: center;
  padding: 10px;
}
.infoBox {
  display: flex;
  .right {
    width: 70vw;
    height: 80vh;
    display: flex;
    flex-direction: column;
    border-bottom: 1px solid darkgray;
    border-left: 1px solid darkgray;
    .top {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      .des,
      .info {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-left: 100px;
        text {
          margin-left: 20px;
        }
      }
    }
    .mid {
      width: 100%;
      .doctor {
        display: flex;
        justify-content: flex-end;
        .mes {
          width: 300px;
          height: auto;
          background-color: #fff;
          border-radius: 10px;
          margin-right: 10px;
          //灰色阴影
          box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
          text-align: left;
          padding: 10px;
        }
      }
      .patient {
        display: flex;
        justify-content: flex-start;
        .mes {
          width: 300px;
          height: auto;
          background-color: #fff;
          border-radius: 10px;
          margin-right: 10px;
          //灰色阴影
          box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
          text-align: left;
          padding: 10px;
        }
      }
    }
  }
}
.bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background-color: #f5f5f5;
  border-top: 1px solid #ccc;
  margin-top: 80px;
}

.chat-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-right: 10px;
}

.send-button {
  background-color: #2b86f1;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50px;
}
</style>