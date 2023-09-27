<template>
        <div class="progress">
      <div class="progress-bar bg-info" role="progressbar" :style="{width: progress + '%' }" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{item}}/10
      </div>
    </div>
</template>

<script>
import { eventBus } from '../main';


export default{
    data(){    
        return{
            item : 0,
            progress: 0

        }
    },
    created(){
        eventBus.$on("progressBar", (productItem) => {
            this.item=productItem;
            this.progress=productItem*10;
        })
}
}

</script>