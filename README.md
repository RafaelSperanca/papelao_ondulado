# Papelão Ondulado
Este projeto analisa e prevê a **produção mensal de papelão ondulado no Brasil** utilizando técnicas de séries temporais, em especial o modelo **SARIMAX**.   Os dados históricos vão de **1980 a 2024**, disponibilizados pela ABPO.

## 💡 Inspiração

A motivação deste projeto surgiu a partir de um comentário feito por um professor, anos atrás, de que, em alguns casos, a **produção de papelão ondulado** é um importante indicador antecedente da atividade econômica.  

Isso porque o papelão é amplamente utilizado em embalagens de bens de consumo e duráveis, refletindo diretamente os ciclos de produção e distribuição da economia.  

Assim, ao analisar sua série histórica, podemos extrair sinais sobre o ritmo da economia brasileira em diferentes períodos, inclusive durante choques como a pandemia de 2020.


## 🔍 Metodologia

1. **Exploração inicial**
   - Visualização da série temporal.
   - Identificação de tendência e sazonalidade.
   - ACF e PACF para defasagens relevantes.

2. **Pré-processamento**
   - Divisão em treino (1980–2011) e teste (2012–2024).
   - Testes de estacionariedade.

3. **Modelagem**
   - Testes com **ARIMA e SARIMAX**.
   - Seleção do melhor modelo com base em AIC/BIC.
   - Validação por análise dos resíduos (Ljung-Box, Jarque-Bera, QQ-plot, histograma).

---

## Tecnologias e Ferramentas Utilizadas

- Python (Pandas, Numpy, Matplotlib, Seaborn, Sciki-Learn, Statsmodels, ambientes virtuais);
- Estatísticas;
- Limpeza, manipulação, visualização e exploração de dados.

---

## 📈 Visualizações

- Série histórica + previsão
- ACF e PACF
- Diagnósticos de resíduos:
  - Histograma  
  - QQ-plot  
  - Correlograma
 
---
  
## 📊 Resultados

O primeiro passo foi criar uma visualização da série original. Observa-se uma forte tendência de alta no início da década de 90.

<img width="1500" height="600" alt="Image" src="https://github.com/user-attachments/assets/64533fac-0b74-4e04-ba64-d50e562d222b" />

Usando o seasonal_decompose, no modelo aditivo, para observar a série original, tendência, sazonalidade e os resíduos, o comportamento anterior se confirma, além de mostrar uma forte sazonalidade.

<img width="1600" height="1500" alt="Image" src="https://github.com/user-attachments/assets/89b51741-846d-451c-8cc6-b2819e473608" />


O gráfico de ACF e PACF parcial é utilizado para identificar se a série é estacionária e sua respectiva sazonalidade. Na imagem temos indícios que a série não é estacionária, o gráfico ACF mostra um decaimento muito lento e gradual, com valores altos e persistentes por muitos lags. Já PACF mostra uma sazonalidade de 12 meses.

<img width="1200" height="400" alt="Image" src="https://github.com/user-attachments/assets/1c29dfc5-39b7-4913-80a1-f306d56df53b" />

Mesmo utilizando o auto arima para escolher o melhor modelo para a série, assim como a análise de ACF mostrou, a série não se mostrou estacionária, onde se fez necessária a diferenciação para uma defasagem.

O Summary do modelo tras os principais resultado do modelo escolhido pelo auto arima com base nos menores AIC e BIC. Os componentes autoregressivos e de médias moveis se mostrarem estatiscamente relevantes para o modelo.
O residuos se mostraram independes (sem autocorrelação) , ou seja, passaram no teste de **Ljung-Box**, apresentando um p-valor maior que 0,05. Já o teste de **Jarque-Bera** avalia se os resíduos de um modelo seguem uma distribuição normal, o que não foi observado no modelo com um resultado de 0.00.

<img width="613" height="383" alt="Image" src="https://github.com/user-attachments/assets/b313eee1-eb6f-4c7a-aebf-fa8c5281a705" />


- Melhor modelo: **SARIMAX(2,0,0)(0,1,1)[12]**
  - Captura persistência de curto prazo (AR(1)=0.89).
  - Sazonalidade anual representada por um termo de média móvel.
- Resíduos sem autocorrelação (bom ajuste).
- Resíduos não normais (caudas pesadas), o que pode afetar intervalos de confiança.
- A pandemia de 2020 aparece como **choque estrutural não previsto** pelo modelo.

### 📌 Métricas principais
- **AIC** ≈ 7754  
- **BIC** ≈ 7769  
- **Ljung-Box** p=0.99 → resíduos independentes  
- **Jarque-Bera** p<0.001 → resíduos não normais

---


