<script setup>
//import...
import { ref, reactive , computed} from 'vue';


//ตัวแปร
const travelList=ref([
  { name :'The Sax Music House' , price: 1700 , img:"https://img.wongnai.com/p/1920x0/2021/01/25/d89985104ddf41f48fc2852591138e60.jpg", quantity: 0 },
  { name :'Ristr8to' , price: 1400, img:"https://scontent.fbkk8-4.fna.fbcdn.net/v/t1.15752-9/377122709_994115998539684_3112291651868365063_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHmeB_NoSDiRFXlx_TqeAaAyvRieiRBKETK9GJ6JEEoRMcyKmZHrohXWo-dbdza-6jRB4sdmd9OWu0MqH5iXgYm&_nc_ohc=rtajCFoM960AX_jE87L&_nc_ht=scontent.fbkk8-4.fna&oh=03_AdRZdSEPhjeaErraclcS7DPQE0FL96kmgfNTJEU2DOnlPw&oe=652BE18E", quantity: 0 } ,
  { name :'di BOSCO COFFEE SPECIALIST', price: 2000, img:"https://scontent.fbkk8-4.fna.fbcdn.net/v/t1.15752-9/377124405_845751270533460_2060598025526403964_n.jpg?_nc_cat=110&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeFYHRG540bGoZdhHynUrdCvE1D2kYNE2iQTUPaRg0TaJCwuNgQIQTN0Nj6MxmK1A22P6H2gkhpO0OqW4JzAvJtB&_nc_ohc=alG10MBBdmEAX927vr4&_nc_ht=scontent.fbkk8-4.fna&oh=03_AdROAzkAOj9mEoqcR4eZ8DbqvnvgA_1TLDf6LbNC-kWDDQ&oe=652BDD05", quantity: 0 } ,
  { name :'LOOPER & CO.', price: 1600 , img:"https://scontent.fbkk8-4.fna.fbcdn.net/v/t1.15752-9/377122428_688862336450689_6270943685738234442_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeEE8-BOK5NCw7_ab-ufdi4vRuKhqZ_eW-xG4qGpn95b7MHXVW8GU-Y6LQD6JtLf41gghZryDwJfbCEKOJFAuO7W&_nc_ohc=pvXBEKmysQIAX8kE7UA&_nc_ht=scontent.fbkk8-4.fna&oh=03_AdSTGZ62eAupGlnzeFkMgyIUTRQH047hQ3vLoZCpFr1jqw&oe=652BE109", quantity: 0 },
  { name :'Nine One Coffee', price: 1900 , img:"https://scontent.fbkk8-4.fna.fbcdn.net/v/t1.15752-9/377121513_854568835832443_4484750541489743961_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeEKSkApGNRlAUToJxhXYVCy2CgTlGQtVknYKBOUZC1WSQO0AKaRDypMx11ZgRJgpLvEV2zgUn-KdjIF8NYiAaMB&_nc_ohc=TSbgpLaS_QUAX_FZr4R&_nc_ht=scontent.fbkk8-4.fna&oh=03_AdTfd2hFHMSxeFkwLim8ylfc_UD5pL2X4Abqcf_KmUrD6w&oe=652BEC45", quantity: 0 },
  { name :'Sukhum Craft ', price: 1500 , img:"https://scontent.fbkk8-4.fna.fbcdn.net/v/t1.15752-9/377122712_3446093835702557_9040405550870029248_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHuQ4DZUJ5NaYCEDgmIFuRc9GXvsC7Lcyv0Ze-wLstzK0JfZJOY4OKYKtDrm752AwN6rG0hDEpfQHMvvSOn1TOu&_nc_ohc=I08xGuD3ga0AX-ZE6Be&_nc_ht=scontent.fbkk8-4.fna&oh=03_AdQ3CEZosO51vzsjzccrj0njPuNFmVIQMsqEA9DtzB8BOw&oe=652BD7D1", quantity: 0 }
  
]);

// เก็บข้อมูลการจองร้าน
const bookingList = reactive([]);



const totalAmount = computed(() => {
  return bookingList.reduce((total, item) => total + item.price, 0);
});


//function

