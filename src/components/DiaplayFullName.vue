<template>
    <div>
        display : 
        {{name + '     ' + lastname}}
    </div>
</template>


<script>
export default {
    props:['name', 'lastname']
}
</script>