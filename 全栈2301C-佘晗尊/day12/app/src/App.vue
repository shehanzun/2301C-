<template>
  <div id="box">
    <div id="content">
      <div id="img">
        <img src="./assets/txt.png" alt="" />
      </div>

      <h3 style="text-align: center">~今天我需要做的事情~</h3>

      <div id="inpbox">
        <input type="text" placeholder="请输入未完成的list" v-model="val" />
        <button @click="add" :class="isAdd ? 'activeAdd' : ''">添加</button>
      </div>

      <div class="content">
        <div
          v-for="it in data2"
          :key="it.tit"
          class="item"
          :style="{ animationName: it.checked ? 'active' : 'noactive' }"
          :class="it.checked ? 'activeItem' : 'noactive'"
        >
          <div class="left">
            <div @click="lei(it.id)">
              <span v-show="it.checked">V</span>
            </div>
            <span>{{ it.tit }}</span>
          </div>
          <div class="right" @click="del(it.id)">X</div>
        </div>
      </div>

      <div id="filterbox">
        <p
          @click="qie(index)"
          v-for="(it, index) in arr"
          :key="index"
          :class="index == active ? 'activeColor' : ''"
        >
          <span v-show="data.length > 0 && index == 0">{{ data.length }}</span>
          <span class="val">{{ it }}</span>
        </p>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      arr: ["无事项", "查看所有", "待完成", "已完成", "清空所有"],
      active: 1,
      isAdd: false,
      val: "",
      activeVal: false,
      data: JSON.parse(localStorage.getItem("data")) || [],
      data2: [],
    };
  },

  methods: {
    add() {
      if (this.val != "") {
        this.isAdd = true;
        setTimeout(() => {
          this.isAdd = false;
        }, 1500);

        let obj = {
          tit: this.val,
          checked: false,
          id: new Date().getTime(),
        };
        this.val = "";
        this.data.push(obj);

        localStorage.setItem("data", JSON.stringify(this.data));
      } else {
        alert("为空");
      }
    },

    qie(i) {
      this.active = i;
      if (i == 4) {
        this.data = [];
        localStorage.setItem("data", JSON.stringify(this.data));
        return;
      }

      if (i == 3) {
        this.data2 = this.data.filter((e) => e.checked);
        return;
      }

      if (i == 2) {
        this.data2 = this.data.filter((e) => !e.checked);
        return;
      }

      if (i == 1) {
        this.data2 = this.data;
      }
    },

    lei(ind) {
      let i = this.data.findIndex((item) => item.id == ind);
      this.data[i].checked = !this.data[i].checked;
      localStorage.setItem("data", JSON.stringify(this.data));
    },

    del(id) {
      let i = this.data.findIndex((item) => item.id == id);
      this.data.splice(i, 1);
      localStorage.setItem("data", JSON.stringify(this.data));
    },

    aa() {
      console.log(this.data.length)
      let val = document.querySelector(".val");
      if (this.data.length > 0) {
        val.innerHTML = "条事项";
      } else {
        val.innerHTML = "无事项";
      }
    },
  },

  watch: {
    data: {
      deep: true,
      immediate: true,
      handler(a) {
        if (this.active == 3) {
          this.data2 = a.filter((e) => e.checked);
          this.aa();
          return;
        }
        if (this.active == 2) {
          this.data2 = a.filter((e) => !e.checked);
          this.aa();

          return;
        }
        this.data2 = a;
        this.aa();
      },
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.left div {
  width: 20px;
  height: 20px;
  margin-right: 10px;
  border: 1px solid black;
}

.left {
  display: flex;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid black;
  padding: 10px;
  margin: 15px 30px;
  border-radius: 10px;
  animation-duration: 0.5s;
}
#box {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(90deg, #f4b6ba, #f6c2aa);
}
#content {
  width: 370px;
  height: 700px;
  border-radius: 15px;
  background-color: #fff;
}

#img {
  text-align: center;
  margin-top: 20px;
}

#inpbox button {
  background-color: #fff;
  padding: 3px 16px;
  border-radius: 6px;
  transform: rotate(5deg);
  margin-left: 20px;
}

#inpbox {
  margin-top: 40px;
  width: 100%;
  display: flex;
  height: 40px;
  justify-content: center;
  align-items: center;
}

#inpbox input {
  border: none;
  border-bottom: 3px dashed #f4b6ba;
  outline: none;

  width: 200px;
}

#filterbox {
  display: flex;
  justify-content: space-around;
  align-items: center;
  font-size: 14px;
  margin-top: 40px;
  padding: 0 25px;
}

.activeColor {
  color: white;
  padding: 4px 5px;
  border-radius: 7px;
  background-color: #ed7b52;
}

#filterbox p:hover {
  color: white;
  padding: 4px 5px;
  border-radius: 7px;
  background-color: #ed7b52;
}

#inpbox button:hover {
  padding: 4px 18px;
  font-size: 18px;
}

.activeAdd {
  background-color: #ed7b52 !important;
  color: white;
}

.activeItem {
  background-color: #ed7b52;
}

.noactive {
  background-color: #fff;
}

@keyframes active {
  0% {
    background-color: #fff;
  }

  100% {
    background-color: #ed7b52;
  }
}

@keyframes noactive {
  0% {
    background-color: #ed7b52;
  }

  100% {
    background-color: #fff;
  }
}
</style>
