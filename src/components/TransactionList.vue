<template>
  <h3 class="historyTitle">
    History
  </h3>

  <div class="divider"></div>

  <n-virtual-list
      style="background-color: #e8e5e5;
       max-height: 230px;"
      :items="transactions"
      :item-size="75"
  >
    <template #default="{ item }">
      <n-popconfirm :show-icon="false"
                    v-model:show="item.showPromptIcons">

        <template #action>
          <n-space>
            <n-icon class="icon" @click="deleteTransaction(item)">
              <delete48-filled/>
            </n-icon>
            <n-icon>
              <pencil-alt/>
            </n-icon>
          </n-space>
        </template>

        <template #trigger>
          <n-card
              :key="item.id"
              class="nCardWrapper"
          >

            <div class="nCard">
              <div>
                {{ item.text }}
              </div>
              <div
                  :class="getAmountClass(item.amount)"
              >
                {{ item.amount }}$
              </div>
            </div>
            <n-button type="error" style="border-radius: 10px" class="delete-btn">X</n-button>
          </n-card>
        </template>
      </n-popconfirm>
    </template>
  </n-virtual-list>


</template>

<script setup>
import {defineProps, defineEmits} from 'vue'
import {NCard, NButton, NVirtualList, NPopconfirm, NIcon, NSpace} from 'naive-ui';
import {PencilAlt} from '@vicons/fa'
import {Delete48Filled} from '@vicons/fluent'


const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  }
})

const emit = defineEmits(['transactionDeleted'])

function deleteTransaction(item) {
  item.showPromptIcons = false;
  emit('transactionDeleted', item.id)

}

function getAmountClass(amount) {
  return amount < 0 ? 'priceMinus' : 'pricePlus';
}
</script>

<style scoped>
.historyTitle {
  margin-top: 15px;
}

.divider {
  height: 1px;
  margin: 2px;
  border: 1px solid #494747;
}

.nCardWrapper {
  border-radius: 15px;
  margin-top: 7px;
  cursor: pointer;
}

.nCard {
  display: flex;
  flex-direction: row;
  justify-content: space-between;


}

.priceMinus {
  color: #c90a0a;
  font-weight: bold;
}

.pricePlus {
  color: #04a904;
  font-weight: bold;
}

.icon {
  cursor: pointer;
}


.delete-btn {
  position: absolute;
  top: 50%;
  left: 0;
  transform: translate(-110%, -50%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.nCardWrapper:hover .delete-btn {
  opacity: 1;
}
</style>