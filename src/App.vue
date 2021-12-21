<template>
  <div class="container">
    <div class="row justify-content-center">
        <div class="col-12 col-md-4">
            <div class="my-5">
                <Title title="Vue Todo List"></Title>

                <ListCreate @create="create"></ListCreate>

                <div class="d-flex justify-content-between">
                    <p class="mb-0 font-weight-bold">Job List{{ lists.length > 1 ? "s" : "" }}</p>
                    <p v-if="lists.length > 0 && doneTotal === lists.length" class="badge badge-success badge-pill">
                        All Done <i class="fas fa-check-circle"></i>
                    </p>
                    <p v-else class="badge badge-primary badge-pill">
                        Done {{ doneTotal }}
                    </p>
                </div>

                <ul class="list-group">
                    <li v-if="lists.length === 0" class="list-group-item text-center">
                      There is no job !
                    </li>
                    <List v-for="list in lists" :key="list.id" :list="list" @del="del"></List>
                </ul>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import List from './components/List.vue';
import ListCreate from './components/ListCreate.vue';
import Title from './components/Title.vue';
  export default {
  components: { Title, List, ListCreate },
    name : "App",
     data() {
       return {
         currentId : 0,
        
        lists : [
           
        ]
       }
     },
    computed : {
        doneTotal(){
            return this.lists.filter(el => el.isDone === true).length;
        }
    },
    methods : {
        create(x){
            this.currentId++
            this.lists.push({
                id : this.currentId,
                message : x,
                isDone : false,
                
            });
            
        },
        del(x){
          // if(confirm('Are you sure to delete ?')){
            setTimeout(()=>this.lists = this.lists.filter(el => el.id !== x ),600)
          // }
        }
    }
  }
</script>

<style>
   .done{
            text-decoration: line-through !important;
            animation: 1s shakeX;
        }
        .created{
            animation: 0.5s fadeInDown;
        }
        .deleted{
            animation: 0.5s zoomOut;
        }
</style>