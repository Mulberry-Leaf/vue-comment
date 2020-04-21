<template>
  <div>
    <textarea
      rows="5"
      cols="80"
      :value="reply"
      @input="updateReply($event.target.value)">
    </textarea>
    <div>
      <button class="publish-btn" @click="publish">发表</button>
    </div>
    
  </div>
  
</template>

<script>
export default {
  model: {
    prop: 'reply',
    event: 'sendReply',
  },
  props: {
    reply: {
      type: String,
      default: '',
    },
  },
  methods: {
    updateReply(value) {
      this.$emit('sendReply', value)
    },
    publish() {
      this.$emit('publishReply')
    }
  }
}
</script>

<style lang="less" scoped>
.publish-btn {
  background: #3871a8;
  color: #fff;
  text-align: center;
  padding: 10px 20px;
  border-radius: 4px;
  outline: none;
}
</style>