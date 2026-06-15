# Nexus PROMETHEE — Fluxos de Preferências Não-Compensatórios

Este repositório é o módulo independente do ecossistema **NEXUS MCDM**, configurado para operar exclusivamente com a família de métodos **PROMETHEE (Preference Ranking Organization Method for Enrichment Evaluations)**.

---

## 🎨 Identidade Visual e Branding
- **Nome Oficial:** Nexus PROMETHEE
- **Cores Oficiais:** Ciano (`#06B6D4`) e Roxo Profundo (`#6D28D9`)
- **Conceito Visual:** Setas direcionais de fluxos líquidos de atratividade e fraqueza.
- **Copyright:** Direitos Reservados © 2026 NEXUS-MCDM.

---

## 🌟 Recursos e Matemática

- **Variantes Suportadas:**
  - **PROMETHEE I:** Ordenação parcial das alternativas exibindo incomparabilidades estruturais.
  - **PROMETHEE II:** Ordenação completa baseada no fluxo líquido de preferência.
  - **PROMETHEE III:** Ordenação baseada em intervalos de confiança e limiares estocásticos.
  - **PROMETHEE IV:** Ordenação contínua.
  - **PROMETHEE V:** Seleção de portfólio de projetos sujeito a restrição de orçamento físico resolvido por PL binária (Knapsack 0-1).
  - **PROMETHEE TRI:** Alocação de alternativas em classes.
- **Fluxos de Preferência:**
  - *Fluxo de Saída (Φ⁺):* O quanto a alternativa domina.
  - *Fluxo de Entrada (Φ⁻):* O quanto a alternativa é dominada.
  - *Fluxo Líquido (Φ):* `Φ = Φ⁺ - Φ⁻`
- **Relatório Técnico PDF:** Relatório ReportLab com portfólios, fluxos e rankings.

---

## 🚀 Instalação e Execução
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python app.py
```
