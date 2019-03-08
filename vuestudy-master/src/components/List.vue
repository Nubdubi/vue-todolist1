<template>
    <div>
        <v-card 
        class="pa-3 mb-3"
        v-for="(list, index) in todoList"
        :key="index"> 
            <!-- v-card : vueatify 카드와 그림자를 만들어주는 컴포넌트
                v-for : 똑같은 형태가 여러개 반복되는것
                :key="inde" 를 넣는 이유는 여러개 반복되기 때문에 순서를 찾아주기위해서 넣어준다.
                class="pa-3" vueatify 카드의 효과중하나로 Padding All 1~5 패딩을 전방위로 1~5 숫자로 넣는다
                mb-3 margin bottomo 3.1-->
            <p> {{list.memo}} </p>
            <p> {{list.status}} </p>

            <v-btn
                v-if="list.status === 'created'"
                @click="$emit('statusControl', index, 'done')"
                 flat round color="green">완료</v-btn>
            <v-btn
            v-else
             @click="$emit('statusControl', index, 'created')"
             flat round color="blue">미완료</v-btn>
            <v-btn 
            @click="$emit('listDelete', index, 'done')"
            flat round color="red">제거</v-btn>

               <v-btn 
               @click="listEdit(list.memo, index)"
               flat round color="orange"
               v-if="list.status === 'created'"
            >수정</v-btn>

        </v-card>
    </div>
</template>

<script>
import { eventBus } from "../main"
export default {
    props: ["todoList"],
    methods: {
        listEdit(memo, index){
            eventBus.listEdit(memo, index)
//eventBus.는 listEdit 에 있는 인자를 해당부분에 내려주는 역활

        }
    }
    
}
</script>
