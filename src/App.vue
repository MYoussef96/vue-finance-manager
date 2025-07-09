<!--
**************************************************************************************************
                                        Finance Manager

    Description: Modern Finance Manager with contemporary design
    Flow: 
    Requirements: 
    TODO: 
      - Add savings goal 
      - make it more modern ✓
**************************************************************************************************
User          Date                Branch             Changes
__________________________________________________________________________________________________
myoussef      07/04/2025          RTS0001            Initial Creation, Styling and all
myoussef      07/08/2025          RTS0001            Adding footer with savings goals and more
myoussef      07/08/2025          RTS0001            Modern redesign with glassmorphism
          
__________________________________________________________________________________________________
**************************************************************************************************
-->
<template>
  <v-app class="modern-finance-app">
    <div class="background-pattern"></div>
    <v-main>
      <v-container fluid class="pa-6">
        <!-- Header Section -->
        <div class="hero-section mb-8">
          <h1 class="hero-title">💰 Finance Manager</h1>
          <p class="hero-subtitle">Track your wealth journey with style</p>
        </div>

        <!-- Main Form Card -->
        <v-card class="main-card mb-6" elevation="0">
          <v-form @submit.prevent="handleSubmit">
            
            <!-- Savings Goals Section -->
            <div class="section-container mb-6">
              <div class="section-header">
                <v-icon class="section-icon">mdi-target</v-icon>
                <h2 class="section-title">Savings Goals</h2>
              </div>
              
              <v-row class="mt-4">
                <v-col cols="12" md="6">
                  <v-text-field
                    label="💰 Cash Savings Goal"
                    v-model="savingsGoalInput"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-currency-usd"
                    @blur="saveSavingsGoal"
                    class="modern-input"
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <v-text-field
                    label="🥇 Gold Savings Goal (grams)"
                    v-model="goldGoalInput"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-gold"
                    @blur="saveGoldGoal"
                    class="modern-input"
                  />
                </v-col>
              </v-row>
              <div class="goal-note">
                <v-icon size="small" class="mr-2">mdi-information</v-icon>
                Goals are saved locally and can be updated anytime. Stay committed!
              </div>
            </div>

            <!-- Date Section -->
            <div class="section-container mb-6">
              <div class="section-header">
                <v-icon class="section-icon">mdi-calendar</v-icon>
                <h2 class="section-title">Paycheck Date</h2>
              </div>
              <v-row class="mt-4 justify-center">
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="Select Date"
                    v-model="paycheckDate"
                    type="date"
                    variant="outlined"
                    prepend-inner-icon="mdi-calendar-today"
                    required
                    class="modern-input"
                  />
                </v-col>
              </v-row>
            </div>

            <!-- Accounts Section -->
            <div class="section-container mb-6">
              <div class="section-header">
                <v-icon class="section-icon">mdi-bank</v-icon>
                <h2 class="section-title">Account Balances</h2>
              </div>
              <v-row class="mt-4">
                <v-col cols="12" sm="6" md="3">
                  <v-text-field
                    label="💵 Cash"
                    v-model="cash"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-cash"
                    class="modern-input"
                  />
                </v-col>
                <v-col cols="12" sm="6" md="3">
                  <v-text-field
                    label="🏦 WF Checking"
                    v-model="checking"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-credit-card"
                    required
                    class="modern-input"
                  />
                </v-col>
                <v-col cols="12" sm="6" md="3">
                  <v-text-field
                    label="💰 FSCU Savings"
                    v-model="fscuSavings"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-piggy-bank"
                    class="modern-input"
                  />
                </v-col>
                <v-col cols="12" sm="6" md="3">
                  <v-text-field
                    label="🍎 Apple Savings"
                    v-model="appleSavings"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-apple"
                    class="modern-input"
                  />
                </v-col>
              </v-row>
            </div>

            <!-- Credit Debt Section -->
            <div class="section-container mb-6">
              <div class="section-header">
                <v-icon class="section-icon">mdi-credit-card-outline</v-icon>
                <h2 class="section-title">Credit Cards</h2>
              </div>
              <v-row class="mt-4">
                <v-col cols="12" lg="6">
                  <div class="credit-card-group">
                    <h3 class="card-name">🛒 Best Buy</h3>
                    <v-row dense>
                      <v-col cols="6">
                        <v-text-field
                          label="Balance"
                          v-model="bestbuy"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                      <v-col cols="6">
                        <v-text-field
                          label="Payment"
                          v-model="bestbuyPayment"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                    </v-row>
                  </div>
                </v-col>
                
                <v-col cols="12" lg="6">
                  <div class="credit-card-group">
                    <h3 class="card-name">🏦 Wells Fargo</h3>
                    <v-row dense>
                      <v-col cols="6">
                        <v-text-field
                          label="Balance"
                          v-model="wells"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                      <v-col cols="6">
                        <v-text-field
                          label="Payment"
                          v-model="wellsPayment"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                    </v-row>
                  </div>
                </v-col>

                <v-col cols="12" lg="6">
                  <div class="credit-card-group">
                    <h3 class="card-name">💳 American Express</h3>
                    <v-row dense>
                      <v-col cols="6">
                        <v-text-field
                          label="Balance"
                          v-model="amex"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                      <v-col cols="6">
                        <v-text-field
                          label="Payment"
                          v-model="amexPayment"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                    </v-row>
                  </div>
                </v-col>

                <v-col cols="12" lg="6">
                  <div class="credit-card-group">
                    <h3 class="card-name">🍎 Apple Card</h3>
                    <v-row dense>
                      <v-col cols="6">
                        <v-text-field
                          label="Balance"
                          v-model="apple"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                      <v-col cols="6">
                        <v-text-field
                          label="Payment"
                          v-model="applePayment"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                    </v-row>
                  </div>
                </v-col>

                <v-col cols="12" lg="6">
                  <div class="credit-card-group">
                    <h3 class="card-name">🏛️ Capital One</h3>
                    <v-row dense>
                      <v-col cols="6">
                        <v-text-field
                          label="Balance"
                          v-model="capitalone"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                      <v-col cols="6">
                        <v-text-field
                          label="Payment"
                          v-model="capitalonePayment"
                          type="number"
                          variant="outlined"
                          density="compact"
                          class="modern-input-compact"
                        />
                      </v-col>
                    </v-row>
                  </div>
                </v-col>
              </v-row>
            </div>

            <!-- Investments Section -->
            <div class="section-container mb-6">
              <div class="section-header">
                <v-icon class="section-icon">mdi-chart-line</v-icon>
                <h2 class="section-title">Investments</h2>
              </div>
              <v-row class="mt-4">
                <v-col cols="12" md="6">
                  <v-text-field
                    label="📈 401(k) Amount"
                    v-model="k401"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-chart-areaspline"
                    class="modern-input"
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <v-text-field
                    label="🥇 Gold (grams)"
                    v-model="gold"
                    type="number"
                    variant="outlined"
                    prepend-inner-icon="mdi-gold"
                    class="modern-input"
                  />
                </v-col>
              </v-row>
            </div>

            <!-- Submit Button -->
            <div class="text-center mb-6">
              <v-btn
                type="submit"
                size="x-large"
                class="save-button"
                elevation="8"
                rounded="xl"
              >
                <v-icon left class="mr-2">mdi-content-save</v-icon>
                Save Entry
              </v-btn>
            </div>
          </v-form>
        </v-card>

        <!-- Financial History Carousel Section -->
        <div class="history-section mb-6" v-if="entriesWithComputed.length > 0">
          <div class="section-header mb-4">
            <v-icon class="section-icon">mdi-history</v-icon>
            <h2 class="section-title">Financial History</h2>
            <div class="carousel-controls">
              <span class="entry-counter">{{ currentEntryIndex + 1 }} of {{ entriesWithComputed.length }}</span>
            </div>
          </div>
          
          <div class="swipe-carousel">
            <!-- Card Stack Container -->
            <div class="card-stack">
              <div class="cards-container">
                <div
                  v-for="(item, index) in getVisibleCards()"
                  :key="`${item.paycheckDate}-${currentEntryIndex}-${index}`"
                  class="swipe-card"
                  :class="{
                    'current': isCurrentCard(index),
                    'previous': isPreviousCard(index),
                    'next': isNextCard(index)
                  }"
                  :style="getCardStyle(index)"
                >
                  <div class="card-content">
                    <div class="entry-header">
                      <div class="entry-date">{{ item.paycheckDate }}</div>
                      <v-btn
                        v-if="isCurrentCard(index)"
                        icon
                        size="small"
                        variant="text"
                        color="error"
                        @click="deleteCurrentEntry"
                        class="delete-btn"
                      >
                        <v-icon size="small">mdi-delete</v-icon>
                      </v-btn>
                    </div>
                    
                    <!-- Main Metrics Grid -->
                    <div class="main-metrics">
                      <div class="metric-card net-worth">
                        <div class="metric-icon">💰</div>
                        <div class="metric-info">
                          <div class="metric-label">Net Worth</div>
                          <div class="metric-value" :class="{ 'positive': item.netWorthChange > 0, 'negative': item.netWorthChange < 0 }">
                            ${{ (item.netWorth ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                          <div class="metric-change" v-if="item.netWorthChange !== 0">
                            <v-icon size="small" :class="{ 'positive': item.netWorthChange > 0, 'negative': item.netWorthChange < 0 }">
                              {{ item.netWorthChange > 0 ? 'mdi-arrow-up' : 'mdi-arrow-down' }}
                            </v-icon>
                            ${{ Math.abs(item.netWorthChange ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                        </div>
                      </div>
                      
                      <div class="metric-card savings">
                        <div class="metric-icon">💵</div>
                        <div class="metric-info">
                          <div class="metric-label">Total Saved</div>
                          <div class="metric-value" :class="{ 'positive': item.totalSaved > 0, 'negative': item.totalSaved < 0 }">
                            ${{ (item.totalSaved ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                        </div>
                      </div>
                      
                      <div class="metric-card debt">
                        <div class="metric-icon">💳</div>
                        <div class="metric-info">
                          <div class="metric-label">Total Debt</div>
                          <div class="metric-value debt">
                            ${{ (item.totalDebt ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                        </div>
                      </div>
                      
                      <div class="metric-card cash-savings">
                        <div class="metric-icon">🏦</div>
                        <div class="metric-info">
                          <div class="metric-label">Cash Savings</div>
                          <div class="metric-value" :class="{ 'positive': item.cashSavingsChange > 0, 'negative': item.cashSavingsChange < 0 }">
                            ${{ (item.cashSavings ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                          <div class="metric-change" v-if="item.cashSavingsChange !== 0">
                            <v-icon size="small" :class="{ 'positive': item.cashSavingsChange > 0, 'negative': item.cashSavingsChange < 0 }">
                              {{ item.cashSavingsChange > 0 ? 'mdi-arrow-up' : 'mdi-arrow-down' }}
                            </v-icon>
                            ${{ Math.abs(item.cashSavingsChange ?? 0).toLocaleString('en-US', { minimumFractionDigits: 2 }) }}
                          </div>
                        </div>
                      </div>
                    </div>
                    
                    <!-- Detailed Breakdown -->
                    <div class="entry-details" v-if="isCurrentCard(index)">
                      <h4 class="details-title">Account Breakdown</h4>
                      <div class="details-grid">
                        <div class="detail-item">
                          <span class="detail-label">💵 Cash</span>
                          <span class="detail-value">${{ (item.cash ?? 0).toFixed(2) }}</span>
                        </div>
                        <div class="detail-item">
                          <span class="detail-label">🏦 Checking</span>
                          <span class="detail-value" :class="{ 'positive': item.checkingChange > 0, 'negative': item.checkingChange < 0 }">
                            ${{ (item.checking ?? 0).toFixed(2) }}
                          </span>
                        </div>
                        <div class="detail-item">
                          <span class="detail-label">💰 FSCU Savings</span>
                          <span class="detail-value" :class="{ 'positive': item.fscuSavingsChange > 0, 'negative': item.fscuSavingsChange < 0 }">
                            ${{ (item.fscuSavings ?? 0).toFixed(2) }}
                          </span>
                        </div>
                        <div class="detail-item">
                          <span class="detail-label">🍎 Apple Savings</span>
                          <span class="detail-value" :class="{ 'positive': item.appleSavingsChange > 0, 'negative': item.appleSavingsChange < 0 }">
                            ${{ (item.appleSavings ?? 0).toFixed(2) }}
                          </span>
                        </div>
                        <div class="detail-item">
                          <span class="detail-label">🥇 Gold</span>
                          <span class="detail-value">{{ (item.gold ?? 0).toFixed(2) }}g</span>
                        </div>
                        <div class="detail-item">
                          <span class="detail-label">📈 401k</span>
                          <span class="detail-value">${{ (item.k401 ?? 0).toFixed(2) }}</span>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Navigation Controls -->
            <div class="swipe-controls">
              <v-btn
                v-if="entriesWithComputed.length > 1"
                icon
                class="swipe-nav-btn"
                @click="swipeLeft"
                :disabled="currentEntryIndex === 0 || isTransitioning"
              >
                <v-icon>mdi-chevron-left</v-icon>
              </v-btn>
              
              <div class="swipe-indicators">
                <div
                  v-for="(item, index) in entriesWithComputed.slice().reverse()"
                  :key="index"
                  class="indicator"
                  :class="{ 'active': index === currentEntryIndex }"
                  @click="!isTransitioning && (currentEntryIndex = index)"
                ></div>
              </div>
              
              <v-btn
                v-if="entriesWithComputed.length > 1"
                icon
                class="swipe-nav-btn"
                @click="swipeRight"
                :disabled="currentEntryIndex === entriesWithComputed.length - 1 || isTransitioning"
              >
                <v-icon>mdi-chevron-right</v-icon>
              </v-btn>
            </div>
          </div>
        </div>

        <!-- Savings Goal Progress -->
        <v-card class="progress-card" elevation="0">
          <div class="section-header mb-4">
            <v-icon class="section-icon">mdi-trophy</v-icon>
            <h2 class="section-title">Goal Progress</h2>
          </div>
          
          <v-row>
            <v-col cols="12" md="6">
              <div class="progress-group">
                <h3 class="progress-title">💰 Cash Savings Goal</h3>
                <div class="progress-stats">
                  <div class="stat">
                    <span class="stat-label">Current</span>
                    <span class="stat-value">${{ latestCashSavings.toLocaleString('en-US', { minimumFractionDigits: 2 }) }}</span>
                  </div>
                  <div class="stat">
                    <span class="stat-label">Remaining</span>
                    <span class="stat-value">${{ cashGoalRemaining.toLocaleString('en-US', { minimumFractionDigits: 2 }) }}</span>
                  </div>
                  <div class="stat">
                    <span class="stat-label">Per Paycheck</span>
                    <span class="stat-value">${{ perPaycheckNeeded.toLocaleString('en-US', { minimumFractionDigits: 2 }) }}</span>
                  </div>
                </div>
                <v-progress-linear
                  :model-value="(latestCashSavings / parseFloat(savingsGoalInput || 1)) * 100"
                  height="8"
                  rounded
                  class="progress-bar"
                  color="success"
                ></v-progress-linear>
              </div>
            </v-col>
            
            <v-col cols="12" md="6">
              <div class="progress-group">
                <h3 class="progress-title">🥇 Gold Savings Goal</h3>
                <div class="progress-stats">
                  <div class="stat">
                    <span class="stat-label">Current</span>
                    <span class="stat-value">{{ latestGoldSavings.toFixed(2) }}g</span>
                  </div>
                  <div class="stat">
                    <span class="stat-label">Remaining</span>
                    <span class="stat-value">{{ goldGoalRemaining.toFixed(2) }}g</span>
                  </div>
                  <div class="stat">
                    <span class="stat-label">Per Paycheck</span>
                    <span class="stat-value">{{ goldPerPaycheckNeeded.toFixed(2) }}g</span>
                  </div>
                </div>
                <v-progress-linear
                  :model-value="(latestGoldSavings / parseFloat(goldGoalInput || 1)) * 100"
                  height="8"
                  rounded
                  class="progress-bar"
                  color="warning"
                ></v-progress-linear>
              </div>
            </v-col>
          </v-row>
          
          <div class="payday-info">
            <v-icon class="mr-2">mdi-calendar-clock</v-icon>
            <span>{{ remainingPaydays }} paychecks remaining this year</span>
          </div>
        </v-card>
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const savingsGoalInput = ref('')
const goldGoalInput = ref('')

const paycheckDate = ref('')
const cash = ref('')
const checking = ref('')
const fscuSavings = ref('')
const appleSavings = ref('')
const k401 = ref('')
const gold = ref('')

const bestbuy = ref('')
const bestbuyPayment = ref('')
const wells = ref('')
const wellsPayment = ref('')
const amex = ref('')
const amexPayment = ref('')
const apple = ref('')
const applePayment = ref('')
const capitalone = ref('')
const capitalonePayment = ref('')

// this is the array that will store all entries
const entries = ref([])

// Carousel state
const currentEntryIndex = ref(0)

// Carousel navigation functions
function swipeRight() {
  if (currentEntryIndex.value < entriesWithComputed.value.length - 1) {
    currentEntryIndex.value++
  }
}

function swipeLeft() {
  if (currentEntryIndex.value > 0) {
    currentEntryIndex.value--
  }
}

function getVisibleCards() {
  const reversedEntries = entriesWithComputed.value.slice().reverse()
  const cards = []
  
  // Always return exactly 3 cards for consistent positioning
  const prevIndex = currentEntryIndex.value - 1
  const currentIndex = currentEntryIndex.value
  const nextIndex = currentEntryIndex.value + 1
  
  // Previous card (if exists)
  if (prevIndex >= 0) {
    cards.push(reversedEntries[prevIndex])
  } else {
    cards.push(null) // placeholder
  }
  
  // Current card
  cards.push(reversedEntries[currentIndex])
  
  // Next card (if exists)
  if (nextIndex < reversedEntries.length) {
    cards.push(reversedEntries[nextIndex])
  } else {
    cards.push(null) // placeholder
  }
  
  return cards.filter(card => card !== null) // Remove null placeholders
}

function isCurrentCard(index) {
  const totalCards = getVisibleCards().length
  if (totalCards === 1) return index === 0
  if (totalCards === 2) {
    return currentEntryIndex.value === 0 ? index === 0 : index === 1
  }
  return index === 1 // Three cards - middle is current
}

function isPreviousCard(index) {
  const totalCards = getVisibleCards().length
  if (totalCards <= 1) return false
  if (totalCards === 2) {
    return currentEntryIndex.value > 0 && index === 0
  }
  return index === 0 // Three cards - first is previous
}

function isNextCard(index) {
  const totalCards = getVisibleCards().length
  if (totalCards <= 1) return false
  if (totalCards === 2) {
    return currentEntryIndex.value === 0 && index === 1
  }
  return index === 2 // Three cards - last is next
}

function getCardStyle(index) {
  const totalCards = getVisibleCards().length
  
  if (totalCards === 1) {
    // Only one card - center it
    return {
      transform: 'translateX(0%) scale(1)',
      opacity: '1',
      zIndex: 3
    }
  }
  
  if (totalCards === 2) {
    // Two cards
    if (currentEntryIndex.value === 0) {
      // First card is current, second is next
      if (index === 0) {
        return {
          transform: 'translateX(0%) scale(1)',
          opacity: '1',
          zIndex: 3
        }
      } else {
        return {
          transform: 'translateX(80%) scale(0.9)',
          opacity: '0.5',
          zIndex: 1
        }
      }
    } else {
      // First card is previous, second is current
      if (index === 0) {
        return {
          transform: 'translateX(-80%) scale(0.9)',
          opacity: '0.5',
          zIndex: 1
        }
      } else {
        return {
          transform: 'translateX(0%) scale(1)',
          opacity: '1',
          zIndex: 3
        }
      }
    }
  }
  
  // Three cards - normal carousel
  if (index === 0) { // Previous card
    return {
      transform: 'translateX(-80%) scale(0.9)',
      opacity: '0.5',
      zIndex: 1
    }
  } else if (index === 1) { // Current card
    return {
      transform: 'translateX(0%) scale(1)',
      opacity: '1',
      zIndex: 3
    }
  } else { // Next card
    return {
      transform: 'translateX(80%) scale(0.9)',
      opacity: '0.5',
      zIndex: 1
    }
  }
}

function deleteCurrentEntry() {
  const actualIndex = entriesWithComputed.value.length - 1 - currentEntryIndex.value
  deleteEntry(actualIndex)
  // Adjust current index if necessary
  if (currentEntryIndex.value >= entriesWithComputed.value.length) {
    currentEntryIndex.value = Math.max(0, entriesWithComputed.value.length - 1)
  }
}

// calculations
const entriesWithComputed = computed(() => {
  return entries.value.map((entry, index) => {
    const prev = index > 0 ? entries.value[index - 1] : null

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

    const payments =
      entry.wellsPayment +
      entry.amexPayment +
      entry.applePayment +
      entry.capitalonePayment

    const totalSpent = (totalDebt - prevDebt) + payments

    const adjustedWells = entry.wells - entry.wellsPayment
    const adjustedAmex = entry.amex - entry.amexPayment
    const adjustedApple = entry.apple - entry.applePayment
    const adjustedCapitalOne = entry.capitalone - entry.capitalonePayment
    const adjustedChecking = entry.checking - payments

    return {
      ...entry,
      goldSavings,
      cashSavings,
      netWorth,
      checkingChange: entry.checking - (prev?.checking ?? 0),
      fscuSavingsChange: entry.fscuSavings - (prev?.fscuSavings ?? 0),
      appleSavingsChange: entry.appleSavings - (prev?.appleSavings ?? 0),
      cashSavingsChange: cashSavings - ((prev?.fscuSavings ?? 0) + (prev?.appleSavings ?? 0)),
      netWorthChange: netWorth - (
        prev
          ? prev.cash + prev.checking + (prev.fscuSavings + prev.appleSavings) + (prev.gold * 107.56) + prev.k401
          : 0
      ),
      totalSaved,
      totalDebt,
      totalSpent,
      adjustedWells,
      adjustedAmex,
      adjustedApple,
      adjustedCapitalOne,
      adjustedChecking
    }
  })
})

const latestCashSavings = computed(() => {
  if (entriesWithComputed.value.length === 0) return 0
  return entriesWithComputed.value[entriesWithComputed.value.length - 1].cashSavings
})

const latestGoldSavings = computed(() => {
  if (entriesWithComputed.value.length === 0) return 0
  return entriesWithComputed.value[entriesWithComputed.value.length - 1].gold
})

const cashGoalRemaining = computed(() => {
  const goal = parseFloat(savingsGoalInput.value || 0)
  const saved = latestCashSavings.value
  return Math.max(goal - saved, 0)
})

const goldGoalRemaining = computed(() => {
  const goal = parseFloat(goldGoalInput.value || 0)
  const saved = latestGoldSavings.value
  return Math.max(goal - saved, 0)
})

// Load saved entries when app starts
onMounted(() => {
  const saved = localStorage.getItem('financeEntries')
  if (saved) {
    try {
      entries.value = JSON.parse(saved)
    } catch (e) {
      console.error('Error parsing saved entries:', e)
      entries.value = []
    }
  }

  const savedCashGoal = localStorage.getItem('savingsGoal')
  if (savedCashGoal) {
    savingsGoalInput.value = parseFloat(savedCashGoal)
  }

  const savedGoldGoal = localStorage.getItem('goldGoal')
  if (savedGoldGoal) {
    goldGoalInput.value = parseFloat(savedGoldGoal)
  }
})

function saveSavingsGoal() {
  localStorage.setItem('savingsGoal', savingsGoalInput.value)
}

function saveGoldGoal() {
  localStorage.setItem('goldGoal', goldGoalInput.value)
}

function handleSubmit(event) {
  event.preventDefault()
  saveEntry()
}

function saveEntry() {
  const newEntry = {
    paycheckDate: paycheckDate.value,
    cash: parseFloat(cash.value || 0),
    checking: parseFloat(checking.value || 0),
    fscuSavings: parseFloat(fscuSavings.value || 0),
    appleSavings: parseFloat(appleSavings.value || 0),
    k401: parseFloat(k401.value || 0),
    gold: parseFloat(gold.value || 0),

    // Bestbuy 
    bestbuy: parseFloat(bestbuy.value || 0),
    bestbuyPayment: parseFloat(bestbuyPayment.value || 0),

    // Wells 
    wells: parseFloat(wells.value || 0),
    wellsPayment: parseFloat(wellsPayment.value || 0),

    // Amex 
    amex: parseFloat(amex.value || 0),
    amexPayment: parseFloat(amexPayment.value || 0),

    // Apple 
    apple: parseFloat(apple.value || 0),
    applePayment: parseFloat(applePayment.value || 0),

    // Capital One 
    capitalone: parseFloat(capitalone.value || 0),
    capitalonePayment: parseFloat(capitalonePayment.value || 0)
  }

  entries.value.push(newEntry)
  
  try {
    localStorage.setItem('financeEntries', JSON.stringify(entries.value))
  } catch (e) {
    console.error('Error saving entries:', e)
  }

  // clear the form
  paycheckDate.value = ''
  cash.value = ''
  checking.value = ''
  fscuSavings.value = ''
  appleSavings.value = ''
  k401.value = ''
  gold.value = ''
  bestbuy.value = ''
  bestbuyPayment.value = ''
  wells.value = ''
  wellsPayment.value = ''
  amex.value = ''
  amexPayment.value = ''
  apple.value = ''
  applePayment.value = ''
  capitalone.value = ''
  capitalonePayment.value = ''
}

function deleteEntry(index) {
  entries.value.splice(index, 1)
  try {
    localStorage.setItem('financeEntries', JSON.stringify(entries.value))
  } catch (e) {
    console.error('Error saving entries after deletion:', e)
  }
}

function getRemainingPayDays() {
  const today = new Date()
  const endOfYear = new Date(today.getFullYear(), 11, 31)
  const paydays = []
  const oneDay = 24 * 60 * 60 * 1000

  // Find next thursday
  const nextThursday = new Date(today)
  nextThursday.setDate(today.getDate() + ((4 - today.getDay() + 7) % 7))

  // Adjust if this thursday is today
  if (nextThursday <= today) {
    nextThursday.setDate(nextThursday.getDate() + 7)
  }

  // Build list of every 2 week thursday
  let current = new Date(nextThursday)
  while (current <= endOfYear) {
    paydays.push(new Date(current))
    current = new Date(current.getTime() + 14 * oneDay)
  }
  return paydays
}

const remainingPaydays = computed(() => getRemainingPayDays().length)

const perPaycheckNeeded = computed(() => {
  if (remainingPaydays.value === 0) return 0
  return cashGoalRemaining.value / remainingPaydays.value
})

const goldPerPaycheckNeeded = computed(() => {
  if (!remainingPaydays.value || isNaN(remainingPaydays.value)) return 0
  return goldGoalRemaining.value / remainingPaydays.value
})
</script>

<style scoped>
/* Dark Modern Finance App Styles */
.modern-finance-app {
  min-height: 100vh;
  background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
  position: relative;
}

.background-pattern {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 25% 25%, rgba(255,255,255,0.02) 0%, transparent 50%),
    radial-gradient(circle at 75% 75%, rgba(255,255,255,0.01) 0%, transparent 50%);
  pointer-events: none;
  z-index: 0;
}

.hero-section {
  text-align: center;
  margin-bottom: 2rem;
  position: relative;
  z-index: 1;
}

.hero-title {
  font-size: 3rem;
  font-weight: 700;
  color: #e8eaf6;
  text-shadow: 0 4px 8px rgba(0,0,0,0.5);
  margin-bottom: 0.5rem;
}

.hero-subtitle {
  font-size: 1.2rem;
  color: rgba(232, 234, 246, 0.8);
  font-weight: 300;
}

.main-card {
  background: rgba(30, 30, 46, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 2rem;
  position: relative;
  z-index: 1;
}

.section-container {
  background: rgba(40, 44, 52, 0.8);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  padding: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.section-header {
  display: flex;
  align-items: center;
  margin-bottom: 1rem;
}

.section-icon {
  color: #7c4dff;
  margin-right: 0.75rem;
  font-size: 1.5rem;
}

.section-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #e8eaf6;
  margin: 0;
}

.modern-input {
  margin-bottom: 0.5rem;
}

.modern-input-compact {
  margin-bottom: 0.25rem;
}

.goal-note {
  background: rgba(124, 77, 255, 0.15);
  border-radius: 12px;
  padding: 0.75rem;
  color: #b39ddb;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  margin-top: 1rem;
}

.credit-card-group {
  background: rgba(50, 54, 62, 0.9);
  border-radius: 12px;
  padding: 1rem;
  margin-bottom: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.card-name {
  font-size: 1.1rem;
  font-weight: 600;
  color: #e8eaf6;
  margin-bottom: 0.75rem;
}

.save-button {
  background: linear-gradient(135deg, #7c4dff 0%, #536dfe 100%) !important;
  color: white !important;
  font-weight: 600;
  padding: 0 3rem;
  box-shadow: 0 8px 32px rgba(124, 77, 255, 0.3);
  transition: all 0.3s ease;
}

.save-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 40px rgba(124, 77, 255, 0.4);
}

.history-section {
  position: relative;
  z-index: 1;
}

.carousel-controls {
  margin-left: auto;
}

.entry-counter {
  background: rgba(124, 77, 255, 0.15);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  color: #b39ddb;
  font-size: 0.9rem;
  font-weight: 500;
}

.swipe-carousel {
  max-width: 900px;
  margin: 0 auto;
}

.card-stack {
  position: relative;
  height: 600px;
  margin-bottom: 2rem;
  perspective: 1000px;
}

.cards-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.swipe-card {
  position: absolute;
  top: 0;
  left: 50%;
  width: 100%;
  max-width: 600px;
  height: 100%;
  margin-left: -50%;
  background: rgba(30, 30, 46, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
  overflow: hidden;
  transition: all 0.5s cubic-bezier(0.4, 0.0, 0.2, 1);
}

.swipe-card.current {
  box-shadow: 0 25px 80px rgba(124, 77, 255, 0.3);
  border-color: rgba(124, 77, 255, 0.2);
}

.swipe-card.previous,
.swipe-card.next {
  pointer-events: none;
}

.card-content {
  padding: 2rem;
  height: 100%;
  overflow-y: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.card-content::-webkit-scrollbar {
  display: none;
}

.entry-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid rgba(124, 77, 255, 0.2);
}

.entry-date {
  font-size: 1.3rem;
  font-weight: 700;
  color: #7c4dff;
}

.main-metrics {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.metric-card {
  background: rgba(40, 44, 52, 0.8);
  border-radius: 16px;
  padding: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.08);
  transition: all 0.3s ease;
  text-align: center;
}

.metric-card:hover {
  transform: translateY(-2px);
  border-color: rgba(124, 77, 255, 0.3);
}

.metric-icon {
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.metric-info {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.metric-label {
  font-size: 0.9rem;
  color: #9e9e9e;
  margin-bottom: 0.5rem;
  font-weight: 500;
}

.metric-value {
  font-size: 1.4rem;
  font-weight: 700;
  color: #e8eaf6;
  margin-bottom: 0.25rem;
}

.metric-value.positive {
  color: #4caf50;
}

.metric-value.negative {
  color: #f44336;
}

.metric-value.debt {
  color: #ff9800;
}

.metric-change {
  font-size: 0.85rem;
  display: flex;
  align-items: center;
  gap: 0.25rem;
  opacity: 0.8;
}

.metric-change .v-icon.positive {
  color: #4caf50;
}

.metric-change .v-icon.negative {
  color: #f44336;
}

.entry-details {
  background: rgba(124, 77, 255, 0.08);
  border-radius: 16px;
  padding: 1.5rem;
}

.details-title {
  color: #e8eaf6;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 1rem;
  text-align: center;
}

.details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
}

.detail-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.75rem;
  background: rgba(50, 54, 62, 0.6);
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.detail-label {
  font-size: 0.9rem;
  color: #9e9e9e;
  font-weight: 500;
}

.detail-value {
  font-size: 0.9rem;
  font-weight: 600;
  color: #e8eaf6;
}

.detail-value.positive {
  color: #4caf50;
}

.detail-value.negative {
  color: #f44336;
}

.swipe-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-top: 1rem;
}

.swipe-nav-btn {
  background: rgba(124, 77, 255, 0.2) !important;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(124, 77, 255, 0.3);
  color: #7c4dff !important;
  width: 48px;
  height: 48px;
}

.swipe-nav-btn:hover {
  background: rgba(124, 77, 255, 0.3) !important;
  transform: scale(1.1);
}

.swipe-indicators {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(124, 77, 255, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
}

.indicator.active {
  background: #7c4dff;
  transform: scale(1.2);
}

.indicator:hover {
  background: rgba(124, 77, 255, 0.6);
}

.delete-btn {
  opacity: 0.6;
  transition: opacity 0.2s ease;
}

.delete-btn:hover {
  opacity: 1;
}

/* Card Swipe Transitions */
.card-swipe-enter-active,
.card-swipe-leave-active {
  transition: all 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.card-swipe-enter-from {
  opacity: 0;
  transform: translateX(100%) scale(0.8);
}

.card-swipe-leave-to {
  opacity: 0;
  transform: translateX(-100%) scale(0.8);
}

.entries-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 1.5rem;
  margin-top: 1rem;
}

.entry-card {
  background: rgba(30, 30, 46, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 20px;
  padding: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  transition: all 0.3s ease;
}

.entry-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4);
  border-color: rgba(124, 77, 255, 0.3);
}

.entry-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 0.75rem;
  border-bottom: 2px solid rgba(124, 77, 255, 0.2);
}

.entry-date {
  font-size: 1.1rem;
  font-weight: 600;
  color: #7c4dff;
}

.delete-btn {
  opacity: 0.6;
  transition: opacity 0.2s ease;
}

.delete-btn:hover {
  opacity: 1;
}

.entry-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 1rem;
}

.metric-group {
  text-align: center;
}

.metric-label {
  font-size: 0.85rem;
  color: #9e9e9e;
  margin-bottom: 0.25rem;
  font-weight: 500;
}

.metric-value {
  font-size: 1.2rem;
  font-weight: 700;
  color: #e8eaf6;
}

.metric-value.positive {
  color: #4caf50;
}

.metric-value.negative {
  color: #f44336;
}

.metric-value.debt {
  color: #ff9800;
}

.entry-details {
  background: rgba(124, 77, 255, 0.08);
  border-radius: 12px;
  padding: 1rem;
  font-size: 0.9rem;
}

.detail-row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  color: #b0bec5;
}

.detail-row:last-child {
  margin-bottom: 0;
}

.progress-card {
  background: rgba(30, 30, 46, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 2rem;
  position: relative;
  z-index: 1;
}

.progress-group {
  background: rgba(40, 44, 52, 0.8);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  padding: 1.5rem;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.progress-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: #e8eaf6;
  margin-bottom: 1rem;
  text-align: center;
}

.progress-stats {
  display: flex;
  justify-content: space-around;
  margin-bottom: 1rem;
}

.stat {
  text-align: center;
}

.stat-label {
  display: block;
  font-size: 0.85rem;
  color: #9e9e9e;
  margin-bottom: 0.25rem;
  font-weight: 500;
}

.stat-value {
  display: block;
  font-size: 1.1rem;
  font-weight: 700;
  color: #e8eaf6;
}

.progress-bar {
  border-radius: 8px;
  overflow: hidden;
}

.payday-info {
  background: rgba(124, 77, 255, 0.15);
  border-radius: 12px;
  padding: 1rem;
  text-align: center;
  color: #b39ddb;
  font-weight: 500;
  margin-top: 1.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .hero-subtitle {
    font-size: 1rem;
  }
  
  .main-card,
  .progress-card {
    padding: 1.5rem;
  }
  
  .section-container {
    padding: 1rem;
  }
  
  .entries-grid {
    grid-template-columns: 1fr;
  }
  
  .entry-content {
    grid-template-columns: 1fr;
    gap: 0.5rem;
  }
  
  .progress-stats {
    flex-direction: column;
    gap: 0.75rem;
  }
}

/* Custom Vuetify Dark Theme Overrides */
:deep(.v-field--variant-outlined .v-field__outline) {
  color: rgba(124, 77, 255, 0.3);
}

:deep(.v-field--variant-outlined.v-field--focused .v-field__outline) {
  color: #7c4dff;
}

:deep(.v-field--variant-outlined .v-field__input) {
  color: #e8eaf6;
}

:deep(.v-field--variant-outlined .v-field__input input) {
  color: #e8eaf6;
}

:deep(.v-field--variant-outlined .v-label) {
  color: #9e9e9e;
}

:deep(.v-field--variant-outlined.v-field--focused .v-label) {
  color: #7c4dff;
}

:deep(.v-field--variant-outlined .v-field__prepend-inner .v-icon) {
  color: #7c4dff;
}

:deep(.v-progress-linear__background) {
  background-color: rgba(124, 77, 255, 0.1) !important;
}

:deep(.v-btn--variant-elevated) {
  box-shadow: none;
}
</style>