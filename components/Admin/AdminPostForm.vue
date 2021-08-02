<template>
    <div class="register">
        <form @submit.prevent="onSave">
            <AppControlInput v-model="editedPost.author">Author Name</AppControlInput>

            <AppControlInput v-model="editedPost.title">Title</AppControlInput>
                    
            <AppControlInput v-model="editedPost.thumbnail">Thumbnail Link</AppControlInput>
                    
            <AppControlInput
                control-type="textarea"
                v-model="editedPost.previewText">Preview Text</AppControlInput>

            <AppControlInput
                control-type="textarea"
                v-model="editedPost.content">Content</AppControlInput>
                    
            <AppButton type="submit">Save</AppButton>
                    
            <AppButton
                type="button"
                style="margin-left: 10px"
                btn-style="cancel"
                @click="onCancel">Cancel</AppButton>
        </form>
    </div>
</template>

<script>
import AppControlInput from "@/components/UI/AppControlInput"
import AppButton from "@/components/UI/AppButton"
export default {
    name: "AdminPostForm",
    components:{
        AppControlInput,AppButton
    },
    props:{
        post:{
            type: Object,
            required: false
        }
    },
    data(){
        return {
            editedPost: this.post 
            ? {...this.post}: {
                author: '',
                title: '',
                previewText: '',
                thumbnail: '',
                content: ''
            }
        }
    },
    methods: {
        onSave(){
            // Save the post
            this.$emit('submit', this.editedPost);
        },
        onCancel(){
            // Navigate back
            this.$router.push('/admin');
        }
    }
}
</script>
<style scoped>

.register{
    border-radius: 40px;
    box-shadow: -3px -3px 2px rbg(225,225,255,0.3),
                5px 6px 2px rbg(0,0,0,0.2),
                15px 15px 15px rbg(0,0,0,0.2);
}