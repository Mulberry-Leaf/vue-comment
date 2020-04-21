<template>
  <div class="reply-item-wrap">
    <div class="reply-actor">
      <span>{{reply.commentator}}</span>
      <span class="spread" @click="triggerChild">[{{showChild ? '-' : '+'}}]</span>
    </div>
    <div v-show="showChild">
      <p class="reply-content">{{reply.content}}</p>
      <div class="reply-btn-wrap">
        <span class="reply-btn" @click.self="replyOther(reply)">回复</span>
      </div>
      <div v-if="showReply">
        <ReplyTextArea v-model="othersReply" @publishReply="publishReply(reply)"></ReplyTextArea>
      </div>
      <ul v-if="reply.child && reply.child.length">
        <li v-for="(item, index) in reply.child" :key="index" >
          <CommentReplyItem :reply="item"></CommentReplyItem>
        </li>
      </ul>
    </div>
    
  </div>
</template>

<script>
import ReplyTextArea from './TextArea.vue';
import Bus from '../utils/eventBus';  

export default {
  name: 'CommentReplyItem',
  props: {
    reply: Object,
    default: {},
  },
  components: {
    ReplyTextArea,
  },
  data() {
    return {
      showChild: true,
      showReply: false,
      othersReply: '',
    };
  },
  methods: {
    triggerChild() {
      this.showChild = !this.showChild;
    },
    replyOther() {
      this.showReply = !this.showReply;
    },
    publishReply(val) {
      this.showReply = false;
      Bus.$emit('replyOther', {
        comment: val,
        reply: this.othersReply,
      });
      this.othersReply = '';
    }
  }
}
</script>

<style lang="less" scoped>
.reply-item-wrap {
  .reply-actor {
    color: #3871a8;
    font-weight: bold;
    font-size: 14px;
    span {
      display: inline-block;
    }
    .spread {
      margin-left: 20px;
      cursor: pointer;
    }
  }
  .reply-wrap-item {
    margin: 10px 0;
  }
  .reply-content {
    font-size: 14px;
    line-height: 30px;
  }
  .reply-btn-wrap {
    border-bottom: 1px solid #f2f2f2;
    margin-bottom: 10px;
  }
  .reply-btn {
    color: #999;
    font-size: 12px;
  }
}

</style>
