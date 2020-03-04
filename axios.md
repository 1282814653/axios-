```js
//  这是在vue 中使用
import axios from "axios";
import qs from "qs";
// 设置 请求的 默认网址
// axios.defaults.baseURL = "http://59.110.138.169"; // 生产环境地址
if (process.env.NODE_ENV == "development") {
  axios.defaults.baseURL = "http://59.110.138.169"; // 生产环境地址
} else {
  axios.defaults.baseURL = "http://59.110.138.168"; // 开发环境地址
}

// 设置 超时的事件
axios.defaults.timeout = 5000;
// token 的 设置
// axios.defaults.headers.common["token"] = token;

// 设置请求 头
axios.interceptors.request.use(
  // 请求成功做的 处理
  function(config) {
    //   当请求的格式 是 post 的时候内容 序列化 输出 如果不是 直接返回数据
    if (config.method == "post") {
      config.data = qs.stringify(config.data);
    }
    return config;
  },
  //   请求失败做的 处理
  function(error) {
    return Promise.reject(error);
  }
);
// 设置相应头
axios.interceptors.response.use(
  // 成功的 回调
  function(config) {
    return config.data;
  },
  //   失败的回调
  function(error) {
    return Promise.reject(error);
  }
);

// 导出 axios
export default axios;

// 导出后 需要 把 axios 引入 到 main.js 中的
//  然后在vue 实例上挂载  Vue.prototype.$ajax = axios;

```