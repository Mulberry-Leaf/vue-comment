<template>
  <div class="article-content">
    <h3>{{articleDetail.title}}</h3>
    <div class="article-body" v-html="articleDetail.content"></div>
    <div class="reply-title">精彩评论</div>
    <div class="reply-wrap">
      <div  class="reply-list">
        <ul>
          <li v-for="item in commentList"   :key="item.commentId">
            <CommentReplyItem :reply="item"></CommentReplyItem>
          </li>
        </ul>
      </div>
    </div>
    <div class="reply-title">发表评论</div>
    <ReplyTextArea v-model="replyContent" @publishReply="publishReply"></ReplyTextArea>
  </div>
</template>

<script>
import { articleDetail, commentList } from './utils/data';
import CommentReplyItem from './components/CommentReplyItem.vue';
import ReplyTextArea from './components/TextArea.vue';
import Bus from './utils/eventBus';  


export default {
  components: {
    CommentReplyItem,
    ReplyTextArea,
  },
  data() {
    return {
      articleDetail,
      commentList,
      replyContent: '',
      userName: 'admin',
    }
  },
  methods: {
    publishReply() {
      this.commentList.push({
        commentId: new Date().getTime(),
        articleId: this.articleDetail.articleId,
        content: this.replyContent,
        commentator: this.userName,
      });
      this.replyContent = '';
    },
    reply(val) {
      const { reply, comment } = val;
      if (!comment.child) {
        comment.child = [];
      }
      comment.child.push({
        commentId: new Date().getTime(),
        articleId: this.articleDetail.articleId,
        content: reply,
        commentator: this.userName,
      });
    }
  },
  mounted() {
    Bus.$on('replyOther', this.reply);
  },
  beforeDestroy() {
    Bus.$off('replyOther', this.reply);
  },
};
</script>

<style lang="less">
.article-content {
  width: 1000px;
  margin: auto;
  padding: 10px;
  border: 1px solid transparent;
  background: #fff;
  h3 {
    margin: 20px 0;
    text-align: center;
  }
  .reply-title {
    margin: 20px 0;
    line-height: 30px;
    padding-left: 10px;
    color: #fff;
    background: #3871a8;
  }
  .reply-wrap {
    ul {
      margin-left: 20px;
    }
    li {
      list-style: none;
      margin-bottom: 10px;
    }
  }
  .article-body {
    p {
      font-size: 14px;
      line-height: 36px;
    }
  }
}
</style>