
<script>
export default {
  data() {
    return {
      arr: [],
      matter: '',
      myObj: {},
      selectTab: '',
      editText:'',
    }
  },
  mounted(){
    // 網頁開啟後先執行裡面JS
    // 把資料從localStorage特定key值拿出來資料丟進msgArr裡面
    // 清空資料
    // localStorage.removeItem('msg');
    if (localStorage.getItem('msg')) {
      this.arr = JSON.parse(localStorage.getItem('msg'));
    };
  },
  // 預處理拿到的資料,有暫存功能可將整個資料拿出來並利用判斷式將資料篩選
  computed: {
    // 將陣列置換分頁內容對應陣列
    filterUseData() {
      if (!this.selectTab) {
        return this.arr;
      }
      return this.arr.filter(user => String(user.check) === this.selectTab);
    },
  },
  methods: {
    // 新增資料
    addData() {
      if (this.matter.trim() != '') {
        const id = this.arr.length > 0 ? this.arr[this.arr.length - 1].id : 0;
        this.myObj = {
            id: id + 1,
            matter: this.matter,
            check: false,
            editSwitch:false,
          };
        this.arr.push(this.myObj);
      }
      this.matter = '';
      localStorage.setItem('msg' , JSON.stringify(this.arr));
    },
    // 查看checkBox是否被按下
    // doOrNot(e, index) {
    //   this.arr[index].check = e.target.checked;
    //   localStorage.setItem('msg' , JSON.stringify(this.arr));
    // },
    // 刪除陣列元素
    deleteData(index) {
      this.arr.splice(index, 1);
      localStorage.setItem('msg' , JSON.stringify(this.arr));
    },
    // 置換編輯文字與陣列文字
    editData(item) {
      item.editSwitch = !item.editSwitch;
      if (item.editSwitch == false) {
        item.matter = this.editText;
      }
      else{
        this.editText = item.matter;
      };
      localStorage.setItem('msg' , JSON.stringify(this.arr));
    },
    // 讀取編輯文字
    editMsg(e){
      this.editText = e.target.value;
    },
    changeCheckBox(){
      localStorage.setItem('msg' , JSON.stringify(this.arr));
    }
  },
}
</script>
<template>
  <div class="w-3/5 m-auto h-full bg-gray-600 overflow-y-auto">
    <div class="input-item flex justify-center mt-3 border-b-2 pb-3">
      <input type="text" class="w-1/3 pl-3 text-black" placeholder="請填寫事項(最多15字)" maxlength="15" v-model="matter">
      <button class="ml-5 text-white hover:bg-slate-500 border p-1 rounded-xl" @click="addData()">
        新增</button>
    </div>
    <div class="flex mt-2 pb-2 border-b-2 gap-3">
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == '' }"
        @click="() => selectTab = ''">全部</button>
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == 'true' }"
        @click="() => selectTab = 'true'">已執行</button>
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == 'false' }"
        @click="() => selectTab = 'false'">未執行</button>
    </div>
    <div>
      <table class="w-full pt-1 pb-2">
        <thead class="w-full justify-between border-b-2">
          <tr>
            <th class="my-thead-th">執行</th>
            <th class="my-thead-th">事項</th>
            <th class="my-thead-th">功能</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in filterUseData" :key="item.id">
            <th class="my-tbody-th"><input type="checkbox" v-model="item.check" class="w-5 h-5" @change="changeCheckBox()"></th>
            <th class="my-tbody-th" v-if="item.editSwitch == false">{{ item.matter }}</th>
            <th class="my-tbody-th" v-else><input type="text" class="text-black" @change="editMsg"></th>
            <th class="my-tbody-th">
              <button class="my-th-btn" @click="editData(item)">編輯</button>
              <button class="my-th-btn ml-3" @click="deleteData(index)">刪除</button>
            </th>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.active {
  @apply bg-white text-black;
}

.my-thead-th {
  @apply text-white w-1/3 border;
}

.my-tbody-th {
  @apply text-white w-1/3 pt-3;
}

.my-th-btn {
  @apply border p-1 hover:bg-slate-500 rounded-xl;
}

.my-chooseTab-btn {
  @apply text-black w-20 text-center;
}
</style>
