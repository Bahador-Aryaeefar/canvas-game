<script setup>
import { computed } from '@vue/reactivity';
import { onMounted, ref } from 'vue';

const deg = ref(0)
const canvas = ref(null)

onMounted(() =>
{
  canvas.value.width = document.body.clientWidth;
  canvas.value.height = document.body.clientHeight;
})

let x = 0
let y = 0
let points = []
let allow = true
const top = ref(500)
const left = ref(500)
const arrowX = ref(500)
const arrowY = ref(500)
const arrowDeg = ref(Math.atan(1) * 180 / Math.PI)
const massage = ref(true)

const enemy1 = ref(null)
const enemy2 = ref(null)
const enemy3 = ref(null)
const enemy4 = ref(null)
const isAlive1 = ref(true)
const isAlive2 = ref(true)
const isAlive3 = ref(true)
const isAlive4 = ref(true)
let level = ref(1)
const speed = computed(() =>
{
  switch (level.value)
  {
    case 1:
      return 1500
    case 2:
      return 1000
    case 3:
      return 500
    case 4:
      return 250
    default:
      return 250
  }
})

const rotSpeed = computed(() =>
{
  switch (level.value)
  {
    case 1:
      return 60
    case 2:
      return 20
    case 3:
      return 7
    case 4:
      return 2
    default:
      return 2
  }
})

const user = ref({ value: 1 })
const enemy = ref({ value: 1 })
const line = ref({ value: 1 })

const pos1 = ref([100, 100])
const pos2 = ref([150, 100])
const pos3 = ref([200, 100])
const pos4 = ref([250, 100])

let enemyMove = setInterval(() =>
{
  pos1.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos1.value[0] < 0) pos1.value[0] = 0
  if (pos1.value[0] > document.body.clientWidth) pos1.value[0] = document.body.clientWidth - 50
  pos1.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos1.value[1] < 0) pos1.value[1] = 0
  if (pos1.value[1] > document.body.clientHeight) pos1.value[1] = document.body.clientHeight - 50

  pos2.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos2.value[0] < 0) pos2.value[0] = 0
  if (pos2.value[0] > document.body.clientWidth) pos2.value[0] = document.body.clientWidth - 50
  pos2.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos2.value[1] < 0) pos2.value[1] = 0
  if (pos2.value[1] > document.body.clientHeight) pos2.value[1] = document.body.clientHeight - 50

  pos3.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos3.value[0] < 0) pos3.value[0] = 0
  if (pos3.value[0] > document.body.clientWidth) pos3.value[0] = document.body.clientWidth - 50
  pos3.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos3.value[1] < 0) pos3.value[1] = 0
  if (pos3.value[1] > document.body.clientHeight) pos3.value[1] = document.body.clientHeight - 50

  pos4.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos4.value[0] < 0) pos4.value[0] = 0
  if (pos4.value[0] > document.body.clientWidth) pos4.value[0] = document.body.clientWidth - 50
  pos4.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
  if (pos4.value[1] < 0) pos4.value[1] = 0
  if (pos4.value[1] > document.body.clientHeight) pos4.value[1] = document.body.clientHeight - 50
}, speed.value)

let rotating = setInterval(function ()
{
  if (deg.value == 360) deg.value = 1
  else deg.value += 1
}, rotSpeed.value)

