
<script>
export default {
  data() {
    return {
      arr: [],
      matter: '',
      myObj: {},
      selectTab: '',
    }
  },
  computed: {
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
      if (this.matter != '') {
        const id = this.arr.length > 0 ? this.arr[this.arr.length - 1].id : 0;
        this.myObj = {
            id: id + 1,
            matter: this.matter,
            check: false,
          };
        this.arr.push(this.myObj);
      }
      this.matter = '';
    },
    addMatter(e) {
      if (e.target.value != '') {
        this.matter = e.target.value;
        e.target.value = '';
      }
    },
    doOrNot(e, index) {
      this.arr[index].check = e.target.checked;
    },
    changeTab(string) {
      this.selectTab = string;
    },
    deleteData(index) {
      this.arr.splice(index, 1);
    },
    editData(index) {
      let userInput = prompt("請輸入事項:");
      if (userInput === null || userInput === "") {
        alert("請輸入內容！");
      } else {
        this.arr[index].matter = userInput;
        alert('成功更換事項');
      }
    },
  },
}
</script>
<template>
  <div class="w-3/5 m-auto h-full bg-gray-600">
    <div class="input-item flex justify-center mt-3 border-b-2 pb-3">
      <input type="text" class="w-1/3 pl-3 text-black" placeholder="請填寫事項(最多15字)" maxlength="15" @change="addMatter">
      <button class="ml-5 text-white hover:bg-slate-500 border p-1 rounded-xl" @click="addData()">
        新增</button>
    </div>
    <div class="flex mt-2 pb-2 border-b-2 gap-3">
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == '' }"
        @click="changeTab('')">全部</button>
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == 'true' }"
        @click="changeTab('true')">已執行</button>
      <button class="my-chooseTab-btn bg-green-300" :class="{ 'active': selectTab == 'false' }"
        @click="changeTab('false')">未執行</button>
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
            <th class="my-tbody-th"><input type="checkbox" v-model="item.check" @change="(e) => doOrNot(e, index)"
                class="w-5 h-5"></th>
            <th class="my-tbody-th">{{ item.matter }}</th>
            <th class="my-tbody-th">
              <button class="my-th-btn" @click="editData(index)">編輯</button>
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
