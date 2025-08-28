# Papelão Ondulado
Este projeto analisa e prevê a **produção mensal de papelão ondulado no Brasil** utilizando técnicas de séries temporais, em especial o modelo **SARIMAX**.   Os dados históricos vão de **1980 a 2024**, disponibilizados pela ABPO.

## 💡 Inspiração

A motivação deste projeto surgiu a partir de um comentário feito por um professor em aula:  
**a produção de papelão ondulado é um importante indicador antecedente da atividade econômica**.  

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

## 📊 Resultados

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

## 📈 Visualizações

- Série histórica + previsão
- ACF e PACF
- Diagnósticos de resíduos:
  - Histograma  
  - QQ-plot  
  - Correlograma  


