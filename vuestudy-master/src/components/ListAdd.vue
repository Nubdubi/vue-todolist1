<template>
    <div>
        <!-- // 1. 텍스트 필드 -->
        <!--  vuetify 에서 Textareas 에서 v-area 아웃라인하나를 복사해준다.-->
        <v-textarea
          outline
          v-model="memo" 
          label="투두리스트를 입력해주세요"
          value=""
        ></v-textarea>
        <!-- v-moel 을 사용
        label = 글자(이름표)를 설정
        value="" 아무것도 안써져있는 null 값으로 하기위해 공백 -->

        <!-- //추가버튼 만들어주기 1-->

        <v-btn v-if="mode === 'add'" @click="listAdd">리스트 추가 </v-btn>
        <v-btn v-else @click="listEdit">리스트 수정 </v-btn>
        <!-- 버튼을 만들어준다. -->

    </div>
</template>

<script>
import { eventBus } from "../main"
export default {
    data(){
        return {
        //   텍스트필드를 null 값으로 해준다.
          memo: null,
          index: null,
          mode: "add"
        } 
    },
    created(){
        eventBus.$on("listEdit",(memo, index) => {
            this.memo = memo
            this.index = index
            this.mode = "edit"
        })
        
    },

    methods : {
        listAdd(){
            if(this.memo === null){
                alert("할일을 입력해주세요. ") // memo가 입력되있지 않을경우 알림
            }else{
            this.$emit("listAdd", this.memo) // memo에 뭔가 적혀있으면 this.memo로 전달
            this.memo = null
            }
        },
         listEdit(){
           
            if(this.memo === null){
                alert("할일을 입력해주세요. ") // memo가 입력되있지 않을경우 알림
            }else{
            this.$emit("listEdit", this.memo, this.index) // memo에 뭔가 적혀있으면 this.memo로 전달
            this.memo = null
            this.mode = "add"
            }
        }
    }

}
</script>
