<template>
  <div>
      <layout-main>
          <div class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom">
            <h1 class="h2">Users</h1>
                <router-link :to="{name : 'createuser'}"
                 class="btn btn-succes">Create New User
                </router-link>
          </div>
          <div class="row row-cols-1 row-cols-md-4 row-cols-sm-2">
            <div v-for="user in datausers" :key="user.id" class="col card">
                <img src="profilepicture.jpg" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{user.name}}</h5>
                        <h6>{{user.username}}</h6>
                        <p class="card-text">
                            Company : {{user.company.name}}
                        </p>
                            
                        <router-link :to="{name : 'detailuser', params: {id: user.id, username: user.username}}"
                         class="btn btn-primary">Detail User
                         </router-link>
                    </div>
            </div>
          </div>
      </layout-main>
  </div>
</template>

<script>
import LayoutMain from "@/views/LayoutMain"

export default {
    components : {
        LayoutMain
    },
    data(){
        return{
            datausers: null,
            data2 : null,
            data3: ""
        }
    },
    methods: {
        //Fungsi, bisa lebih dari 1 
        getUsers(){
            fetch("https://jsonplaceholder.typicode.com/users")
                .then(response => response.json()) //then 1 untuk set respon sebagai json
                .then(json => {
                    this.datausers = json;
                }) //then2 mengambil json dan di tmpung k dlm data
                .catch(error => {
                    console.log(error);
                })
        }
    },
    
    //Untuk memanggil fungsi
    mounted(){
        console.log("Halo");
        this.getUsers();
    }
}
</script>