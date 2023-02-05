<template>
  <div class="container">
    <navbar/>
    <side/> 
    <semua-produk :listdata="list" @emitKirim="kirimList" @emitTambah="tambahList" @emitDelete="deleteList"/>
    <keranjang-produk :listdata="list" :listdata2="list2" @emitReturn="returnList" @emitPopup="runPopup" @emitDelete="deleteList"/>
  </div>
</template>
<script>
    export default({
        data(){
            return{
                list: [
                    {
                        nama: "Tas Selempang Slingbag",
                        desk: "Untuk Pembelian 10 Pcs Mendapatkan Gratis 1 Gantungan Kunci",
                        stok:17,
                        harga:10000,
                        cart:0,
                        ct:1,
                        sum:0,
                        status:false
                    },
                    {
                        nama: "Powerbank 20000 mAh",
                        desk: "Kualitas Bagus, Layak untuk dipercaya!",
                        stok:51,
                        harga:95000,
                        cart:0,
                        ct:1,
                        sum:0,
                        status:false
                    },
                    {
                        nama: "TWS Headset Bluetooth 5.0",
                        desk: "Generasi baru headset Bluetooth",
                        stok:18,
                        harga:70000,
                        cart:0,
                        ct:1,
                        sum:0,
                        status:false
                    },
                    {
                        nama: "Helm bogo dewasa Classic kaca cembung",
                        desk: "Helm Bogo Classic Original",
                        stok:9,
                        harga:55000,
                        cart:0,
                        ct:1,
                        sum:0,
                        status:false
                    },
                    {
                        nama: "Batik Pria Lengan Panjang",
                        desk: "Matt 100% full katun halus,tidak mudah kusut,jahitan rapi",
                        stok:4,
                        harga:30000,
                        cart:0,
                        ct:1,
                        sum:0,
                        status:false
                    },
                ],
                list2:[
                    {
                        total:0
                    }
                ]
            }
        },
        methods:{
            tambahList(index){
                let z = this.list[index]
                z['ct']+=1
            },
            deleteList(index){
                let z = this.list[index]
                z['ct']-=1
            },
            kirimList(a,b,c){
                let z = this.list[b]
                let y = this.list2[0]
                z['status']=true
                z['stok']-=a
                z['cart']+=a
                z['ct']=1
                z['sum']=z['sum']+(c*a)
                y['total']=y['total']+(c*a)
            },
            returnList(a,b,c){
                let z = this.list[b]
                let y = this.list2[0]
                if(z['cart']==1){
                    z['status']=false;
                };
                z['stok']+=a
                z['cart']-=a
                z['sum']=z['sum']-(c*a)
                y['total']=y['total']-(c*a)
            },
            runPopup(a){
                if(a!=0){
                if(window.confirm("Total Biaya adalah = Rp."+a+". Konfirmasi Checkout? ")){
                    window.alert("Terimakasih sudah checkout 🤑");
                    location.reload();
                }
                else
                {
                    window.alert("Anda membatalkan Checkout 😭");
                };
                };
                if(a==0){
                    window.alert("Keranjang belanja masih kosong!");
                }
            }
        }
    })
</script>