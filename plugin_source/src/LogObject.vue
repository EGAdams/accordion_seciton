
<template>
    <li>
        <div class="log-object-container">
            <div>
                {{ log_object?.method }}
            </div>
            <div>
                {{ new Date( log_object?.timestamp ).toLocaleString() }}
            </div>
            <div>
                {{ log_object?.message }}
            </div>
        </div>
    </li>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import ILogObject from "./typescript_source/abstract/ILogObject";
export default defineComponent({
    name: "log_object",
    props: {
        log_object: { 
            type: Object as PropType< ILogObject >,
            default: {},
        }
    }
});
</script>

<style>
.log-object-container {
    column-gap: 15px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    padding: 0.1px;
    border: solid 0.0px;
    margin-bottom: 3px;
}
li { 
    list-style: none;
}

</style>
