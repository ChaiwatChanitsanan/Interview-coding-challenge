<template>
    <tbody>
        <tr @click="getDetail(no)" data-bs-toggle="modal" data-bs-target="#exampleModal">
            <td>{{no+1}}</td>
            <td>{{ name }}</td>
            <td v-text="getTime(date)"></td>
            <td v-if="pict.length != 0">
                <img :src="pict" width="100" height="100">
            </td>
            <td v-else>
                <p>ไม่มีรูปภาพประกอบ</p>
            </td>
            <td>{{ crew.length }}</td>
        </tr>
    </tbody>
</template>

<script>
export default {
    name: "TableShowLaunch",
    props: ["no","name", "date", "pict", "crew"],
    methods: {
        getTime(timestamp) {
            var date = new Date(timestamp);
            return date.toLocaleString();//date.toDateString();
        },
        getDetail(id){
           
            this.$emit("detail",id);
        }
    }
}
</script>

<style>
</style>