<template>
    <div class="feed" ref="feed">
        <ul v-if="contact">
            <li v-for="message in messages" :class="`message${message.to == contact.id ? ' sent' : ' received'}`" :key="message.id">
                <div class="text">
                    <p>{{ message.text }}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "MessagesFeed",
        props: {
            contact: {
                type: Object,
            },
            messages: {
                type: Array,
                required: true
            }
        },
        methods: {
            scrollToBottom() {
                setTimeout(() => {
                    this.$refs.feed.scrollTop = this.$refs.feed.scrollHeight - this.$refs.feed.clientHeight;
                }, 50)
            }
        },
        watch: {
            contact(contact) {
                this.scrollToBottom();
            },
            messages(messages) {
                this.scrollToBottom();
            }
        }
    }
</script>

<style lang="scss" scoped>
    ::-webkit-scrollbar {
        width: 6px;
    }

    /* Track */
    ::-webkit-scrollbar-track {
        background: #f1f1f1;
    }

    /* Handle */
    ::-webkit-scrollbar-thumb {
        background: #a8a8a8;
        border-radius: 2px;
    }

    /* Handle on hover */
    ::-webkit-scrollbar-thumb:hover {
        background: #7a7a7a;
    }
    .feed {
        background: #f1f1f17a;
        overflow: scroll;
        overflow-x: hidden;
        height: 100%;
        border-top: 1px solid #cfd0d1;
        border-bottom: 1px solid #cfd0d1;

        ul {
            list-style-type: none;
            padding: 5px;
            li {
                &.message {
                    margin: 5px;
                    width: 100%;
                    float: right;
                    .text {
                        border-radius: 5px;
                        padding: 12px;
                        display: inline-block;
                        word-break: break-word;
                        p {
                            text-align: left;
                            margin: 0;
                        }
                    }
                    &.received {
                        text-align: left;
                        max-width: 60%;
                        float: left;
                        margin-left: 20px;
                        .text {
                            color: black;
                            background: #E0E0E0;
                        }
                    }
                    &.sent {
                        max-width: 60%;
                        text-align: right;
                        margin-right: 30px;
                        .text {
                            color: white;
                            background: #3F51B5;
                        }
                    }
                }
            }
        }
    }
</style>
