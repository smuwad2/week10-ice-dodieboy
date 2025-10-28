<script>
    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        props: {
            mood: String,
            entry: String,
            subject: String
        }
    }
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card --> 
    <div class="card">
        <img src="../../../public/assets/angry.png" v-if="mood == 'Angry'" width="250px" class="mx-auto"></img>
        <img src="../../../public/assets/happy.png" v-if="mood == 'Happy'" width="250px" class="mx-auto"></img>
        <img src="../../../public/assets/sad.png" v-if="mood == 'Sad'" width="250px" class="mx-auto"></img>
        <h2>{{ subject }}</h2>
        <p>{{ entry }}</p>
    </div>
</template>

