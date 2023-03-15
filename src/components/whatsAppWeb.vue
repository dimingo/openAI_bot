<template>
    <div class="h-screen ">


        <div class="z-20 overflow-y-scroll  scroll-smooth  pt-5 pb-32 mx-6 ">
            <div class="messages  " v-for="(message, index) in messages" :key="message.id">

                <div class="flex text-sm text-gray-500 italic" v-if="message.from !== 'me'">
                    <img v-if="message.from !== 'me'" :src="message.avatar" :alt="message.from"
                    class="message-avatar flex " />
                    {{ message.id}}

                </div>
              
               
                <div :class="[message.from === 'me' ? 'outgoing-message flex' : 'incoming-message ']">
                    {{ message.text }}
                </div>


            </div>


        </div>
        






        <div
            class="  bg-black items-center  fixed bottom-0 left-0 w-full border-t md:border-t-0 dark:border-white/20 md:border-transparent md:dark:border-transparent md:bg-vert-light-gradient bg-gray dark:bg-gray-800 md:!bg-transparent dark:md:bg-vert-dark-gradient">
            <form @submit.prevent="userInput"
                class="stretch mx-2 flex flex-row gap-3  last:mb-2 md:last:mb-6 lg:mx-auto lg:max-w-3xl lg:p-4">
                <div class="relative flex h-full flex-1 md:flex-col">
                    <div class="ml-1 mt-1.5 md:w-full md:m-auto md:flex md:mb-2 gap-2 justify-center"></div>
                    <div
                        class="flex flex-col w-full py-2 px-3 flex-grow md:py-3 md:pl-4 relative border border-black/10 bg-white dark:border-gray-900/50 dark:text-white dark:bg-gray-700 rounded-md shadow-[0_0_10px_rgba(0,0,0,0.10)] dark:shadow-[0_0_15px_rgba(0,0,0,0.10)]">
                        <input tabindex="0" v-model="newMessage" type="text" placeholder="What can I help you with? "
                            style="max-height: 200px; height: 24px; overflow-y: hidden;" rows="1"
                            class="m-0 w-full resize-none border-0 bg-transparent p-5 pr-7 focus:ring-0 focus-visible:ring-0 dark:bg-transparent" />
                        <button type="submit"
                            class="absolute hover:text-gray-500 p-2 rounded-md text-green-500 bottom-1.5 right-1 md:bottom-2.5 md:right-2 hover:bg-gray-100 dark:hover:text-gray-400 dark:hover:bg-gray-900 disabled:hover:bg-transparent dark:disabled:hover:bg-transparent"><svg
                                stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 20 20"
                                class="h-7 w-7  " height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z">
                                </path>
                            </svg></button>
                    </div>
                </div>
            </form>

        </div>



    </div>


</template>
  
<script>
import botPic from '../assets/images/chatbot.png'
import moment from 'moment';


export default {
    data() {
        return {
            messages: [],
            newMessage: ''
        }
    },
    methods: {
        async userInput() {
            this.messages.push({
                time: Date.now(),
                from: 'me',
                text: this.newMessage
            })
            const { data } = await(this.$http.post(
                'http://127.0.0.1:8000/api/generate',
                { user_input: this.newMessage }
                ));
           
                this.messages.push(
                   { avatar: botPic,
                    id: moment(new Date()).format('YYYY-MM-DD hh:mm a'),
                    from: 'them',
                    text: data.text
                });
                this.newMessage = ''
                
        },
        sendMessage() {
            // Add the new message to the messages array

            this.messages.push({
                id: Date.now(),
                from: 'me',
                text: this.newMessage
            }, {
                id: new Date(Date.now()),
                from: 'chatbot',
                text: 'Hello',


            })
            // Clear the new message input
            this.newMessage = ''
        }
    }
}
</script>
  
<style>
/* Add some style to the chat app */
.scrollbtm {
    overflow-y: scroll;
    overscroll-behavior-y: contain;
    scroll-snap-type: y proximity;
}

.chat-app {
    display: flex;
    flex-direction: column;
}

.chat-screen {
    flex: 1;
    display: flex;
    flex-direction: column;

    top: 0;
    z-index: 100;
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    overflow-x: hidden;
    overflow-y: scroll;

}

.messages {
    flex: 1;
    display: flex;
    flex-direction: column;
    padding: 20px;
}

.outgoing-message {
    align-self: flex-end;
    background: #3bc914;
    border-radius: 20px;
    margin-bottom: 20px;
    padding: 10px 20px;
}

.incoming-message {
    align-self: flex-start;
    background: rgb(51, 53, 51);
    color: #e6e6e6;
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
  