function incLevel()
{
  if (isAlive1.value || isAlive2.value || isAlive3.value || isAlive4.value) return
  level.value++
  clearInterval(enemyMove)
  enemyMove = setInterval(() =>
  {
    pos1.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos1.value[0] < 0) pos1.value[0] = 0
    if (pos1.value[0] > document.body.clientWidth) pos1.value[0] = document.body.clientWidth - 50
    pos1.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos1.value[1] < 0) pos1.value[1] = 0
    if (pos1.value[1] > document.body.clientHeight) pos1.value[1] = document.body.clientHeight - 50

    pos2.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos2.value[0] < 0) pos2.value[0] = 0
    if (pos2.value[0] > document.body.clientWidth) pos2.value[0] = document.body.clientWidth - 50
    pos2.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos2.value[1] < 0) pos2.value[1] = 0
    if (pos2.value[1] > document.body.clientHeight) pos2.value[1] = document.body.clientHeight - 50

    pos3.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos3.value[0] < 0) pos3.value[0] = 0
    if (pos3.value[0] > document.body.clientWidth) pos3.value[0] = document.body.clientWidth - 50
    pos3.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos3.value[1] < 0) pos3.value[1] = 0
    if (pos3.value[1] > document.body.clientHeight) pos3.value[1] = document.body.clientHeight - 50

    pos4.value[0] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos4.value[0] < 0) pos4.value[0] = 0
    if (pos4.value[0] > document.body.clientWidth) pos4.value[0] = document.body.clientWidth - 50
    pos4.value[1] += ((Math.random() < 0.5) ? (1000 * Math.random()) : (-1000 * Math.random()))
    if (pos4.value[1] < 0) pos4.value[1] = 0
    if (pos4.value[1] > document.body.clientHeight) pos4.value[1] = document.body.clientHeight - 50
  }, speed.value)
  clearInterval(rotating)
  rotating = setInterval(function ()
  {
    if (deg.value == 360) deg.value = 1
    else deg.value += 1
  }, rotSpeed.value)
  setTimeout(() =>
  {
    isAlive1.value = true
    isAlive2.value = true
    isAlive3.value = true
    isAlive4.value = true
  }, 1000)
}

// eslint-disable-next-line
function draw(event)
{
  let ctx = canvas.value.getContext("2d");
  let ex = event.x
  let ey = event.y
  let defx = ex - x
  let defy = ey - y

  if (!(defy == 0 && defx == 0)) arrowDeg.value = Math.atan2(defy, defx) * (180 / Math.PI) + 90
  ctx.beginPath();
  ctx.moveTo(x, y);
  ctx.lineTo(ex, ey);
  ctx.lineWidth = 5;
  ctx.lineCap = 'round';
  ctx.strokeStyle = line.value.value
  ctx.stroke();
  arrowX.value = x - 20
  arrowY.value = y - 20
  x = ex
  y = ey
  points.push([x, y])
}

function start()
{
  if (!allow) return
  x = left.value + 20
  y = top.value + 20
  points.push([x, y])
  window.addEventListener("mouseup", stop)
  canvas.value.addEventListener("mousemove", draw)
}

function stop()
{
  if (!allow) return
  massage.value = false
  allow = false
  arrowX.value = points[points.length - 1][0] - 20
  arrowY.value = points[points.length - 1][1] - 20
  canvas.value.removeEventListener("mousemove", draw)
  window.removeEventListener("mouseup", stop)
  let i = 0
  const fade = setInterval(() =>
  {
    if (i >= points.length - 1)
    {
      allow = true
      points = []
      clearInterval(fade)
      return
    }
    let ctx = canvas.value.getContext("2d");
    ctx.beginPath();
    ctx.moveTo(points[i][0], points[i][1]);
    ctx.lineTo(points[i + 1][0], points[i + 1][1]);
    ctx.lineWidth = 7;
    ctx.lineCap = 'round';
    ctx.strokeStyle = '#1D2D44'
    ctx.stroke();
    top.value = points[i + 1][1] - 20
    left.value = points[i + 1][0] - 20
    let enemyLeft = enemy1.value.offsetLeft
    let enemyTop = enemy1.value.offsetTop
    if ((top.value > enemyTop - 40 && top.value < enemyTop + 40) && (left.value > enemyLeft - 40 && left.value < enemyLeft + 40))
    {
      isAlive1.value = false
      incLevel()
    }
    enemyLeft = enemy2.value.offsetLeft
    enemyTop = enemy2.value.offsetTop
    if ((top.value > enemyTop - 40 && top.value < enemyTop + 40) && (left.value > enemyLeft - 40 && left.value < enemyLeft + 40))
    {
      isAlive2.value = false
      incLevel()
    }
    enemyLeft = enemy3.value.offsetLeft
    enemyTop = enemy3.value.offsetTop
    if ((top.value > enemyTop - 40 && top.value < enemyTop + 40) && (left.value > enemyLeft - 40 && left.value < enemyLeft + 40))
    {
      isAlive3.value = false
      incLevel()
    }
    enemyLeft = enemy4.value.offsetLeft
    enemyTop = enemy4.value.offsetTop
    if ((top.value > enemyTop - 40 && top.value < enemyTop + 40) && (left.value > enemyLeft - 40 && left.value < enemyLeft + 40))
    {
      isAlive4.value = false
      incLevel()
    }
    i++
  }, Math.min(500 / points.length, 20))
}

