<template>
  <el-card shadow="hover" :body-style="{ padding: '20px' }">
    <el-row class="card-header">
      <p style="display:none">{{product.id}}</p>
      <el-button
        class="unLikeBtn"
        @click="unLike(product.id)"
        type="text"
        title="不喜欢"
        v-if="unLike_disable"
      >
        <i class="el-icon-close"></i>
      </el-button>
    </el-row>
    <router-link :to="{path: '/item',query: {id:product.id}}">
      <el-row class="card-img">
        <el-image :src="imgUrl" class="image" fit="scale-down" lazy>
          <div slot="error" class="image-slot">
            <span>加载失败</span>
          </div>
        </el-image>
      </el-row>
      <el-row class="card-name">
        <span class="name">{{product.name}}</span>
      </el-row>
      <el-row class="card-info">
        <span class="info">{{product.info}}</span>
      </el-row>
      <el-row class="card-price">
        <p class="price">￥{{product.price}}</p>
      </el-row>
    </router-link>
  </el-card>
</template>

<script>
export default {
  props: {
    product: {
      type: Object
    },
    imgUrl: {
      type: String,
      default () {
      }
    },
    unLike_disable: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
    }
  },
  methods: {
    unLike (pid) {
      // 让父组件删除此组件
      this.$emit('unlike', '')
      this.$axios.post("/unlike/"+pid)
    }
  }
}
</script>

<style scope>
.el-card:hover {
  transform: translate(0px, -4px);
}
.el-card {
  padding: 0;
  height: 300px;
  width: 180px;
  border-radius: 0.5em;
  background: linear-gradient(
    145deg,
    var(--color-gradient-start),
    var(--color-gradient-stop)
  );
  --color-gradient-start: #ffffff;
  --color-gradient-stop: #ffffff;
  --color-outset-start: #ececec;
  --color-outset-stop: #ececec;
  --color-inset-start: rgba(0, 0, 0, 0);
  --color-inset-stop: rgba(0, 0, 0, 0);

  box-shadow: 0.4em 0.4em 1em var(--color-outset-start),
    -0.4em -0.4em 1em var(--color-outset-stop),
    inset 0.2em 0.2em 0.4em var(--color-inset-start),
    inset -0.2em -0.2em 0.4em var(--color-inset-stop);
}
a {
  text-decoration: none;
  outline: none;
}
.router-link-active {
  text-decoration: none;
}
.card-img {
  display: block;
  height: 140px;
  width: 140px;
}
.image-slot {
  display: inline-block;
  width: 100%;
  line-height: 150px;
  border-radius: 5px;
  color: #999;
  font-weight: 100;
  background-color: rgba(214, 214, 214, 0.3);
}
.card-header {
  width: 100%;
  height: 10px;
}

.card-name {
  height: 20px;
  color: black;
  /* color: rgb(105, 105, 105); */
  overflow: hidden;
}
.card-info {
  height: 50px;
  overflow: hidden;
}
.card-price {
  height: 40px;
  overflow: hidden;
}
.unLikeBtn {
  color: rgba(0, 0, 0, 0.3);
  float: right;
  margin: 0px auto;
  margin-top: -26px;
  margin-right: -16px;
}
.unLikeBtn:hover {
  background-color: rgb(161, 11, 11);
  color: white;
}
.el-card:hover .unLikeBtn {
  display: block;
  width: 16px;
  height: 16px;
}
.image {
  width: 100%;
  height: 100%;
  display: block;
}
.info {
  overflow: hidden;
  font-size: 13px;
  color: #999;
  word-break: break-all;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  text-overflow: ellipsis;
}
.name {
  /* font-weight: 550; */
  overflow: hidden;
  font-size: 15px;
  word-break: break-all;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
  text-overflow: ellipsis;
}
.price {
  color: rgb(223, 7, 7);
  font-weight: bold;
}
</style>
