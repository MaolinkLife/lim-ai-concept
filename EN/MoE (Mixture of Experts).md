# MoE (Mixture of Experts)

  

# MoE (Mixture of Experts)

 

**Mixture of Experts** is an architectural approach in which a model consists of **multiple specialized “expert” submodels**. On each query, **only part of them is activated**.

 

The idea: **“not all knowledge is needed every time,”** so instead of using one giant monolithic model, we build **a set of experts,** each better at something different—and give the model **a mechanism to choose** which ones to activate.

 

### **How It Works (Mechanics)**

 

1. **Input** (text, tokens) is fed into the model.
2. A separate block called the **“Router”** decides: – which experts are best suited for this task.
3. **2–4 experts** are chosen out of, say, 16.
4. **Only the chosen experts receive the input** and produce their outputs.
5. **Outputs are aggregated** (usually averaged or summed with weights) and passed on.

 

---

 

### **Comparison with Regular Models**

 

| Model | Operating Principle | Pros | Cons |
|----|----|----|----|
| **Monolithic** | All parameters are active at each step | Simplicity, predictability | Huge computational load |
| **MoE** | Only part of the parameters are active each step | Efficiency, scalability | Implementation and routing complexity |

 

---

 

### **Why MoE Is Needed**

 

- **Scaling without rising costs**: you can create a **1-trillion-parameter** model, but only use **10%** on a query.
- **Versatility**: experts can be specialized for different types of tasks (translation, code, math).
- **Error localization**: easier to fine-tune or replace a single expert than the entire model.

 

---

 

### **Key Components of MoE**

 

1. **Experts** — submodels (usually MLP blocks).
2. **Router** — decides which to activate.
3. **Sparse Activation** — only N experts out of the full set are activated.
4. **Load Balancing Loss** — a regularizer ensuring all experts get used.

 

---

 

### **Architectures Using MoE**

 

- **Switch Transformer (Google, 2021)** — a simplified MoE: only **1 expert** is active at a time.
- **GShard** (Google) — the first scalable MoE on billions of tokens.
- **GLaM** (Google, 2021) — 1.2 trillion parameters, but 97% of them are never activated simultaneously.
- **GPT-4 (possibly)** and **GPT-4-Turbo (almost certainly)** — use MoE behind the scenes.

 

---

 

### **Example: Simple MoE Scheme**

 

```javascript
Input → [Router]
           ↓
       ┌──────────────┐
       │ Expert 1     │
       │ Expert 2     │  → (only these are active)
       │ Expert 3     │
       │ ...          │
       └──────────────┘
           ↓
     Aggregation
           ↓
        Output
```

 

---

 

### **Why It Matters**

 

Because MoE is **key to further scaling models**. You can train everything, then use only what’s needed. It’s like having an army of specialists but calling up only the right ones for the job.

  