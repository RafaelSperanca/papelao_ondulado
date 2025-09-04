# Papelão Ondulado
Este projeto analisa e prevê a **produção mensal de papelão ondulado no Brasil** utilizando técnicas de séries temporais, em especial o modelo **SARIMAX**.   Os dados históricos vão de **1980 a 2024**, disponibilizados pela ABPO.

## Inspiração

A motivação deste projeto surgiu a partir de um comentário feito por um professor, anos atrás, de que, em alguns casos, a **produção de papelão ondulado** é um importante indicador antecedente da atividade econômica.  

Isso porque o papelão é amplamente utilizado em embalagens de bens de consumo e duráveis, refletindo diretamente os ciclos de produção e distribuição da economia.  

Assim, ao analisar sua série histórica, podemos extrair sinais sobre o ritmo da economia brasileira em diferentes períodos, inclusive durante choques como a pandemia de 2020.


## Metodologia

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

## Visualizações

- Série histórica + previsão
- ACF e PACF
- Diagnósticos de resíduos:
  - Histograma  
  - QQ-plot  
  - Correlograma
 
---
  
## Resultados

O primeiro passo foi criar uma visualização da série original. Observa-se uma forte tendência de alta no início da década de 90.

<img width="1500" height="600" alt="Image" src="https://github.com/user-attachments/assets/64533fac-0b74-4e04-ba64-d50e562d222b" />

Usando o seasonal_decompose, no modelo aditivo, para observar a série original, tendência, sazonalidade e os resíduos, o comportamento anterior se confirma, além de mostrar uma forte sazonalidade.

<img width="1600" height="1500" alt="Image" src="https://github.com/user-attachments/assets/89b51741-846d-451c-8cc6-b2819e473608" />


O gráfico de ACF e PACF parcial é utilizado para identificar se a série é estacionária e sua respectiva sazonalidade. Na imagem temos indícios que a série não é estacionária, o gráfico ACF mostra um decaimento muito lento e gradual, com valores altos e persistentes por muitos lags. Já PACF mostra uma sazonalidade de 12 meses.

<img width="1200" height="400" alt="Image" src="https://github.com/user-attachments/assets/1c29dfc5-39b7-4913-80a1-f306d56df53b" />

Para automatizar o processo de escolha dos melhores parâmetros p,d e q e para detctar a presença de sazonalidade na série temporal, para o parâmetros P,D e Q foi utilizado o AutoARIMA. O resultados obtidos foram:

- Melhor modelo: **SARIMAX(2,0,0)(0,1,1)[12]**

O gráfico abaixo compara graficamente os valores reais com as previsões. Percebe-se que os dados previstos não acompnham muito bem o movimento dos valores reais, porém, seguem sua tendência.

<img width="1500" height="600" alt="Image" src="https://github.com/user-attachments/assets/5ba7bbe8-9089-4752-93e4-9dac81357186" />


O Summary do modelo tras os principais resultado do modelo escolhido pelo auto arima com base nos menores AIC e BIC. Os componentes autoregressivos e de médias moveis se mostrarem estatiscamente relevantes para o modelo.
O residuos se mostraram independes (sem autocorrelação) , ou seja, passaram no teste de **Ljung-Box**, apresentando um p-valor maior que 0,05. Já o teste de **Jarque-Bera** avalia se os resíduos de um modelo seguem uma distribuição normal, o que não foi observado no modelo com um resultado de 0.00.

<img width="613" height="383" alt="Image" src="https://github.com/user-attachments/assets/20c71c80-13b5-45c7-9a80-c92e9c53f602" />

- **Métricas principais**
   - **AIC** ≈ 11363,73  
   - **BIC** ≈ 11385,07  
   - **Ljung-Box** p=0.99 → resíduos independentes  
   - **Jarque-Bera** p<0.001 → resíduos não normais

- **Valores Treinados**

Ao realizar a previsão sobre os dados de treino, observa-se que os valores previstos apresentam um bom alinhamento em relação aos valores reais.

<img width="2000" height="600" alt="Image" src="https://github.com/user-attachments/assets/1bd8bd9b-4a6d-4a51-8101-247042c151b4" />


## Avaliação do modelo

O desempenho do modelo foi avaliado tanto no conjunto de treino quanto no de teste, utilizando diferentes métrica de erro

- **Período de Teste (2012–2024)**
- **RMSE: 16.835**
- **MAPE: 4,1%**
- **MAE: 12.339**
- **R²: 0,713**
  
**Obs:** indica que o modelo explica aproximadamente **71% da variabilidade dos dados**, com um erro percentual médio em torno de **4%**

- **Período de Treino (1980–2011)**
- **RMSE: 10.917**
- **MAPE: 0,6%**
- **MAE: 7.701**
- **R²: 0,971**
  
**Obs:** Mostra um forte ajuste nos dados de treino, cerca de **97%**


## Análise dos resíduos

No gráfico abaixo apresentamos a análise dos resíduos, incluindo o histograma, o gráfico QQ e o correlograma.

**1 - Resíduos padronizados:** observa-se que os resíduos estão em torno de zero, sem nehum padrão aparente. Porém, há alguns picos ocasionais, como em 2020, efeito da pandemia.

**2 - Histograma + densidade:** os resíduos apresentam formato aproximadamente simétrico, mas com caudas mais pesadas do que a normal téorica, linha verde.

**3 - Gráfico QQ:** A maior parte dos pontos seguem a linha vermelha, mas há desvios significativos nas extremidades, confirmando as caudas pesadas.

**4 - Correlograma:** Não há autocorrelação significativa nos resíduos (a maioria está dentro do intervalo de confiança), indicando que o modelo capturou bem a estrutura temporal.


<img width="1000" height="600" alt="Image" src="https://github.com/user-attachments/assets/2a4a236d-7792-4273-aa22-a65ab2b1dc1a" />

---
## Previsão

Mesmo que o modelo não tenha atendido plenamente a análise dos resíduos, seguiremos com a previsão utilizando todos os dados, ou seja, realizando um novo treinamento do modelo.

Gráfico mostra a previsão para 12 períodos.

<img width="2000" height="600" alt="Image" src="https://github.com/user-attachments/assets/fa38660a-503d-43d7-bbbf-35a68342f07a" />

O gráfico abaixo compara os valores reais da produção de papelão ondulado (linha azul) com as previsões geradas pelo modelo SARIMAX (linha amarela) para o ano de 2025.

- Observa-se que o modelo acompanha bem a tendência geral da série, capturando os movimentos de queda e recuperação ao longo dos meses.

- Em alguns pontos, como junho e agosto, a previsão apresenta desvios em relação ao valor real, mas ainda mantém o padrão de sazonalidade.

- Esse comportamento indica que o modelo é capaz de gerar previsões consistentes no curto prazo, embora choques ou variações abruptas (como em julho e agosto) sejam mais difíceis de antecipar

<img width="1500" height="600" alt="Image" src="https://github.com/user-attachments/assets/44d9e871-4305-4034-8c20-5c419fee9606" />

---
**Autor:** Rafael Sperança

**Ano:** 2025
