<template>
    <v-container>
        <!-- {{ todoList }} -->
        <!-- todoList 가 잘돌아가는지 확인. -->
        <v-layout row wrap>
            <v-flex xs12 text-xs-center>
                
                <h1>투두 리스트</h1>
            <p>전체 할일:{{ todoList.length }} / 완료된 할일: {{ countDone }}/ 남은할일:{{ todoList.length - countDone}}</p>

            </v-flex>
            
            
               <v-flex xs12 pa-2>
                <ListAdd
                 @listAdd="listAdd"
                 @listEdit="listEdit"
                />
                <!--listAdd가 신호가 오면 listAdd 를 기입 11-->
            </v-flex>

            <v-flex xs12 pa-2>
                <List
                    :todoList="todoList" 
                    @statusControl ="statusControl"
                    @listDelete="listDelete"
                />
                <!-- todoList라는 값을 todoList로 전달해줘 -->
            </v-flex>
         
        </v-layout>

    </v-container>
</template>



<script>
import List from "./List"
// List라는 componet 에 ./List.vue 를 넣어준다
import ListAdd from "./ListAdd"
// ListAdd라는 componet 에 ./ListAdd.vue 를 넣어준다


export default {
    components: {
        List,
        ListAdd
// componet 의 이름을 기입해주는것
    },
    data() { 
        return {
        todoList:[]
// todolist에 메모가 들어가기 떄문에 빈 Array 생성
        }
    },
    computed:{
        countDone(){
            let count = 0
            this.todoList.forEach(list => {
                if (list.status === "done") count++
            })
            return count
        }
    },

    methods: {
        listAdd(memo) {
            console.log("받았다!")
            // 정확하게 받아지는지 console 확인
            this.todoList.push({memo: memo, status: "created"})
            //todo 리스트를 수정할 수있어야 하기때문에 memo를 바로 기입하는 것이아니라 memo를 기입해주는것과 생성될때의 Created를 만들어준다.
        },
        statusControl(index, status){
            this.todoList[index].status = status

        },
        listDelete(index){
            this.todoList.splice(index, 1)//splice(x, x)투두리스트의 x 번째의 수를 찾아 x개를 지워준다.

        },
        listEdit(memo, index){
            this.todoList[index].memo = memo
        }
    }
    
}
</script>
