# 何时 Mock

只 Mock **系统边界**：

- 外部 API（支付、邮件等）
- 数据库（有时 - 优先用测试 DB）
- 时间/随机性
- 文件系统（有时）

不要 mock：

- 你自己的类/模块
- 内部协作者
- 你控制的任何东西

## 为可 Mock 性设计

在系统边界，设计易于 mock 的接口：

**1. 使用依赖注入**

传入外部依赖而非内部创建：

```typescript
// 易 mock
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// 难 mock
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

**2. 优先 SDK 风格接口而非通用 fetcher**

为每个外部操作创建特定函数，而非一个带条件逻辑的通用函数：

```typescript
// 好：每个函数独立可 mock
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch('/orders', { method: 'POST', body: data }),
};

// 坏：mock 需要条件逻辑
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```

SDK 方式意味着：
- 每个 mock 返回特定形状
- 测试设置无条件逻辑
- 更易看出测试练习了哪些端点
- 每个端点类型安全