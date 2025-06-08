<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style> -->

<template>
  <div id="app" class="container">
    <header>
      <h1>Vue 3 变量管理演示</h1>
      <p class="subtitle">
        展示如何使用 Composition API 管理各种类型的变量，包括基本类型、数组、对象以及复杂自定义结构体
      </p>
    </header>

    <div class="dashboard">
      <!-- 基本类型 -->
      <div class="card">
        <h2>基本类型</h2>
        <div class="data-item">
          <div class="data-label">字符串 (ref)</div>
          <div class="data-value">{{ message }}</div>
          <input type="text" v-model="message" placeholder="输入新消息..." />
        </div>

        <div class="data-item">
          <div class="data-label">数字 (ref)</div>
          <div class="counter">
            <div class="counter-value">{{ count }}</div>
            <div class="controls">
              <button @click="increment">+1</button>
              <button @click="decrement">-1</button>
            </div>
          </div>
        </div>

        <div class="data-item">
          <div class="data-label">布尔值 (ref)</div>
          <div class="data-value">{{ isActive ? '激活状态' : '未激活' }}</div>
          <div class="controls">
            <button @click="toggleActive">切换状态</button>
          </div>
        </div>
      </div>

      <!-- 数组和对象 -->
      <div class="card">
        <h2>数组和对象</h2>
        <div class="data-item">
          <div class="data-label">数组 (ref)</div>
          <div class="data-value">
            <div v-for="(item, idx) in items" :key="idx">
              {{ idx + 1 }}. {{ item }}
            </div>
          </div>
          <div class="controls">
            <button @click="addItem">添加项目</button>
            <button @click="removeItem">移除项目</button>
          </div>
        </div>

        <div class="data-item">
          <div class="data-label">响应式对象 (reactive)</div>
          <div class="complex-data">
            <div>
              <div class="data-label">用户名</div>
              <div class="data-value">{{ user.username }}</div>
              <input type="text" v-model="user.username" placeholder="输入用户名" />
            </div>
            <div>
              <div class="data-label">邮箱</div>
              <div class="data-value">{{ user.email }}</div>
              <input type="email" v-model="user.email" placeholder="输入邮箱" />
            </div>
            <div>
              <div class="data-label">角色</div>
              <div class="data-value">{{ user.role }}</div>
              <select v-model="user.role">
                <option value="admin">管理员</option>
                <option value="editor">编辑</option>
                <option value="viewer">查看者</option>
              </select>
            </div>
          </div>
        </div>
      </div>

      <!-- 复杂结构体 -->
      <div class="card">
        <h2>复杂结构体</h2>
        <div class="data-item">
          <div class="data-label">产品信息 (reactive)</div>
          <div class="complex-data">
            <div>
              <div class="data-label">产品名称</div>
              <div class="data-value">{{ product.name }}</div><input type="text" v-model="product.name"
                placeholder="产品名称" />
            </div>
            <div>
              <div class="data-label">价格</div>
              <div class="data-value">¥{{ product.price.toFixed(2) }}</div><input type="number"
                v-model.number="product.price" step="0.01" min="0" placeholder="价格" />
            </div>
            <div>
              <div class="data-label">库存</div>
              <div class="data-value">{{ product.stock }}</div><input type="number" v-model.number="product.stock"
                min="0" placeholder="库存" />
            </div>
          </div>
        </div>

        <div class="data-item">
          <div class="data-label">订单详情 (嵌套对象)</div>
          <div class="complex-data">
            <div>
              <div class="data-label">订单ID</div>
              <div class="data-value">{{ order.id }}</div>
            </div>
            <div>
              <div class="data-label">客户</div>
              <div class="data-value">{{ order.customer.name }}</div>
            </div>
            <div>
              <div class="data-label">总金额</div>
              <div class="data-value">¥{{ order.total.toFixed(2) }}</div>
            </div>
            <div>
              <div class="data-label">状态</div>
              <div class="data-value">{{ order.status }}</div>
            </div>
          </div>
          <div class="controls">
            <button @click="updateOrderStatus">更新状态</button>
            <button @click="calculateTotal">重新计算总额</button>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <h2>计算属性和监听器</h2>
      <div class="data-item">
        <div class="data-label">计算属性 (产品折扣价)</div>
        <div class="data-value">¥{{ discountedPrice.toFixed(2) }} ({{ discountRate * 100 }}% 折扣)</div>
      </div>

      <div class="data-item">
        <div class="data-label">监听器日志</div>
        <div class="data-value log-list">
          <div v-for="(log, idx) in logs" :key="idx" class="log-item">{{ log }}</div>
        </div>
      </div>
    </div>

    <footer>
      <p>Vue 3 Composition API 变量管理演示 | 使用 ref, reactive, computed, watch 等特性</p>
    </footer>
  </div>
