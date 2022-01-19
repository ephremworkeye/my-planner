<template>
<form @submit.prevent="addProject">
    <label>Title:</label>
    <input type="text" required v-model="title">
    <label>Detail:</label>
    <textarea required v-model="details"></textarea>

    <button>Add Project</button>

</form>
</template>

<script>
export default {
    data() {
        return {
            title: '',
            details: ''
        }
    },
    methods:{
        addProject() {
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            }
            fetch("http://localhost:3000/projects",
                {
                    method: "POST",
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify(project)
                }).then(() => {
                    this.router.push('/')
                }).then(err => {
                    console.log(err.message)
                })
                
    
        }
    }
}
</script>

<style>
    form {
        background: white;
        padding: 20px;
        border-radius: 10px;
    }

    label {
        display: block;
        font-size: 1.15rem;
        font-weight: bold;
        margin: 20px 0 10px 0;
        text-transform: uppercase;
        color: rgb(36, 36, 36);
    }

    input {
        width: 100%;
        padding: 10px;
        border: none;
        border-bottom: 1px solid gray;
        box-sizing: border-box;

    }
    textarea {
        border: 1px solid gray;
        width: 100%;
        padding: 10px;
        box-sizing: border-box;
        height: 100px;

    }

    form button {
        display: block;
        background: green;
        border: none;
        padding: 10px 20px;
        color: white;
        margin: 20px auto 0;
        font-size: 1.2rem;
        border-radius: 20px;
    }

    form button:hover {
        background: rgb(4, 55, 4);
    }

</style>