window.addEventListener("resize", function ()
{
  canvas.value.width = document.body.clientWidth;
  canvas.value.height = document.body.clientHeight;
});

</script>

<template>

  <div v-if="massage"
    class="absolute left-[480px] top-[460px] text-xl font-semibold pointer-events-none text-[#EAE8FF] z-30">
    Drag me
  </div>

  <div class="w-10 h-10 rounded-full z-30 cursor-pointer "
    :style="'position:absolute; top:' + top + 'px; left:' + left + 'px; background-color: ' + user.value + '; -webkit-box-shadow: 0px 0px 50px 16px ' + user.value + '; box-shadow: 0px 0px 50px 16px ' + user.value + ';'"
    @mousedown.prevent="start"></div>

  <div :class="(isAlive1) ? '' : 'hidden'"
    class="ease-linear w-10 h-10 rounded-full z-30 pointer-events-none transition-all" ref="enemy1"
    :style="'transition-duration: ' + speed + 'ms; position:absolute; top: ' + pos1[1] + 'px; left: ' + pos1[0] + 'px; background-color: ' + enemy.value + '; -webkit-box-shadow: 0px 0px 50px 16px ' + enemy.value + '; box-shadow: 0px 0px 50px 16px ' + enemy.value + ';'">
  </div>

  <div :class="(isAlive2) ? '' : 'hidden'"
    class="ease-linear w-10 h-10 rounded-full z-30 pointer-events-none transition-all" ref="enemy2"
    :style="'transition-duration: ' + speed + 'ms; position:absolute; top: ' + pos2[1] + 'px; left: ' + pos2[0] + 'px; background-color: ' + enemy.value + '; -webkit-box-shadow: 0px 0px 50px 16px ' + enemy.value + '; box-shadow: 0px 0px 50px 16px ' + enemy.value + ';'">
  </div>

  <div :class="(isAlive3) ? '' : 'hidden'"
    class="ease-linear w-10 h-10 rounded-full z-30 pointer-events-none transition-all" ref="enemy3"
    :style="'transition-duration: ' + speed + 'ms; position:absolute; top: ' + pos3[1] + 'px; left: ' + pos3[0] + 'px; background-color: ' + enemy.value + '; -webkit-box-shadow: 0px 0px 50px 16px ' + enemy.value + '; box-shadow: 0px 0px 50px 16px ' + enemy.value + ';'">
  </div>

  <div :class="(isAlive4) ? '' : 'hidden'"
    class="ease-linear w-10 h-10 rounded-full z-30 pointer-events-none transition-all" ref="enemy4"
    :style="'transition-duration: ' + speed + 'ms; position:absolute; top: ' + pos4[1] + 'px; left: ' + pos4[0] + 'px; background-color: ' + enemy.value + '; -webkit-box-shadow: 0px 0px 50px 16px ' + enemy.value + '; box-shadow: 0px 0px 50px 16px ' + enemy.value + ';'">
  </div>

  <svg class="w-10 h-10 z-20 pointer-events-none"
    :style="'position:absolute; top:' + arrowY + 'px; left:' + arrowX + 'px; transform: rotate(' + arrowDeg + 'deg)'"
    viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
    <path d="M19.9201 15.0499L13.4001 8.52989C12.6301 7.75989 11.3701 7.75989 10.6001 8.52989L4.08008 15.0499"
      :stroke="line.value" stroke-width="1.5" stroke-miterlimit="10" stroke-linecap="round" stroke-linejoin="round" />
  </svg>

  <canvas class="absolute top-0 right-0 bg-[#1D2D44]" width="500" height="500" ref="canvas"></canvas>


  <div class="p-2 rounded-full bg-[#0D1321] m-10 w-fit relative z-10 overflow-hidden" style="-webkit-box-shadow: 0px 0px 31px 12px #3066BE; 
