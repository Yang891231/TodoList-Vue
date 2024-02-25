<script setup>

</script>

<template>
  <div class="w-3/5 m-auto h-full bg-gray-600">
    <div class="input-item flex justify-center mt-3 border-b-2 pb-3">
      <input type="text" class="w-1/3 pl-3 text-black" placeholder="請填寫事項(最多15字)" maxlength="15">
      <button class="ml-5 text-white hover:bg-slate-500 border p-1 rounded-xl">新增</button>
    </div>
    <div class="all-title flex mt-2 pb-2 border-b-2 gap-3">
      <button class="ml-3 title title-bgc text-black w-20 text-center bg-green-300 focus:bg-green-700"
        data-title="all">全部</button>
      <button class="title text-black w-20 text-center bg-green-300 focus:bg-green-700" data-title="do">已執行</button>
      <button class="title text-black w-20 text-center bg-green-300 focus:bg-green-700"
        data-title="not-to-do">未執行</button>
    </div>
    <div>
      <table class="w-full pt-1 pb-2">
        <thead class="w-full justify-between border-b-2">
          <tr>
            <th class="text-white w-1/3 border-r-2">執行</th>
            <th class="text-white w-1/3 border-r-2">事項</th>
            <th class="text-white w-1/3">功能</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th class="text-white w-1/3 pt-3"><input type="checkbox" id=""></th>
            <th class="text-white w-1/3 pt-3">XXX</th>
            <th class="text-white w-1/3 pt-3">
              <button class="border p-1 hover:bg-slate-500 rounded-xl">編輯</button>
              <button class="border p-1 ml-3 hover:bg-slate-500 rounded-xl">刪除</button>
            </th>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

