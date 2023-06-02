<template>
<div>
    <div class="statusList">
        <div v-for="item in dataStatus" :key="dataStatus" class="statusListItem">
            <div>
                <h4> {{ item.TITLE }} </h4>
                <p>{{ orders(item.TITLE).value.length }} {{ orders(item.TITLE).value.length %2 ? "Сделка" : "Сделок"}}</p>
                <button class="hiddenOn" v-if="item.TO_HIDE === 'Y'"></button>
            </div>
            <statusItem
            :dataOrder = orders(item.TITLE)
            ></statusItem>
        </div>
    </div>
</div>

</template>

<script>
import statusItem from './statusItem.vue';
import axios from 'axios'
import { ref } from 'vue';
import { computed } from '@vue/reactivity';

export default{

    setup(){

        const dataStatus = ref()
        const statusAllList = ref()

        const getStatusItems = async () =>{
            const {data} = await axios.get(`https://nastintesthodl.stocrm.ru/api/external/v1/offers/get_from_filter?SID=10813_0c0a9a2f86eab09196705a274378b64a&FILTER[BOARD_ID]=1843(ASC/DESC)&PAGE=1&LIMIT=99999&REQUIRED_FIELDS[0]=Поле_1`)
            statusAllList.value = data.RESPONSE.DATA

        }

        getStatusItems()
        


        const getDataStatus = async () =>{
            const {data} = await axios.get('https://nastintesthodl.stocrm.ru/api/external/v1/offer/all_statuses?SID=10813_0c0a9a2f86eab09196705a274378b64a&BOARD_ID=1843')
            dataStatus.value = data.RESPONSE
        }

        getDataStatus()


        const orders = (status) => 
        computed(() => {return statusAllList.value.filter(statusItem => statusItem.STATUS_NAME === status) })

        return{dataStatus, statusAllList, orders}
    },
    components:{statusItem}
}

</script>

<style scoped>

.statusList{
    display: flex;
    width: -webkit-fill-available;
    overflow-x: scroll;
}


.statusListItem{
    min-width: 20rem;
    margin-bottom: 1rem;
    display: grid;
    align-items: center;
    height: -webkit-fill-available;
    margin-top: 2rem;
}

.hiddenOn{
    position: initial;
    float: right;
    width: 2rem;
    height: 2rem;
    margin-top: -2.5rem;
    border-color: transparent;
    background-color: transparent;
    justify-self: right;
    background-size: cover;
    background-image: url('../assets/hidden.png');
}

.statusListItem h4{
    width: 11rem;
    height: 1rem;
    margin: 0.5rem 0rem;
    margin-left: 1rem;
    margin-top: 1rem;
    font-size: 0.9rem;
    font-family: monospace;
}

.statusListItem p {
    margin: 0rem;
    font-size: 0.9rem;
    margin-left: 1rem;
}

</style>