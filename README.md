# Vue 3.0.0-beta、compositionを試用してみた
今回、Vue 3.0.0-beta、compositionをいち早く使って見ましたので
そこで得た知見を共有したいと思います。

Vue 3.0-betaへの変更は下記記事でまとめられていますのでこちらから変更可能です。

[環境構築で参考にした記事](https://qiita.com/mascii/items/331c084d8e2d6c68197f)

## Vue CLI環境

```bash
$ vue -V
@vue/cli 4.3.1
```

## compositionを使用したreactiveデータの描画方法

- 【従来】 => `data() { return { ... } }`

- 【composition使用】 => ` setup() { const state = reactive ({ ... }); return { state } } `

reactive関数の中は「プロパティ: '内容'」の形で記述

computedなどもreactive関数の中に記述します。(Counter.jsにサンプルコードあり)

```vue
<template>
  <div class="index">
    <h2>{{ state.title }}</h2>
    <div>{{ state.message }}</div>
    <div>{{ refMessage }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue';

export default defineComponent ({
  // ...省略
  setup() { 
    // 配列にまとめて格納
    const state = reactive ({
      title: 'Hello World',
      message: 'This is a Vue 3.0 - Beta',
    });
    
    // 単体で格納
    const refMessage = ref ('こんにちは');

    // 必ずreturnする
    return {
      state,
      refMessage
    }
  }
});
</script>
```

```vue
<template>
  <div class="index">  
    <!-- 従来の描画 -->
    <h2>{{ title }}</h2>
    <div>{{ message }}</div>
  </div>
</template>

<script  lang="ts">
export default {
    // 従来のreactive
    // Vue 3.0 - Beta - ではLegacyOptions(レガシー)になります
    data() {
        return {
            title: 'Hello World',
            message: 'This is a Vue 3.0 - Beta',
        }
    },
}
</script>
```

## ライフスタイル

```vue
<script lang="ts">
import { defineComponent, onMounted, onUpdated, onUnmounted } from 'vue';

export default defineComponent({
    // ...省略
    setup() {
        // ライフサイクルメソッド
        onMounted(() => {
            // レンダー後呼び出し
            console.log('描画しました');
        });
        onUpdated(() => {
            // 更新後呼び出し
            console.log('更新しました');
        });
    }
});
</script>
```

|  Vue 2.x  |  Compostion API  |
| ---- | ---- |
|  beforeCreate  |  -  |
|  created  |  -  |
|  beforeMount  |  onBeforeMount  |
|  beforeUpdate  |  onBeforeUpdate  |
|  beforeDestroy  |  onBeforeUnmount  |
|  destroyed  |  onUnmounted  |
|  errorCaptured  |  onErrorCaptured  |

## 感想

今回Vue3.0-betaを使ってみて、reactiveの記述方法など
従来と変わったところはありましたが個人的には目立った問題はなかった印象です。

1点注意点としては「Counter.vue」のところで
`count: {{ state.counts[0] }}`という配列の1番目を取る方法は
2xでは機能しないということ(3x〜記述可)。

まだまだBeta版ということで今後使っていく中で
いろいろ問題点も出てくるかと思うので
常に最新情報をキャッチアップしていくことが大切だと思いました。