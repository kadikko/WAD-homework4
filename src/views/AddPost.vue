<template>
    <div class="grid">
        <div class="sidebar"></div>
        <div class="form">
            <h3>Add a Post</h3>
            <label for="body">Body: </label>
            <input name="body" type="text" id="body" required v-model="post.body" />
            <button @click="addPost" class="addPost">Add Post</button>
        </div>
        <div class="sidebar"></div>
    </div>
</template>
  
<script>
export default {
    name: "AddPost",
    data() {
        return {
            post: {
                date: new Date(),
                body: ""
            },
        };
    },
    methods: {
        addPost() {
            var data = {
                date: this.post.date,
                body: this.post.body
            };
            // using Fetch - post method - send an HTTP post request to the specified URI with the defined body
            fetch("http://localhost:3010/api/posts", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(data),
            })
                .then((response) => {
                    console.log(response.data);
                    // redirect to /allposts view
                    this.$router.push("/api/allposts");
                })
                .catch((e) => {
                    console.log(e);
                    console.log("error");
                });
        },
    },
};
</script>


<style scoped>
.form {
    max-width: 420px;
    margin: 30px auto;
    background: rgba(255, 255, 255, 0.432);
    text-align: center;
    padding: 40px;
    border-radius: 10px;
    border: 8px solid rgba(255, 255, 255, 0.358);

}

h3 {
    text-align: center;
    color: rgb(8, 110, 110);
}

label {
    color: rgb(8, 110, 110);
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.8em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input {
    display: block;
    padding: 10px 6px 60px 10px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid white;
    border-radius: 10px;
}

button {
    border: 3px solid rgba(235, 223, 183, 0.758);
    background-color: transparent;
    margin-top: 20px;
    border: 3px solid rgba(235, 223, 183, 0.758);
    cursor: pointer;
    border-radius: 20px;
    height: 40px;
    padding-left: 20px;
    padding-right: 20px;
}
button:hover {
    background-color: rgba(231, 229, 195, 0.548);

}


.template {
    background-image: url(../assets/NSwitch_AnimalCrossingNewHorizons_bg_grass.jpg);
}

.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    gap: 2vh 8vw;
    margin: 10px auto;
}

.sidebar {
    padding: 20px;
    background-image: url(../assets/AC_wallpaper.jpg);
    background-size: 100%;
    background-repeat: round;
    border-radius: 10px;
    border: 8px solid rgba(255, 255, 255, 0.358);
}
</style>