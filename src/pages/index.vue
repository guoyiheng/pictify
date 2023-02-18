<script setup lang="ts" generic="T extends any, O extends any">
import { UseImage } from '@vueuse/components'

defineOptions({
  name: 'IndexPage',
})

/**
 * step1 get comment data
 */
const source = $ref('https://m.dongqiudi.com/article/3278234.html')
const hotSize = $ref('10')
watchEffect(() => {
  if (Number(hotSize) >= 100)
    hotSize = '10'
})

async function handleGetComment() {
  // use regex to get article id
  const articleId = source.match(/\d+/)?.[0]
  if (!articleId)
    return
  const commentUrI = `https://api.dongqiudi.com/v2/article/${articleId}/hot?size=${hotSize}`
  // open link in new tab
  window.open(commentUrI, '_blank')
}

/**
 * step2 analysis comment data
 */
const result: any = $ref('')
const mediaList: any = $ref([])
function handleAnalysis() {
  try {
    // 解析出来评论数据
    const commentData: any = JSON.parse(result)
    const commentList = commentData.data.comment_list
    // 取出所有的 attachments
    mediaList = commentList.map((item: any) => item.attachments).filter((item: any) => item).flat().map((item: any) => item.url.split('?')[0])
  }
  catch (error) {

  }
}

/**
 * preview image
 */
const show = $ref(false)
const previewSource = $ref('')
function handlePreview(source: string) {
  // show = true
  // previewSource = source
}
</script>

<template>
  <div>
    <div i-mdi:watermark text-4xl inline-block />
    <p>
      <a rel="noreferrer" href="https://github.com/guoyiheng/pictify" target="_blank">
        Pictify
      </a>
    </p>
    <p>
      <em text-sm op75> 获取懂球帝评论区无水印图片 </em>
    </p>

    <div py-4 />

    <div flex="~ col" gap-4>
      <label
        for="comment-id"
        class="block font-medium"
      >
        1️⃣ 帖子链接：
      </label>

      <div>
        <TheInput
          id="comment-id"
          v-model="source"
          placeholder="请输入帖子链接"
          autocomplete="false"
          w-full
        />
      </div>
      <div>
        <label for="comment-count"> 获取数量： </label>
        <TheInput
          id="comment-count"
          v-model="hotSize"
          autocomplete="false"
          w="60px"
        />
      </div>
      <div>
        <button
          class="btn py-2"
          :disabled="!source"
          w-full
          @click="handleGetComment"
        >
          获取评论数据
        </button>
      </div>
    </div>
    <div py-4 />
    <div flex="~ col" gap-4>
      <label
        for="comment-result"
        class="block font-medium"
      >
        2️⃣ 粘贴返回结果：
      </label>
      <div>
        <TheTextArea
          id="comment-result"
          v-model="result"
          placeholder="请粘贴返回结果"
          autocomplete="false"
          w-full
        />
      </div>
      <div>
        <button
          class="btn py-2"
          :disabled="!source"
          w-full
          @click="handleAnalysis"
        >
          查看图片
        </button>
      </div>
    </div>
    <div py-4 />
    <div flex="~ col" gap-4>
      <label
        class="block font-medium"
      >
        3️⃣ 图片展示：
      </label>
      <div grid="~ cols-2" gap-2>
        <div v-for="media in mediaList" :key="media" @click="handlePreview(media)">
          <UseImage :src="media">
            <template #loading>
              Loading..
            </template>
            <template #error>
              Failed
            </template>
          </UseImage>
        </div>
      </div>
    </div>
    <div py-4 />
    <ImagePreview v-model:show="show" :source="previewSource" />
    <div py-4 />
  </div>
</template>
