<template>
    <div id="app">
        <header>
            <div class="header-content">
                <img class="logo" src="@/assets/logo.png" alt="ChatALL" />
                <div class="column-icons">
                    <img
                        src="@/assets/column-1.svg"
                        @click="changeColumns(1)"
                        :class="{ 'selected': columns === 1 }"
                    />
                    <img
                        src="@/assets/column-2.svg"
                        @click="changeColumns(2)"
                        :class="{ 'selected': columns === 2 }"
                    />
                    <img
                        src="@/assets/column-3.svg"
                        @click="changeColumns(3)"
                        :class="{ 'selected': columns === 3 }"
                    />
                </div>
            </div>
        </header>
            <main class="content">
                <div id="content">
                    <ChatMessages :columns="columns"></ChatMessages>
                </div>
            </main>
            <footer :style="{ height: footerHeight + 'px' }">
                <textarea class="prompt-input"
                ref="textarea"
                placeholder="Type your message here..."
                @input="resizeFooter"
            ></textarea>
            <button class="send-button">{{ $t("footer.sendPrompt") }}</button>
            <div class="icons">
                <img src="assets/chatgpt-icon.png" alt="ChatGPT" />
                <img src="assets/bingchat-icon.png" alt="Bing Chat" />
                <img src="assets/wenxin-icon.png" alt="文心一言" />
                <img src="assets/bard-icon.png" alt="Bard" />
            </div>
        </footer>
    </div>
</template>

<script>
import ChatMessages from "@/components/Messages/ChatMessages.vue";

export default {
    name: "App",
    components: {
        ChatMessages
    },
    data() {
        return {
            footerHeight: 60,
            columns: 1,
        };
    },
    methods: {
        resizeFooter() {
            const lineHeight = 20; // Adjust this value according to your desired line height
            const minRows = 1;
            const maxRows = 10;

            const textarea = this.$refs.textarea;
            textarea.style.height = "auto";
            const numRows = Math.min(
                Math.max(textarea.scrollHeight / lineHeight, minRows),
                maxRows
            );
            textarea.style.height = numRows * lineHeight + "px";

            this.footerHeight = numRows * lineHeight + 40; // Adjust this value based on your desired padding and button height
        },
        changeColumns(n) {
            this.columns = n;
        },
    },
};
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: "Arial", sans-serif;
}

#app {
    display: flex;
    flex-direction: column;
    height: 100vh;
}

header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background-color: white;
    box-shadow: 0 4px 4px rgba(0, 0, 0, 0.25);
    padding: 16px;
}

.header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
  height: 40px;
}

.column-icons img{
    opacity: 0.5;
    cursor: pointer;
    width: 24px;
    height: 24px;
    margin: 4px;
}

.column-icons img.selected {
    opacity: 1;
    color: #062AAA;
}

.content {
    flex: 1;
    background-color: #f3f3f3;
    padding: 16px;
}

footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    background-color: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 8px 16px;
    gap: 8px;
    box-sizing: border-box;
}

.prompt-input {
    width: 100%;
    height: 40px;
    resize: none;
    border-radius: 4px;
    border: 1px solid #ccc;
    padding: 4px;
    box-sizing: border-box;
    outline: none;
}

.send-button {
    padding: 8px 16px;
    background-color: #062AAA;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.icons img {
    width: 32px;
    height: 32px;
    cursor: pointer;
}
</style>