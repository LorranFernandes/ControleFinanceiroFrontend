# Vue 3 + TypeScript + Vite

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

Learn more about the recommended Project Setup and IDE Support in the [Vue Docs TypeScript Guide](https://vuejs.org/guide/typescript/overview.html#project-setup).

# Controle Financeiro - Frontend

Interface web desenvolvida em **Vue 3 com TypeScript** para controle de despesas pessoais. O sistema permite lançamentos de despesas do tipo **cheque**, **parcelada** e **periódica**, com formulário inteligente que adapta os campos conforme o tipo selecionado. Os dados são exibidos em uma tabela com filtros dinâmicos, ações em linha e integração total com a API backend.

## 🚀 Funcionalidades

- Cadastro de despesas com tipos:
  - Cheque (com campos como banco, titular e beneficiário)
  - Parcelada (cria várias parcelas com datas futuras automaticamente)
  - Periódica (cria lançamentos mensais recorrentes)
- Interface reativa com Vue 3 + Composition API
- Tabela interativa com:
  - Exclusão
  - Marcar como paga
- Filtros por data, categoria e nome da conta
- Comunicação com backend via Axios

## 🛠 Tecnologias utilizadas

- Vue 3
- TypeScript
- Axios
- Vite

## 📦 Instalação local

```bash
git clone https://github.com/LorranFernandes/ControleFinanceiroFrontend.git
cd ControleFinanceiroFrontend
npm install
npm run dev

