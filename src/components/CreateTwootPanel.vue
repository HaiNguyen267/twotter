<template>
    <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot"
        :class="{ '--exceeded': newTwootCharacterCount > 180}">

        <label for="newTwoot">
            <strong>New twoot {{ newTwootCharacterCount }}/180</strong>
            <textarea name="" id="newTwoot" v-model="state.newTwootContent" />
        </label>

        <div class="user-profile__create-twoot-type">
            <label for="newTwootType">
                <strong>Type: </strong>
                <select name="" id="newTwootType" v-model="state.selectedTwootType">
                    <option :value="option.value" v-for="(option, index) in state.twootType" :key="index">
                        {{ option.name }}
                    </option>
                </select>
            </label>
        </div>
        <button>
            Twoot!
        </button>
    </form>
</template>

<script>
import { reactive, computed } from 'vue'

export default {
    name: "CreateTwootPanel",
    setup(props, ctx) {
        const state = reactive({
            newTwootContent: "",
            selectedTwootType: "instant",
            twootType: [
                { value: 'draft', name: 'Draft' },
                { value: 'instant', name: 'Instant' }
            ]
        })

        const newTwootCharacterCount = computed(() => state.newTwootContent.length)


        const createNewTwoot = () => {
            console.log('createNewTwoot function is working');
            console.log(state.newTwootContent);
            
            if (state.newTwootContent && state.newTwootContent.length <= 180 && state.selectedTwootType !== 'draft') {
                ctx.emit('add-twoot', state.newTwootContent)
                console.log('inner if');
                
            }

            state.newTwootContent = ""
        }
        return {
            state,
            newTwootCharacterCount,
            createNewTwoot
        };
    }
}
</script>

<style lang="scss" >
.user-profile__create-twoot {
    border-top: 1px solid black;
    margin-top: 5px;
    padding-top: 10px;


    label {
        display: flex;
        flex-direction: column;
        height: fit-content;
        margin: 10px 0;

        textarea {
            height: 100px;
        }
    }

    &.--exceeded {
        color: red;
        border-color: red;

        button {
            color: white;
            background-color: red;
        }
    }

}



button {
    width: fit-content;
    background: lightseagreen;
    color: white;
    padding: 5px 10px;
    border: none;
    transition: all 0.2s ease-in-out;
    cursor: pointer;
    border-radius: 5px;
}

button:hover {
    background: rgb(18, 122, 117);
}
</style>