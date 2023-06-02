<template>

<div class="statusItemMain">

    <div class="statusItem" v-for="user in dataOrder" :key="user" :style="{borderLeftColor: user.FRONT_COLOR}">
        <div class="statusItem_1lvl">
            <p class="idStatus"># {{ user.OFFER_ID}}</p>
            <p class="statusItem_1lvl_date">{{ dateOrder(user.OFFER_DATE_CREATE_FRONTEND_TIMESTAMP*1000) }}</p>
            <button></button>
        </div>
        <div class="statusItem_2lvl">
            <p>{{ user.CITY_NAME ?? '' }}</p>
        </div>
        <div class="statusItem_3lvl">
            <p class="statusItem_3lvl_p_first">{{ user.OFFER_FIRST_RESPONSIBLE ?? '' }}</p>
            <p>{{ user.CONTACT_TITLE ?? '' }}</p>
            <!-- <div class="statusItem_3lvl_numberAutoAll">
                <div class="statusItem_3lvl_numberPart1">
                    <p>C062CX</p>
                </div>
                <div class="statusItem_3lvl_numberPart2">
                    <p>799</p>
                </div>
            </div> -->
        </div>
        <div class="statusItem_4lvl">
            <p> {{ user.SEGMENT_NAME }}</p>
            <p class="statusItem_4lvl_price">{{ user.OFFER_SUM ?? '' }} ₽</p>
        </div>
        
    </div>
</div>

<!-- :style="{borderLeftColor: item.FRONT_COLOR}" -->

</template>

<script>
import axios from 'axios';
import { computed } from '@vue/reactivity';
import { ref } from 'vue';

export default{

    props:['dataOrder'],

    setup(props){

        const dataOrder = ref(props.dataOrder)

        
    
    const dateOrder = (time) => computed(() => {
        const timeOrder = new Date(time)
        const options = { year: 'numeric', month: 'long', day: 'numeric' };
        return timeOrder.toLocaleDateString('en-US', options);
        })

    

        return{dataOrder, dateOrder}
    }
}

</script>

<style>

.statusItem{
    border: solid;
    border-radius: 0.5rem;
    padding: 0.5rem;
    width: 18rem;
    margin-top: 2rem;
    background-color: ghostwhite;
    border-width: 0.1rem;
    border-left-width: 0.4rem;
}

.statusItemMain{
    justify-self: center;
}

.statusItem_1lvl{
    display: flex;
    font-size: 0.9rem;
}

.idStatus{
    margin: 0rem 0.5rem;
    min-width: 5rem;
    height: 1rem;
}

.statusItem_1lvl_date{
    margin: 0rem 0.5rem;
    min-width: 7rem;
    height: 1rem;
}

.statusItem_1lvl button{
    margin-left: 2rem;
    height: 0.5rem;
    width: 2.2rem;
    padding: 0.4rem;
    background-size: cover;
    border-color: transparent;
    background-color: transparent;
    background-image: url('../assets/ellipsis.png');
}

.statusItem_2lvl{
    max-width: 10rem;
    float: right;
    font-size: 0.9rem;
}

.statusItem_2lvl p{
    margin: 0.6rem 0rem;
}

.statusItem_3lvl{
    margin-top: 3rem;
    font-size: 0.9rem;
    font-weight: bold;
}

.statusItem_3lvl p{
    margin: 0.5rem 0rem;
}

.statusItem_3lvl_p_first{
    margin-top: -1rem !important;
}

.statusItem_3lvl_numberAutoAll{
    display: flex;
}

.statusItem_3lvl_numberPart1 p{
    border: solid;
    height: 1.2rem;
    width: 3rem;
    border-width: 0.1rem;
    padding: 0rem 0.4rem;
    text-align: center;
    font-weight: bold;
    align-items: center;
    display: flex;
}

.statusItem_3lvl_numberPart2 p{
    border: solid;
    height: 1.2rem;
    width: 1.2rem;
    border-width: 0.1rem;
    padding: 0rem 0.4rem;
    text-align: center;
    font-weight: bold;
    align-items: center;
    display: flex;
}

.statusItem_4lvl{
    display: flex;
    font-size: 0.9rem;
}

.statusItem_4lvl_price{
    max-width: 7rem;
    margin-left: 12rem;
    margin-bottom: 0rem;
}

.statusItem_4lvl p{
    margin-bottom: 0rem;
}

</style>