<template>
  <div>
    <div class="header">
      <p v-if="show"> {{ layrathu }},{{ thang }} {{ ngays }} {{ nam }}</p>
      <h4>{{ layrathu }}</h4>
    </div>
    <h2>Tháng {{ thang }} {{ ngays }} {{ nam }}</h2>


    <button @click="hienthithangsau"> sau</button>
    {{ layrathu }}
    <button @click="hienthithangtruoc"> trước</button>

    <table style="margin: 14px auto">
      <tr>
        <th>T2</th>
        <th>T3</th>
        <th>T4</th>
        <th>T5</th>
        <th>T6</th>
        <th>T7</th>
        <th>CN</th>
      </tr>
      <tr v-for="(tuan, indexTuan) in hienthitrong1thang" v-bind:key="indexTuan">
        <td v-for="(ngay, index) in tuan" v-bind:key="index">
          <button v-if="this.ngays === new Date().getDate()" v-on:click="show = !show" style="background-color: red; width: 100%; border:none;height: 23px ;border-radius: 50% ">
            {{ngay}}
          </button>
          <button v-else v-on:click="show = !show" style=" width: 100%; border:none;height: 23px ;border-radius: 50% " >
            {{ngay}}
          </button>
<!--          <button v-on:click="show = !show" id="doi_mau">{{ ngay }}</button>-->
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: "Lich",
  data() {
    return {
      today: new Date(),
      show: false
    }
  },
  computed: {
    //làm những cái gì tiếp theo:
    // 1: thêm những chỗ trống vào các ngày cuối vs đầu tháng sau or trước trong 1 tháng --> làm đc rồi
    // 2: thêm dấu đỏ (invalid)
    // 3: nếu ngày đầu tháng mà vào thứ 7 or cn thì nó tự nhẩy xuống thứ 2 --> fixx dược rồi
    // (nếu sửa lỗi 1 mà không bị lỗi nữa thì không phải sửa )
    // 4: click vô ngày nào thì nó hiện ra thứ ngày tháng năm của ngày đó


    hienthitrong1thang() {
      let ngayKetThucthang = this.songaytrong1thang()
      let y = this.today.getDay()
      let x = null
      let thungto = [[]]
      let mangTotal = []
      let songaygiamdan = []
      if (y === 0) {
        y = 7
      }

      if ((y - (this.ngays % 7)) > 0) {
        x = y - (this.ngays % 7)
      } else {
        x = 7 + (y - (this.ngays % 7))
      }

      for (let i = this.songaytrongthangtruocdo(); i > 0; i--) {
        songaygiamdan.push(i)
      }

      for (let i = 0; i < x; i++) {
        mangTotal.unshift(songaygiamdan[i])
      }
      for (let i = 1; i <= ngayKetThucthang; i++) {
        mangTotal.push(i)
      }
      for (let i = 1; i <= 42 - ngayKetThucthang - x; i++) {
        mangTotal.push(i)
      }
      for (let j = 0; j < mangTotal.length; j++) {
        let value = mangTotal[j]
        let thungmoi = []
        if (thungto[thungto.length - 1].length === 7) {
          thungmoi.push(value)
          thungto.push(thungmoi)
        } else {
          thungto[thungto.length-1].push(value)

        }
      }
      // console.log(thungto);


      return thungto
    },


    layrathu() {
      let thu = this.today.getDay()
      let thutrongtuan = ''

      if (thu === 0) {
        thutrongtuan = 'Chủ nhật'
      }
      if (thu === 1) {
        thutrongtuan = 'Thứ 2'
      }
      if (thu === 2) {
        thutrongtuan = 'Thứ 3'
      }
      if (thu === 3) {
        thutrongtuan = 'Thứ 4'
      }
      if (thu === 4) {
        thutrongtuan = 'Thứ 5'
      }
      if (thu === 5) {
        thutrongtuan = 'Thứ 6'
      }
      if (thu === 6) {
        thutrongtuan = 'Thứ 7'
      }
      return thutrongtuan
    },
    ngays() {
      return this.today.getDate()
    },
    thang() {
      return this.today.getMonth() + 1
    },
    nam() {
      return this.today.getFullYear()
    },
    // theky() {
    //   let theky = this.nam.toString().slice(0, 1)
    //   return parseInt(theky)
    // }
  },
  methods: {
    // tính toán ra số thứ cn = 0 , t2 =1, ...
    // tinhtoanrathu() {
    //   return ((13 * this.thang - 1) / 5 + this.nam / 4 + this.theky / 4 + this.ngays + this.nam - 2 * this.theky) % 7
    // },
    thang2namnhuan() {
      if ((this.nam % 4) || ((this.nam % 100 === 0) && (this.nam % 400))) {
        return 0
      } else {
        return 1
      }
    },
    songaytrong1thang() {
      return this.thang === 2 ? (28 + this.thang2namnhuan(this.nam)) : 31 - (this.thang - 1) % 7 % 2;
    },
    songaytrongthangtruocdo() {
      return (this.thang - 1) === 2 ? (28 + this.thang2namnhuan(this.nam)) : 31 - (this.thang - 1 - 1) % 7 % 2;
    },
    hienthithangsau() {
      this.today.setMonth(this.today.getMonth() - 1)
      this.today = new Date(this.today.toDateString())
    },
    hienthithangtruoc() {
      this.today.setMonth(this.today.getMonth() + 1)
      this.today = new Date(this.today.toDateString())
    },
  },

}
</script>

<style scoped>
/*#doi_mau {*/
/*  background-color: #fff;*/
/*  border: none;*/

/*}*/

/*#doi_mau:first-child {*/
/*  background-color: red;*/
/*}*/

</style>