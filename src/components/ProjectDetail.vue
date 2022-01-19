<template>
    <div class="project" :class="{ complete: project.complete }">
        <div class="actions">
            <h3 @click="showDetail">{{ project.title }}</h3>
            <div class="icons">
                <span @click="deleteProject" class="material-icons">delete</span>
                <router-link :to="{ name: 'EditProject', params: {id: project.id}}">
                    <span @click="editProject" class="material-icons">edit</span>
                </router-link>
                <span @click="toggleComplete" class="material-icons tick">done</span>
            </div>
        </div>
        <div class="details" v-if="showDetails">
            <p>{{ project.details }}</p>
        </div>
    </div>
</template>
 

<script>

export default {
    props: ['project'],
    data() {
        return {
            showDetails: false,
            uri: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods: {
        showDetail() {
            this.showDetails = !this.showDetails
        },
        deleteProject() {
            fetch(this.uri, { method: "DELETE" })
                .then(() => this.$emit('delete', this.project.id))
                .catch(err => console.log(err.message))
        },
        toggleComplete() {
            fetch(this.uri, {
                method: "PATCH",
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({ complete: !this.project.complete })
            })
                .then( () => this.$emit('complete', this.project.id))
                .then(err => console.log(err.message))
        },
    },


}
</script>

<style>
.project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 2px rgba(0, 0, 0, 0.393);
    border-left: 4px solid red;
}
h3 {
    cursor: pointer;
}
.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.material-icons {
    font-size: 1.5rem;
    margin-left: 10px;
    color: rgba(0, 0, 0, 0.249);
    cursor: pointer;
}
.material-icons:hover {
    color: rgba(0, 0, 0, 0.708);
}

.project.complete {
    border-left: 4px solid green;
}
.project.complete .tick {
    color: green;
}
</style>