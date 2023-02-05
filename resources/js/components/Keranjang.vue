<template>
    <div class="card-body" id="batas2">
    <h1>Keranjang Belanja 🛒</h1>
    <table class="table">
        <thead>
            <tr>
                <th>Nama Produk</th>
                <th>Qty</th>
                <th>Harga</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(item,index) in listdata" :key="index">
                <td v-if="item.status==true">{{ item.nama }}</td>
                <td v-if="item.status==true">{{ item.cart }}</td>
                <td v-if="item.status==true">Rp.{{ item.sum }}</td>
                <td v-if="item.status==true"><button-form color="red" text="Hapus" @emitClick="returnList(1,index,item.harga)"/></td>
            </tr>
        </tbody>
        <thead v-for="(item,index) in listdata2" :key="index">
            <tr>
                <th>Total:</th>
                <th></th>
                <th>Rp.{{ item.total }}</th>
            </tr>
            <br>
            <tr>
                <button-form color="green" text="Checkout" @emitClick="runPopup(item.total)"/>
            </tr>
        </thead>
    </table>
    </div>
    </template>
    
    <script>
    export default{
        props:{
            listdata:{
                type:Array,
                default:() =>{
                    return[];
                },
            },
            listdata2:{
                type:Array,
                default:() =>{
                    return[];
                },
            }
        },
        methods:{
            deleteList(a,b,c){
                this.$emit('emitDelete', a,b,c)
            },
            runPopup(a){
                this.$emit('emitPopup', a)
            },
            returnList(a,b,c){
                this.$emit('emitReturn', a,b,c)
            }
        }
    }
    </script>