box-shadow: 0px 0px 31px 12px #3066BE;">
    <div class="flex gap-4">
      <input class="w-8 h-8 cursor-pointer opacity-0" type="color" value="#48E5C2" ref="user">
      <input class="w-8 h-8 cursor-pointer opacity-0" type="color" value="#DE6B48" ref="enemy">
      <input class="w-8 h-8 cursor-pointer opacity-0" type="color" value="#EAE8FF" ref="line">
    </div>
    <div class="flex gap-4 -mt-[2rem]">
      <div class="w-[1.875rem] h-[1.875rem] rounded-full ml-[0.0625rem] mt-[0.0625rem] pointer-events-none"
        :style="'background-color: ' + user.value + ';'"></div>
      <div class="w-[1.875rem] h-[1.875rem] rounded-full ml-[0.125rem] mt-[0.0625rem] pointer-events-none"
        :style="'background-color: ' + enemy.value + ';'">
      </div>
      <svg class="w-8 h-8 pointer-events-none" viewBox="0 0 24 24" :stroke="line.value" fill="none"
        xmlns="http://www.w3.org/2000/svg">
        <path
          d="M12 22C17.5228 22 22 17.5228 22 12C22 6.47715 17.5228 2 12 2C6.47715 2 2 6.47715 2 12C2 17.5228 6.47715 22 12 22Z"
          stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
        <path d="M12 15.5V9.5" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
        <path d="M9 11.5L12 8.5L15 11.5" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      </svg>
    </div>
  </div>

  <div class="absolute right-6 bottom-6 w-40 h-40 bg-[#0D1321] rounded-full flex items-center justify-center" style="-webkit-box-shadow: 0px 0px 31px 12px #3066BE; 
box-shadow: 0px 0px 31px 12px #3066BE;" @click="incLevel" :style="'transform: rotate(' + deg + 'deg)'">

    <div class="text-2xl font-bold text-[#EAE8FF]" :style="'transform: rotate(' + -deg + 'deg)'">
      {{ level }}
    </div>

    <svg v-if="!isAlive1" class="w-10 h-10 absolute top-2 right-[3.75rem]" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#48E5C2"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.75 12L10.58 14.83L16.25 9.17004" stroke="#48E5C2" stroke-width="1.5" stroke-linecap="round"
        stroke-linejoin="round" />
    </svg>
    <svg v-else class="w-10 h-10 absolute top-2 right-[3.75rem]" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#DE6B48"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M15.9965 12H16.0054" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M11.9955 12H12.0045" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.99451 12H8.00349" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
    </svg>

    <svg v-if="!isAlive2" class="w-10 h-10 absolute top-[3.75rem] right-2" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#48E5C2"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.75 12L10.58 14.83L16.25 9.17004" stroke="#48E5C2" stroke-width="1.5" stroke-linecap="round"
        stroke-linejoin="round" />
    </svg>
    <svg v-else class="w-10 h-10 absolute top-[3.75rem] right-2" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#DE6B48"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M15.9965 12H16.0054" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M11.9955 12H12.0045" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.99451 12H8.00349" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
    </svg>

    <svg v-if="!isAlive3" class="w-10 h-10 absolute bottom-2 right-[3.75rem]"
      :style="'transform: rotate(' + -deg + 'deg)'" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#48E5C2"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.75 12L10.58 14.83L16.25 9.17004" stroke="#48E5C2" stroke-width="1.5" stroke-linecap="round"
        stroke-linejoin="round" />
    </svg>
    <svg v-else class="w-10 h-10 absolute bottom-2 right-[3.75rem]" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#DE6B48"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M15.9965 12H16.0054" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M11.9955 12H12.0045" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.99451 12H8.00349" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
    </svg>

    <svg v-if="!isAlive4" class="w-10 h-10 absolute top-[3.75rem] left-2" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#48E5C2"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.75 12L10.58 14.83L16.25 9.17004" stroke="#48E5C2" stroke-width="1.5" stroke-linecap="round"
        stroke-linejoin="round" />
    </svg>
    <svg v-else class="w-10 h-10 absolute top-[3.75rem] left-2" :style="'transform: rotate(' + -deg + 'deg)'"
      viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M12 22C17.5 22 22 17.5 22 12C22 6.5 17.5 2 12 2C6.5 2 2 6.5 2 12C2 17.5 6.5 22 12 22Z" stroke="#DE6B48"
        stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M15.9965 12H16.0054" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M11.9955 12H12.0045" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
      <path d="M7.99451 12H8.00349" stroke="#DE6B48" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
    </svg>
  </div>
</template>

<style>
#app {}

html,
body {
  height: 100%;
  margin: 0;
  overflow: hidden;
}
</style>
