<!--
**************************************************************************************************
                                        Finance Manager

    Description: 
    Flow: 
    Requirements: 
**************************************************************************************************
User          Date                Branch             Changes
__________________________________________________________________________________________________
myoussef      07/04/2025          RTS0001            Initial Creation 
__________________________________________________________________________________________________
**************************************************************************************************
-->
<template>
  <v-app>
    <v-main>
      <v-container>
        <h1 class="text-h4 mb-4">My Finance Manager</h1>
        <v-form @submit.prevent="saveEntry">
          <!-- Date Section -->
          <v-row>
            <v-col cols="12" class="text-center">
              <v-text-field label="Paycheck Date" v-model="paycheckDate" type="date" required
                style="max-width: 300px; margin: auto;" />
            </v-col>
          </v-row>
          <v-divider class="my-4"></v-divider>

          <!-- ACCOUNTS SECTION -->
          <h2 class="text-h6 mb-2">Accounts</h2>
          <v-row dense>
            <v-col cols="12" sm="6">
              <v-text-field label="Cash Amount ($)" v-model="cash" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="WF Checking ($)" v-model="checking" type="number" required />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="FSCU Savings ($)" v-model="fscuSavings" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Apple Savings ($)" v-model="appleSavings" type="number" />
            </v-col>
          </v-row>
          <v-divider class="my-4"></v-divider>

          <!-- CREDIT DEBT SECTION -->
          <h2 class="text-h6 mb-2">Credit Debt</h2>
          <v-row dense>
            <v-col cols="12" sm="6">
              <v-text-field label="Best Buy Credit Card ($)" v-model="bestbuy" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Wells Credit Card ($)" v-model="wells" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Amex Credit Card ($)" v-model="amex" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Apple Credit Card ($)" v-model="apple" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Capital One Credit Card ($)" v-model="capitalone" type="number" />
            </v-col>
          </v-row>

          <v-divider class="my-4"></v-divider>

          <!-- INVESTMENTS SECTION -->
          <h2 class="text-h6 mb-2">Investments</h2>
          <v-row dense>
            <v-col cols="12" sm="6">
              <v-text-field label="401(k) Amount ($)" v-model="k401" type="number" />
            </v-col>
            <v-col cols="12" sm="6">
              <v-text-field label="Gold (grams)" v-model="gold" type="number" />
            </v-col>
          </v-row>

          <v-btn type="submit" color="primary" class="mt-4">
            Save Entry
          </v-btn>

          <v-data-table
            class="mt-6"
            :headers="headers"
            :items="entriesWithComputed"
          >
            <template v-slot:item.cash="{ item }">
              {{ (item.cash ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.checking="{ item }">
              {{ (item.checking ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.fscuSavings="{ item }">
              {{ (item.fscuSavings ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.appleSavings="{ item }">
              {{ (item.appleSavings ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.cashSavings="{ item }">
              {{ (item.cashSavings ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.netWorth="{ item }">
              {{ (item.netWorth ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.totalSaved="{ item }">
              {{ (item.totalSaved ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.bestbuy="{ item }">
              {{ (item.bestbuy ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.wells="{ item }">
              {{ (item.wells ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.amex="{ item }">
              {{ (item.amex ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.apple="{ item }">
              {{ (item.apple ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.capitalone="{ item }">
              {{ (item.capitalone ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.totalSpent="{ item }">
              {{ (item.totalSpent ?? 0).toFixed(2) }}
            </template>
            <template v-slot:item.totalDebt="{ item }">
              {{ (item.totalDebt ?? 0).toFixed(2) }}
            </template>
          </v-data-table>


        </v-form>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const paycheckDate = ref('')
const cash = ref('')
const checking = ref('')
const fscuSavings = ref('')
const appleSavings = ref('')
const k401 = ref('')
const gold = ref('')

const bestbuy = ref('')
const wells = ref('')
const amex = ref('')
const apple = ref('')
const capitalone = ref('')


// this is the array that will store all entries
const entries = ref([])

// defining headers
const headers = [
  { title: 'Date', key: 'paycheckDate' },
  { title: 'Cash ($)', key: 'cash' },
  { title: 'Checking ($)', key: 'checking' },
  { title: 'FSCU Savings ($)', key: 'fscuSavings' },
  { title: 'Apple Savings ($)', key: 'appleSavings' },
  { title: 'Cash Savings ($)', key: 'cashSavings' },
  { title: 'Net Worth ($)', key: 'netWorth' },
  { title: 'Total Saved ($)', key: 'totalSaved' },
  { title: 'Best Buy ($)', key: 'bestbuy' },
  { title: 'Wells ($)', key: 'wells' },
  { title: 'Amex ($)', key: 'amex' },
  { title: 'Apple ($)', key: 'apple' },
  { title: 'Capital One ($)', key: 'capitalone' },
  { title: 'Total Spent ($)', key: 'totalSpent' },
  { title: 'Total Debt ($)', key: 'totalDebt' }
]

// calculations
const entriesWithComputed = computed(() => {
  return entries.value.map((entry, index) => {
    const goldSavings = entry.gold * 107.56
    const cashSavings = entry.fscuSavings + entry.appleSavings

    const netWorth =
      entry.cash +
      entry.checking +
      cashSavings +
      goldSavings +
      entry.k401

    // Previous row Net Worth for Total Saved
    let prevCashSavings = 0
    if (index > 0) {
      const prev = entries.value[index - 1]
      prevCashSavings = prev.fscuSavings + prev.appleSavings
    }
    const totalSaved = cashSavings - prevCashSavings

    // Total Debt = Wells + Amex + Apple + Capital One
    const totalDebt =
      entry.wells +
      entry.amex +
      entry.apple +
      entry.capitalone

    // Previous Debt to calculate Total Spent
    let prevDebt = 0
    if (index > 0) {
      const prev = entries.value[index - 1]
      prevDebt =
        prev.wells +
        prev.amex +
        prev.apple +
        prev.capitalone
    }
    const totalSpent = totalDebt - prevDebt

    return {
      ...entry,
      goldSavings,
      cashSavings,
      netWorth,
      totalSaved,
      totalDebt,
      totalSpent
    }
  })
})
// Load saved entries when app starts
onMounted(() => {
  const saved = localStorage.getItem('financeEntries')
  if (saved) {
    entries.value = JSON.parse(saved)
  }
})

function saveEntry() {
  const newEntry = {
    paycheckDate: paycheckDate.value,
    cash: parseFloat(cash.value || 0),
    checking: parseFloat(checking.value || 0),
    fscuSavings: parseFloat(fscuSavings.value || 0),
    appleSavings: parseFloat(appleSavings.value || 0),
    k401: parseFloat(k401.value || 0),
    gold: parseFloat(gold.value || 0),
    bestbuy: parseFloat(bestbuy.value || 0),
    wells: parseFloat(wells.value || 0),
    amex: parseFloat(amex.value || 0),
    apple: parseFloat(apple.value || 0),
    capitalone: parseFloat(capitalone.value || 0)
  }

  entries.value.push(newEntry)
  localStorage.setItem('financeEntries', JSON.stringify(entries.value))

  // clear the form
  paycheckDate.value = ''
  cash.value = ''
  checking.value = ''
  fscuSavings.value = ''
  appleSavings.value = ''
  k401.value = ''
  gold.value = ''
  bestbuy.value = ''
  wells.value = ''
  amex.value = ''
  apple.value = ''
  capitalone.value = ''
}

</script>

<style scoped>
/* add styling later here */
</style>