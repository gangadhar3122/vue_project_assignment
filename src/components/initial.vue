<template>
    <div>
        <h1>Ask a question</h1>
        <div class="mb-3">
            <input type="text" name="question" class="form-control" id="question" v-model="question" />
        </div>
        <button class="btn" v-if="question" @click="handleNext">Next</button>
        <div v-if="error">the question is short</div>

    </div>
</template>
<script>
export default {
    data() {
        return {
            question: '', error: false
        }
    },
    methods: {
        handleNext(e) {
            e.preventDefault();
            if (this.question.length <= 15) {
                this.error = true
            } else {
                this.error = false;
                this.$emit('goto',1)
                this.$emit('question',this.question)
            }
        }
    }
}


</script>
