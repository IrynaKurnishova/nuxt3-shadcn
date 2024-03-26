<template>
  <div class="grid w-full gap-4">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>Hi, welcome back, Iryna!</p>
        <h1>Dashboard</h1>
      </div>
      <div class="w-[120px] bg-neutral-200 h-[36px]"></div>
    </header>

    <main class="grid w-full gap-4">
        <Tabs default-value="Today"  class="w-full" @click="setCategory">
          <TabsList class="max-w-[400px]">
            <TabsTrigger v-for="(item, index) in list" :key="index" :value="item.title">
              {{item.title}}
            </TabsTrigger>
          </TabsList>
          <TabsContent class="w-[100%]" v-for="(item, index) in list" :key="index" :value="item.title">
            <component :is="item.component"/>
            <highchart v-if="data.length > 0" :options="options"/>
          </TabsContent>
        </Tabs>
    </main>

    <footer>
      <div class="flex items-center gap-4">
        <div
            v-for="(item, index) in 3"
            :key="index"
            class="w-full h-[260px] bg-neutral-200"
        ></div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
import {resolveComponent} from "vue";

const list = [
  {
    title: "Today",
    component: resolveComponent("TabsToday")
  },
  {
    title: "Week",
    component: resolveComponent("TabsWeek")
  },
  {
    title: "Month",
    component: resolveComponent("TabsMonth")
  },
  {
    title: "Year",
    component: resolveComponent("TabsYear")
  },
]

let data = ref([])

let categories = ref({
  today : ['00:00', '01:00', '02:00', '03:00', '04:00', '05:00', '06:00',
    '07:00', '08:00', '09:00', '10:00', '11:00', '12:00', '13:00',
    '14:00', '15:00', '16:00', '17:00', '18:00', '19:00', '20:00',
    '21:00', '22:00', '23:00'
  ]
  ,
  week : ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
  year : ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
})
let currentCategory = ref('today')

const options = computed(() => (
    {
      chart: {
        type: 'line',
        animation: {
          enabled: false
        }
      },
      legend: {
        enabled: false
      },
      title: {
        text: ''
      },
      xAxis: {
        gridLineColor: 'transparent',
        categories: categories.value[currentCategory.value]
      },
      yAxis: {
        gridLineColor: 'transparent',
        title: {
          text: ''
        }
      },
      plotOptions: {
        line: {
          marker: {
            enabled: false
          },
          dataLabels: {
            enabled: false
          },
          enableMouseTracking: false
        }
      },
      series: [{
        name: 'line',
        lineWidth: '4px',
        color: {
          linearGradient: {},
          stops: [
              [0, 'rgba(252, 176, 69, 1)'],
              [0.33, 'rgba(253, 29, 29, 1)'],
              [0.66, 'rgba(131, 58, 180, 1)'],
              [1, 'rgba(29, 217, 83, 1)']
          ]
        },
        data: data.value
      }]
    }
))

function generateMonth() {
  let currentDate = new Date();
  let currenMonth = currentDate.getMonth() + 1;
  let currentYear = currentDate.getFullYear()

  function  generateMonthDates() {
    let monthDates = []
    let daysInMonth = new Date(currentYear, currenMonth, 0).getDate();

    for (let i = 1; i <= daysInMonth; i++) {
      let dayString = ("0" + i).slice(-2)
      let monthString = ("0" + currenMonth).slice(-2)
      monthDates.push(monthString + "/" + dayString)
    }
    return monthDates
  }

  let month = generateMonthDates()
  categories.value = ({...categories.value, month})
  return month;
}

function generateRandomData(number = 23) {
  let values = []
  for (let i = 0; i < number + 1; i++) {
    values.push(Math.floor(Math.random() * 100));
  }
  data.value = values;
  return values
}

const setCategory = (e) => {
  let v = e.target.innerText.toLowerCase()
  currentCategory.value = v
  switch (v) {
    case 'today':
      generateRandomData(23);
      break;
    case 'week':
      generateRandomData(6);
      break;
    case 'month':
      generateRandomData(30);
      break;
    case 'year':
      generateRandomData(11);
      break;
  }
}

onMounted(() => {
  generateMonth()
  generateRandomData(23)
})
</script>