function booking_control(name, quantity) {
  const itemindex = bookingList.findIndex(item => item.name === name);

  if (itemindex !== -1) {
    bookingList[itemindex].quantity += quantity;
    bookingList[itemindex].price = bookingList[itemindex].quantity * travelList.value.find(item => item.name === name).price;
  } else {
    const item = {
      name: name,
      quantity: quantity,
      price: quantity * travelList.value.find(item => item.name === name).price
    };
    bookingList.push(item);
  }
}

function quantity_increased(item) {
  item.quantity++;
  item.price = item.quantity * travelList.value.find(travel => travel.name === item.name).price;
}

function quantity_decreased(item) {
  if (item.quantity > 0) {
    item.quantity--;
    item.price = item.quantity * travelList.value.find(travel => travel.name === item.name).price;
  }
}

function removeItem(index) {
  bookingList.splice(index, 1);
}

//pop up

const form_costumer = ref({
  name: "",
  phone: "",
  date: "",
  time: ""
});

const showPopup = ref(false);

function togglePopup() {
  showPopup.value = !showPopup.value;
}

const isFormComplete = ref(false);

function checkFormCompletion() {
  const { name, phone, date, time } = form_costumer;
  isFormComplete.value = name !== "" && phone !== "" && date !== "" && time !== "";
}


</script>

<template>

<div class="header">
    <h1>Coffee shop booking website</h1>
</div><hr>

    <div class="container">
      <div class="row">
        <div class="col" v-for=" (i,index) in travelList" :key="index">
          <div class="card product-box shadow">
            <div class="bd-placeholder-img card-img-top" >
              <title>Placeholder</title>
              <img :src="i.img" >
            </div>
            <div class="card-body">
              <h5 class="card-title">{{ i.name }}</h5>
                <p>ราคาโต๊ะ : {{i.price}}</p>
                <h>-*-*- 5 คนต่อ 1 โต๊ะ -*-*-</h><br><br>
                <p class="card-text">จำนวนโต๊ะ <br><br>
                   <input type="number" class="value_out width_value_out" v-model="i.quantity">
                </p>
              <div class="box_btn">
                <div class="btn-group">
                  <button type="button" class="btn btn-sm btn-outline-secondary" @click="booking_control(i.name,i.quantity)">จองโต๊ะ</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

  <div class="contrainer_costumer" v-if="bookingList.length>0">
  <div class="form_box"> <h2 style="text-align: center;">กรุณากรอกข้อมูล</h2></div>
  <form>
    <div class="form_box">
      <label for="name">ชื่อ-นามสกุล </label><br>
      <input type="text" id="name" class="form-control" v-model="form_costumer.name" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="phone">เบอร์โทร </label><br>
      <input type="tel" id="phone" class="form-control" v-model="form_costumer.phone" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="date">วันที่ </label><br>
      <input type="date" id="date" class="form-control" v-model="form_costumer.date" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="time">เวลา </label><br>
      <input type="time" id="time" class="form-control" v-model="form_costumer.time" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <button type="button" class="btn btn-success" @click="togglePopup" :disabled="!isFormComplete">ยืนยันการจอง</button>
    </div>
  </form>
</div>

      <h1 style="text-align: center;" v-if="bookingList.length>0" class="head">รายการจองโต๊ะ</h1>
      <div class="List_cout">
        <table class="table table-hover" v-if="bookingList.length>0">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">ลำดับ</th>
                <th scope="col">ชื่อร้าน</th>
                <th scope="col">จำนวนโต๊ะ</th>
                <th scope="col">ราคา</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(i,index) in bookingList" :key="index" >
                <th scope="row">{{index+1}}</th>
                <td>{{ i.name }}</td>
                <td>
                    <div class="table_quantity">
                        <button type="button" class="add" @click="quantity_increased(i)" >+</button>
                        <span>{{ i.quantity }}</span>
                        <button type="button" class="cut"  @click="quantity_decreased(i)" :end="i.quantity === 0">-</button>
                    </div>
                </td>
                <td>{{ i.price }}</td>
                <td>
                    <button type="button" class="btn btn-danger" @click="removeItem(index)" >ลบ</button>
                </td>
              </tr>
            </tbody>
          </table>
        </table>
      </div>
      
    
