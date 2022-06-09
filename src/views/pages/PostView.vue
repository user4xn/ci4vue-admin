<template>
    <div class="row">
        <div class="col-lg-12">
            <div class="card">
                <div class="card-body">
                    <router-link :class="['btn btn-md btn-info mb-2 float-right font-weight-bold']" to="/create">Tambah Post</router-link>
                    <div class="card-title">
                        <h4>Management Post</h4>
                    </div>
                    <div class="table-responsive">
                        <table class="table">
                             <thead>
                                <tr>
                                    <th>TITLE</th>
                                    <th>KONTEN</th>
                                    <th>AKSI</th>
                                </tr>
                                </thead>
                                <tbody>
                                <tr v-for="(post, index) in posts" :key="post.id">
                                    <td>{{ post.title }}</td>
                                    <td>{{ post.content }}</td>
                                    <td class="text-center">
                                        <router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-sm btn-primary mr-2">EDIT</router-link>
                                        <button @click.prevent="PostDelete(post.id, index)" class="btn btn-sm btn-danger">HAPUS</button>
                                    </td>
                                </tr>
                                </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'

export default {
    
    name: 'Post',
        data() {
            return {
                posts: []
            }
        },
        created() {
            axios.get('http://localhost:8080/api/post').then(response => {
                this.posts = response.data.data;
            });
        },
        methods: {
            PostDelete(id, index)
            {
                axios.delete(`http://localhost:8080/api/post/${id}`)
                    .then(response => {
                        this.posts.splice(index, 1);
                        console.log(response);
                    }).catch(error => {
                    console.log(error.response);
                });
            }
        }
}
</script>
<style lang="">
    
</style>