</template>

<script setup>
import { ref, reactive, computed, watch, onMounted } from 'vue'

// 基本变量
const message = ref('欢迎使用Vue 3 Composition API')
const count = ref(0)
const isActive = ref(true)

// 数组 & 对象
const items = ref(['项目A', '项目B', '项目C'])
const user = reactive({ id: 1, username: 'vue_user', email: 'user@vue3.com', role: 'admin' })

// 复杂对象
const product = reactive({ id: 101, name: 'Vue 3 高级教程', price: 99.99, stock: 50, category: '书籍' })
const order = reactive({
  id: 2023001,
  customer: { id: 1001, name: '张三', email: 'zhangsan@example.com', address: '北京市朝阳区' },
  items: [{ productId: 101, quantity: 2, price: 99.99 }, { productId: 102, quantity: 1, price: 49.99 }],
  total: 0,
  status: '处理中'
})



const discountRate = ref(0.2)
const discountedPrice = computed(() => product.price * (1 - discountRate.value))

// 日志
const logs = ref([])
function addLog(text) {
  const ts = new Date().toLocaleTimeString()
  logs.value.unshift(`[${ts}] ${text}`)
  if (logs.value.length > 10) logs.value.pop()
}

// 方法
function calculateTotal() {
  order.total = order.items.reduce((sum, item) => sum + item.price * item.quantity, 0)
  addLog(`计算订单总额: ¥${order.total.toFixed(2)}`)
}
calculateTotal()

// Watchers
watch(count, (newV, oldV) => addLog(`计数器变化: ${oldV} → ${newV}`))
watch(() => product.price, (newP, oldP) => addLog(`产品价格变化: ¥${oldP.toFixed(2)} → ¥${newP.toFixed(2)}`))
watch(user, newU => addLog(`用户信息更新: ${newU.username} (${newU.role})`), { deep: true })

// 交互函数
function increment() { count.value++ }
function decrement() { count.value-- }
function toggleActive() { isActive.value = !isActive.value; addLog(`状态切换为: ${isActive.value ? '激活' : '未激活'}`) }
function addItem() { const item = `项目${String.fromCharCode(65 + items.value.length)}`; items.value.push(item); addLog(`添加项目: ${item}`) }
function removeItem() { if (items.value.length) { const rem = items.value.pop(); addLog(`移除项目: ${rem}`) } }
function updateOrderStatus() {
  const ss = ['处理中', '已发货', '已完成', '已取消']
  const i = ss.indexOf(order.status)
  order.status = ss[(i + 1) % ss.length]
  addLog(`订单状态更新: ${order.status}`)
}

onMounted(() => addLog('组件已挂载'))
</script>

<style scoped>
/* 你原来复制的所有样式都可以保留在这里 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
  background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
  color: #fff;
  min-height: 100vh;
  padding: 20px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

header {
  text-align: center;
  padding: 30px 0;
  margin-bottom: 40px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

h1 {
  font-size: 2.8rem;
  margin-bottom: 10px;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}

.subtitle {
  font-size: 1.2rem;
  opacity: 0.9;
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.6;
}

.dashboard {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 25px;
  margin-bottom: 40px;
}

.card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  padding: 25px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.3);
}

.card h2 {
  font-size: 1.8rem;
  margin-bottom: 20px;
  color: #fdbb2d;
  border-bottom: 2px solid rgba(253, 187, 45, 0.3);
  padding-bottom: 10px;
}

.data-item {
  background: rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  padding: 15px;
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}

.data-label {
  font-weight: 600;
  margin-bottom: 5px;
  color: #fdbb2d;
  font-size: 0.9rem;
}

.data-value {
  font-size: 1.1rem;
  word-break: break-all;
}

.complex-data {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
  margin-top: 10px;
}

.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  margin-top: 15px;
}

button {
  background: linear-gradient(to right, #fdbb2d, #b21f1f);
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 50px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
  flex: 1;
  min-width: 120px;
}

button:hover {
  transform: scale(1.05);
  box-shadow: 0 5px 15px rgba(178, 31, 31, 0.4);
}

input,
select {
  background: rgba(255, 255, 255, 0.15);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  padding: 10px 15px;
  border-radius: 50px;
  width: 100%;
  margin-top: 5px;
}

input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.counter {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
}

.counter-value {
  font-size: 2rem;
  font-weight: bold;
  color: #fdbb2d;
}

footer {
  text-align: center;
  padding: 30px 0;
  margin-top: 40px;
  font-size: 0.9rem;
  opacity: 0.8;
}

@media (max-width: 768px) {
  .dashboard {
    grid-template-columns: 1fr;
  }

  h1 {
    font-size: 2.2rem;
  }
}

/* ...rest of your CSS... */
</style>
