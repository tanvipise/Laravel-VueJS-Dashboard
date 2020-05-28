<template>
    <div class="container">
        <div class="row mt-5">
          <div class="col-md-12">
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">User Table</h3>

                <div class="card-tools">
                  <button class="btn btn-success" data-toggle="modal" data-target="#addNew">Add new user   <i class="fas fa-user-plus fa-fw"></i> </button>
                </div>
              </div>
              <!-- /.card-header -->
              <div class="card-body table-responsive p-0">
                <table class="table table-hover text-nowrap">
                  <thead>
                    <tr>
                      <th>ID</th>
                      <th>User</th>
                      <th>Email</th>
                      <th>Registered at</th>
                      <th>Type</th>
                      <th>Edit</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="user in users" :key="user.id">
                    
                      <td>{{user.id}}</td>
                      <td>{{user.name}}</td>
                      <td>{{user.email}} </td>
                      <td>{{user.created_at | myDate}} </td>
                      <td><span class="tag tag-success">Approved</span></td>
                      <td>
                          <a href="#"> </a>
                          <i class="fa fa-edit"></i>
                            /
                            <a href="#"> </a>
                          <i class="fa fa-trash"></i>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="addNewLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                   <div class="modal-header">
                      <h5 class="modal-title" id="addNewLabel">Add New User </h5>
                      <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                      <span aria-hidden="true">&times;</span>
                    </button>
      </div>
        <form @submit.prevent="create">
            
      <div class="modal-body">
          
        <div class="form-group">
            <input v-model="form.name" type="text" name="name" placeholder="Enter name"
                 class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
            <has-error :form="form" field="name"></has-error>
        </div>

        <div class="form-group">
            <input v-model="form.email" type="email" name="email" placeholder="Enter email"
                 class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
            <has-error :form="form" field="email"></has-error>
        </div>

        <div class="form-group">
            <input v-model="form.password" type="password" name="password" placeholder="Enter password"
                 class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
            <has-error :form="form" field="password"></has-error>
        </div>
      </div>
        
      <div class="modal-footer">
        <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
        <button type="submit" class="btn btn-primary">Add</button>
      </div>
    </form>
    </div>
  </div>
</div>
    </div>
</template>

<script>
import Form from 'vform'; 
    export default {
        data () {
             return {
                users: {},   
                form: new Form({
                    name: '',
                    email:'',
                    email_verified_at:'',
                    password: ''
      })
    }
  },
  methods: {
   loadUsers(){
     axios.get("/api/user").then(({data}) => (this.users=data)).catch((err)=>console.log(err));         
   },

    create(){
         this.form.post('api/user');
    }
  },
  created(){
      this.loadUsers();
  },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
