
<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 col-md-offset-2">
                <div class="panel panel-default">
                    <div class="panel-heading">Create Notebook</div>

                    <div class="panel-body">
                        <form @submit.prevent="addNotebooks()">
                            <div class="form-group">
                                <label for="name">Name</label>
                                <input type="text" class="form-control" id="" placeholder="Name" v-model="notebookData.name">
                                <span class="text-danger">{{errors.name?errors.name[0]:""}}</span>
                            </div>
                            <div class="form-group">
                                <label for="name">Body</label>
                                <input type="text" class="form-control" id="" placeholder="Description" v-model="notebookData.body">
                                <span class="text-danger">{{errors.body?errors.body[0]:""}}</span>
                            </div>
                            <button type="submit" class="btn btn-primary">Submit</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                notebookData: {
                    name: '',
                    body: ''
                },
                errors: {}
            }
        },
        methods:{
            addNotebooks(){
                axios.post('/notebook', this.notebookData)
                .then(response=>{
                    //console.log('response');
                    this.notebookData = "";
                    this.errors = "";
                    this.$router.push('/');
                })
                .catch(error=>{
                    //console.log(error.response);
                    this.errors=error.response.data
                });
            }
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