<div v-if="showPopup" class="overlay">
  <div class="popup">
    <h2 style="text-align: center; color:green;">ยืนยันการจองสำเร็จ</h2>
    <h3>รายละเอียด</h3>
    <div class="form">
      <strong>ชื่อ-นามสกุล:</strong> {{ form_costumer.name }}
      <strong>เบอร์โทร:</strong> {{ form_costumer.phone }}
      <strong>วันที่:</strong> {{ form_costumer.date }}
      <strong>เวลา:</strong> {{ form_costumer.time }}
    </div>

    <table class="box_table">
      <thead>
        <tr>
          <th>ลำดับ</th>
          <th>ชื่อร้าน</th>
          <th>จำนวนโต๊ะ</th>
          <th>ราคา</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in bookingList" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.price }}</td>
        </tr>
      </tbody>
    </table>

    <div class="total_all">
    <strong>ยอดรวมทั้งหมด:</strong> {{ totalAmount }} บาท
    </div>

    <button class="btn btn-danger" @click="showPopup = false">ปิด</button>
  </div>
</div>



</template>
      


<style>

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');
*{
    font-family: 'Poppins', sans-serif;
    margin: 0;
    padding: 0;
    scroll-padding-top: 2rem;
    scroll-behavior: smooth;
    box-sizing: border-box;
    list-style: none;
    text-decoration: none;
}

body {
    background-image: linear-gradient(135deg,#83D1D4 1%,#878BCD 100%);
}

img{
    width: 100%;
}

.logo{
    font-size: 1.5rem;
    color: #000;
    font-weight: 500;
}

.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    margin: 20px auto;
    max-width: 1200px;
}

.card {
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}
.card-title {
    font-size: 1.2rem;
    margin: 10px 0;
}

.card-text {
    font-size: 0.9rem;
}

.value_out {
    background-image: linear-gradient(135deg,#83D1D4 1%,#878BCD 100%);
    color:black;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 10px;
    text-align: center;
    font-size: 1rem;
}

.btn-group button {
    cursor: pointer;
}

.head {
    text-align: center;
    font-size: 1.5rem;
    background-color: #fff;
    padding: 20px;
    width: 820px;
    border-radius: 10px;
}

.List_cout {
    padding: 4px;
    border: 1px solid #ccc;
    border-radius: 10px;
    background-color: #fff;
}

.table_quantity {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.add,.cut {
    width: 30px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-image: linear-gradient(135deg,#83D1D4 1%,#878BCD 100%);
    border: none;
    cursor: pointer;
    font-size: 1rem;
    border-radius: 20%;
    margin-right: 20%;
    margin-left: 20%;
}

.add:hover,.cut:hover {
    background-image: linear-gradient(135deg,#F6AEC5 10%,#f05770 100%)
}

.contrainer_costumer {
    max-width: 400px;
    margin: 20px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
}

.form_box {
    margin-bottom: 15px;
}

.form-control {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.btn-success {
    background-color: #28a745;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 1rem;
    border-radius: 5px;
}

.btn-success:hover {
    background-color: #1d8c3b;
}

.overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 100;
}

.popup {
    max-width: 750px;
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

.popup h2 {
    text-align: center;
    color: green;
    margin-bottom: 10px;
}

.popup h3 {
    margin-top: 10px;
}

.popup .form strong {
    display: block;
    margin-top: 10px;
}

.box_table {
    width: 100%;
    margin-top: 20px;
}

.popup button {
    background-color: #dc3545;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 1rem;
    border-radius: 5px;
    margin-top: 10px;
}

.popup button:hover {
    background-color: #c82333;
}

.contrainer_costumer {
    width: 380px;
    height: 100%;
    margin: 10px auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
    float: right;
}

.table {
    width: 100%;
    max-width: 800px;
}

.shop-content{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, auto));
    gap: 1.5rem;
}

.product-box{
    position: relative;
    border-radius: 10px;
}

.product-box:hover{
    padding: 10px;
    border: 1px solid #add8e6;
    transition: 0.4s;
}

.product-img{
    width: 100%;
    height: auto;
    margin-bottom: 0.5rem;
    border-radius: 10px;
}

.product-title{
    font-size: 1.1rem;
    font-weight: 600;
    text-transform: uppercase;
    margin-bottom: 0.5rem;
    margin-left: 10px;
}

.price{
    font-weight: 500;
    margin-left: 10px;
}

</style>