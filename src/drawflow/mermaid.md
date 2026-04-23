Mermaid 的语法非常丰富，它不仅仅能画流程图。为了让你在 IDEA 的 Markdown 预览中达到最佳效果，我按**功能模块**为你整理了 Mermaid 的全语法示例。

你可以直接将这些代码块复制到 IDEA 的 Markdown 文件中测试。

---

### 1. 流程图 (Flowcharts)
支持多种方向（TB, BT, LR, RL）和丰富的形状。

```mermaid
graph TD
    %% 节点与形状
    Start([开始]) --> Process[普通矩形]
    Process --> Condition{判断分支}
    
    %% 分支路径
    Condition -- Yes --> SubProcess[[子程序]]
    Condition -- No --> Error((圆形错误))
    
    %% 特殊形状
    SubProcess --> DB[(数据库)]
    DB --> Output[/平行四边形数据/]
    Output --> Stop([结束])

    %% 样式定制
    style Start fill:#f9f,stroke:#333,stroke-width:4px
    style Stop fill:#ccf,stroke:#f66,stroke-dasharray: 5 5
```

---

### 2. 时序图 (Sequence Diagrams)
这是开发中使用频率最高的部分，支持逻辑判断和循环。

```mermaid
sequenceDiagram
    autonumber
    actor User as 用户
    participant Auth as 鉴权中心
    participant SRV as 业务服务器
    
    User->>Auth: 登录请求 (ID/PWD)
    Auth-->>User: 返回 Token
    
    rect rgb(240, 240, 240)
        Note over User, SRV: 业务操作流程
        User->>+SRV: 携带 Token 请求数据
        SRV->>SRV: 校验 Token
        
        alt 校验成功
            SRV-->>User: 返回 200 OK
        else 校验失败
            SRV-->>-User: 返回 401 Unauthorized
        end
    end

    loop 每分钟轮询
        SRV->>SRV: 检查心跳
    end
```

---

### 3. 类图 (Class Diagrams)
对 Java 开发者最友好，支持成员变量、方法和继承关系。

```mermaid
classDiagram
    %% 继承与实现
    Animal <|-- Duck
    Animal <|-- Fish
    BaseService <|.. OrderServiceImpl
    
    %% 类成员定义
    class Animal {
        +String name
        +int age
        #void move()
        +abstract eat()*
    }
    
    class OrderServiceImpl {
        -OrderRepo repo
        +saveOrder(Order o) boolean
    }
    
    %% 关系标注
    OrderServiceImpl *-- OrderRepo : 组合
    Customer "1" --> "n" Order : 关联
```

---

### 4. 状态图 (State Diagrams)
适合描述复杂的业务生命周期（如订单状态、线程状态）。

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Processing: 接收任务
    
    state Processing {
        [*] --> Step1
        Step1 --> Step2
        Step2 --> [*]
    }
    
    Processing --> Success: 完成
    Processing --> Failed: 报错
    
    Success --> [*]
    Failed --> Idle: 重试
```

---

### 5. 实体关系图 (ER Diagram)
用于描述数据库建模。

```mermaid
erDiagram
    USER ||--o{ ORDER : "places"
    ORDER ||--|{ LINE-ITEM : "contains"
    USER {
        string username
        string email
        string password
    }
    ORDER {
        int orderNumber
        string deliveryAddress
    }
```

---

### 6. 甘特图与用户旅程 (Gantt & User Journey)
用于项目管理和需求分析。

```mermaid
%% 甘特图
gantt
    title 项目开发计划
    dateFormat  YYYY-MM-DD
    section 需求
    调研           :a1, 2026-04-01, 10d
    方案设计        :after a1, 7d
    section 开发
    后端开发        :2026-04-15, 20d
    前端开发        :2026-04-20, 15d

%% 用户旅程
journey
    title 用户购物体验
    section 浏览
      查找商品: 5: 用户
      对比价格: 3: 用户
    section 支付
      填写地址: 4: 用户
      确认支付: 2: 用户, 银行
```

---

### 7. 饼图、心智图与象限图 (Others)
Mermaid 最近更新支持了更多的可视化类型。

```mermaid
%% 饼图
pie title 编程语言占比
    "Java" : 45
    "Python" : 25
    "Go" : 20
    "Others" : 10

%% 心智图 (Mindmap - 需要较新版本插件)
mindmap
  root((Sprival 项目))
    技术栈
      Spring Boot
      MongoDB
      WSL2
    AI 工具
      Cursor
      Mermaid
      
%% 象限图 (Quadrant Chart)
quadrantChart
    title 技术选型评估
    x-axis 低学习成本 --> 高学习成本
    y-axis 低价值 --> 高价值
    "Mermaid": [0.2, 0.8]
    "PlantUML": [0.5, 0.9]
    "Visio": [0.8, 0.2]
```

---

### IDEA 配合总结：
* **Mermaid 插件**支持以上所有语法。
* 如果你的 IDEA 预览不显示，请检查 `Settings -> Languages & Frameworks -> Markdown` 里的预览引擎是否设为 **JCEF**。
* **技巧**：在时序图中，使用 `+` 和 `-`（如 `User->>+SRV`）可以让侧边的激活条（Activation Bar）自动显示，这能极大地提高图表的可读性。

你打算把哪个类型的图表先集成到你的 `plan.md` 自动化工作流中？