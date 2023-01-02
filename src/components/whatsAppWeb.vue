<template>
    <div class="chat-app flex h-80   flex-col-reverse">
        <!-- Chat screen -->
        <div class="chat-screen   bg-gray-900 h-full w-full p-14  overflow-y-auto">
            <!-- Chat messages -->
            <div class="messages flex" v-for="message in messages" :key="message.id">
                <img v-if="message.from !== 'me'" :src="message.avatar" :alt="message.from"
                    class="message-avatar flex " />
                <div :class="[message.from === 'me' ? 'outgoing-message flex' : 'incoming-message ']">

                    {{ message.text }}
                </div>
            </div>


        </div>
        <!-- Chat input -->

    </div>
    <div
        class="absolute bottom-0 left-0 w-full border-t md:border-t-0 dark:border-white/20 md:border-transparent md:dark:border-transparent md:bg-vert-light-gradient bg-gray dark:bg-gray-800 md:!bg-transparent dark:md:bg-vert-dark-gradient mb-3">
        <form @submit.prevent="sendMessage"
            class="stretch mx-2 flex flex-row gap-3 pt-2 last:mb-2 md:last:mb-6 lg:mx-auto lg:max-w-3xl lg:pt-6">
            <div class="relative flex h-full flex-1 md:flex-col">
                <div class="ml-1 mt-1.5 md:w-full md:m-auto md:flex md:mb-2 gap-2 justify-center"></div>
                <div
                    class="flex flex-col w-full py-2 pl-3 flex-grow md:py-3 md:pl-4 relative border border-black/10 bg-white dark:border-gray-900/50 dark:text-white dark:bg-gray-700 rounded-md shadow-[0_0_10px_rgba(0,0,0,0.10)] dark:shadow-[0_0_15px_rgba(0,0,0,0.10)]">
                    <input tabindex="0" v-model="newMessage" type="text" placeholder="Type a message"
                        style="max-height: 200px; height: 24px; overflow-y: hidden;" rows="1"
                        class="m-0 w-full resize-none border-0 bg-transparent p-0 pr-7 focus:ring-0 focus-visible:ring-0 dark:bg-transparent" />
                    <button type="submit"
                        class="absolute p-1 rounded-md text-gray-500 bottom-1.5 right-1 md:bottom-2.5 md:right-2 hover:bg-gray-100 dark:hover:text-gray-400 dark:hover:bg-gray-900 disabled:hover:bg-transparent dark:disabled:hover:bg-transparent"><svg
                            stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 20 20"
                            class="h-4 w-4 rotate-90" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
                            <path
                                d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z">
                            </path>
                        </svg></button>
                </div>
            </div>
        </form>

    </div>

</template>
  
<script>
import botPic from '../assets/images/chatbot.png'

export default {
    data() {
        return {
            messages: [],
            newMessage: ''
        }
    },
    methods: {
        async userInput(text) {
            const { data } = await this.$http.post(
                'http://127.0.0.1:8000/api/generate',
                { user_input: "what do you understand by the term business?" }
            );
            console.log(data);
            // example response: { id: 1, name: "something" }
        },
        sendMessage() {
            // Add the new message to the messages array

            this.messages.push({
                id: Date.now(),
                from: 'me',
                text: this.newMessage
            }, {
                id: Date.now(),
                from: 'them',
                text: 'Hello',
                avatar: botPic,

            })
            // Clear the new message input
            this.newMessage = ''
        }
    }
}
</script>
  
<style>
/* Add some style to the chat app */
.chat-app {
    display: flex;
    flex-direction: column;
    height: 100%;
}

.chat-screen {
    flex: 1;
    display: flex;
    flex-direction: column;
}

.messages {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 20px;
}

.outgoing-message {
    align-self: flex-end;
    background: #e6e6e6;
    border-radius: 20px;
    margin-bottom: 20px;
    padding: 10px 20px;
}

.incoming-message {
    align-self: flex-start;
    background: #ccc;
    border-radius: 20px;
    margin-bottom: 20px;
    padding: 10px 20px;
}

.chat-input {
    padding: 20px;
}

.chat-input form {
    display: flex;
}

.chat-input input {
    flex: 1;
    border: none;
    padding: 10px;
    font-size: 16px;
    border-radius: 20px 0 0 20px;
}

.chat-input button {
    border: none;
    background: #4caf50;
    color: white;
    padding: 10px;
    font-size: 16px;
    border-radius: 0 20px 20px 0;
}

.message-avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 10px;
}
</style>
  