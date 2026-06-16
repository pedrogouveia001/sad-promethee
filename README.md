# SAD PROMETHEE — Fluxos de Preferências Não-Compensatórios

Este repositório é o módulo independente do ecossistema **SAD MCDM**, configurado para operar exclusivamente com a família de métodos **PROMETHEE**.

---

## 🎨 Identidade Visual e Branding
- **Nome Oficial:** SAD PROMETHEE
- **Cores Oficiais:** Ciano (`#06B6D4`) e Roxo Profundo (`#6D28D9`)
- **Conceito Visual:** Setas direcionais de fluxos líquidos de atratividade e fraqueza.
- **Copyright:** Direitos Reservados © 2026 SAD-MCDM. Todos os direitos reservados.

---

## 🧠 Formulação Matemática e Funcionamento

O método **PROMETHEE** estabelece uma relação de sobreclassificação valorizada comparando as alternativas de forma através de preferências unilaterais. Ele avalia o quanto uma alternativa supera as outras (Fluxo de Saída) e o quanto ela é superada (Fluxo de Entrada).

### 1. Funções de Preferência ($P_j(a, b)$)
Mapeiam a diferença de desempenho físico $d = g_j(a) - g_j(b)$ em uma escala de preferência de 0 a 1. Os tipos implementados no resolvedor SAD são:
* **Tipo I (Usual):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le 0 \\ 1 & \text{se } d > 0 \end{cases}$$
* **Tipo II (U-Shape):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le q \\ 1 & \text{se } d > q \end{cases}$$
* **Tipo III (V-Shape):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le 0 \\ \frac{d}{p} & \text{se } 0 < d \le p \\ 1 & \text{se } d > p \end{cases}$$
* **Tipo IV (Level):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le q \\ 0.5 & \text{se } q < d \le p \\ 1 & \text{se } d > p \end{cases}$$
* **Tipo V (Linear / V-Shape com indiferença):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le q \\ \frac{d - q}{p - q} & \text{se } q < d \le p \\ 1 & \text{se } d > p \end{cases}$$
* **Tipo VI (Gaussian):**
  $$P_j(d) = \begin{cases} 0 & \text{se } d \le 0 \\ 1 - e^{-\frac{d^2}{2s^2}} & \text{se } d > 0 \end{cases}$$

### 2. Índice de Preferência Global ($\pi(a, b)$)
A atratividade média de $a$ sobre $b$ ponderada pelos pesos dos critérios $w_j$ é:
$$\pi(a, b) = \sum_{j=1}^n w_j \cdot P_j(a, b)$$

### 3. Fluxos de Preferência e Ranking
* **Fluxo de Saída Positivo ($\Phi^+(a)$):** O quanto a alternativa $a$ domina todas as outras:
  $$\Phi^+(a) = \frac{1}{m-1} \sum_{x \in A \setminus \{a\}} \pi(a, x)$$
* **Fluxo de Entrada Negativo ($\Phi^-(a)$):** O quanto a alternativa $a$ é dominada por todas as outras:
  $$\Phi^-(a) = \frac{1}{m-1} \sum_{x \in A \setminus \{a\}} \pi(x, a)$$
* **Fluxo Líquido ($\Phi(a)$) (PROMETHEE II):** Fornece a ordenação final completa:
  $$\Phi(a) = \Phi^+(a) - \Phi^-(a)$$

---

### 4. PROMETHEE V (Seleção de Portfólio de Projetos)
Para problemas em que o objetivo não é apenas ordenar, mas selecionar o melhor grupo de alternativas sujeitas a uma restrição física/financeira total $B$ (ex: orçamento):
$$\max \sum_{i=1}^m \Phi(a_i) \cdot x_i$$
$$\text{sujeito a:}$$
$$\sum_{i=1}^m c_i \cdot x_i \le B$$
$$x_i \in \{0, 1\}$$
Onde:
* $x_i = 1$ indica que a alternativa $i$ é selecionada para o portfólio.
* $c_i$ é o custo de capital da alternativa $i$.

O resolvedor SAD executa o Knapsack Problem (Problema da Mochila 0-1) usando Programação Linear Inteira para fornecer o portfólio de investimento ótimo.

---

## 🚀 Instalação e Execução
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```
Acesse: `http://127.0.0.1:5000`
