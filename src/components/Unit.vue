<template>
   <div class="parent" :style="'top:' + (unit * 20 - 20) + 'px'" > 
       <div class="number" v-text="number + 'mL'" /><div class="line"  />
   </div>
</template>
<script>
export default {
    name: 'Unit',
    props: ['unit','number']
}
</script>
<style scoped lang="scss">
    $width: 100px;
    $height: 100px;
    .number {
        display: inline-block;
        font-size: 12px;
        position: relative;
        top:2px;
        right:3px
    }
    .line {
        display: inline-block;
        width: 30px;
        height: 2px;
        background-color: black;
    }

    .parent {
        position: absolute;
        z-index: 20;
        right: 0px;
    }

</style>