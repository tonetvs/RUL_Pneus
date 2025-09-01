# Predição da Vida Útil Restante (RUL) de Pneus com LightGBM

Este projeto tem como objetivo construir um modelo preditivo robusto para estimar a vida útil remanescente (RUL) de pneus automotivos com base em condições operacionais, características técnicas e fatores ambientais. A aplicação dessa solução pode apoiar estratégias de manutenção preditiva, aumentar a segurança e reduzir custos com trocas prematuras ou tardias.

## Objetivo

Prever com precisão o número de quilômetros restantes até a substituição ideal de cada pneu, utilizando um dataset sintético realista e técnicas de aprendizado de máquina supervisionado. O foco está em criar uma solução interpretável, confiável e com forte apelo para demonstração em portfólios técnicos profissionais.

---

## 1. Análise Exploratória e Insights

Antes da modelagem, foi conduzida uma análise exploratória com foco em:

- Distribuição das variáveis operacionais e ambientais
- Correlação entre features e a variável alvo (`remaining_useful_life`)
- Verificação de outliers e vazamentos de informação
- Criação de features auxiliares como `pressure_diff`
- Análise de temperatura, desgaste e classificação de pneus

**Principais descobertas:**

- Variáveis como `expected_tyre_life`, `current_tread_depth` e `kilometers_driven` apresentavam vazamento e foram removidas.
- Pneus com profundidade inferior a 4 mm ou RUL inferior a 10.000 km são considerados críticos.
- Foi adotada uma classificação de status com base no RUL:
  - Saudável: > 20.000 km
  - Moderado: entre 10.000 km e 20.000 km
  - Crítico: < 10.000 km

---

## 2. Pipeline de Modelagem

```mermaid
flowchart LR
  A[Base Sintética] --> B[Limpeza e Engenharia de Features]
  B --> C[One-Hot Encoding e Padronização]
  C --> D[LightGBM Regressor]
  D --> E[Predição e Avaliação]
  E --> F[Visualizações e Interpretação]
```

### Pré-processamento

- Remoção de colunas com risco de vazamento
- One-hot encoding para categorias como combustível, transmissão, clima e tipo de estrada
- Escalonamento com `StandardScaler`

### Modelagem

- Algoritmo principal: `LGBMRegressor`
- Dataset reduzido para 300.000 amostras para viabilizar o treinamento
- Divisão: 70% treino, 15% validação, 15% teste

---

## 3. Métricas de Desempenho

### Validação
- **MAE:** 5455.15 km  
- **RMSE:** 7115.72 km  
- **R²:** 0.8414

### Teste
- **MAE:** 5425.48 km  
- **RMSE:** 7092.12 km  
- **R²:** 0.8422

O modelo apresentou **boa generalização** e **alta robustez**, mesmo após a remoção de colunas com vazamento. As métricas demonstram capacidade sólida de prever com precisão o desgaste dos pneus em diferentes condições.

---

## 4. Visualizações Geradas

- Gráfico de dispersão RUL real vs RUL previsto
- Gráfico de resíduos
- Tabela com 50 pneus:
  - RUL real, RUL previsto, erro absoluto
  - Status do pneu colorido por severidade
  - Sinalizador visual do erro (verde, amarelo, vermelho)

---

## 5. Conclusão

O modelo final baseado no LightGBM demonstrou excelente equilíbrio entre desempenho, interpretabilidade e consistência. Apesar do dataset ser sintético, o projeto oferece uma **base sólida para aplicações reais** em manutenção preditiva e segurança automotiva. Os desafios envolveram evitar vazamento de dados e lidar com alta correlação entre variáveis.

A entrega final, com métricas explicadas, visualizações bem apresentadas e classificação interpretável dos pneus, torna este projeto altamente adequado para compor um portfólio profissional na área de ciência de dados aplicada à indústria.

---

## Requisitos

As bibliotecas utilizadas estão listadas em `requirements.txt`, incluindo:

- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- lightgbm  
- plotly  

---

## Execução

```bash
git clone https://github.com/seu-usuario/rul-pneus.git
cd rul-pneus

conda create -n rul-pneus python=3.11 -y
conda activate rul-pneus
pip install -r requirements.txt

jupyter notebook RUL_Pneus.ipynb
```

---

## Autor

**Heitor Tonet**  
Engenheiro de Controle e Automação | Cientista de Dados  
Foco em manutenção preditiva, mobilidade inteligente e aplicações industriais.

## Licença

MIT License
