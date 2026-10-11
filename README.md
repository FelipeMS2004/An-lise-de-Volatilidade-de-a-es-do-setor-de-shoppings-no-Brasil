# Análise de Volatilidade de ações do setor de shoppings no Brasil
## Um estudo sobre a variação dos preços e retornos das ações de Allos, Multiplan e Iguatemi.

```import yfinance as yf
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt```

 ### Definindo o símbolo dos ativos

```ativo_1 = "ALOS3.SA"
ativo_2 = "MULT3.SA"
ativo_3 = "IGTI11.SA"```

### Baixando os dados dos ativos em um intervalo de 2022 até o momento

```dados_ativo_1 = yf.download(ativo_1, start = "2022-01-01", end = "2026-09-30")
dados_ativo_2 = yf.download(ativo_2, start = "2022-01-01", end = "2026-09-30")  
dados_ativo_3 = yf.download(ativo_3, start = "2022-01-01", end = "2026-09-30")```

### Calcular os retornos diários

```dados_ativo_1["Retorno"] = dados_ativo_1["Close"].pct_change()
dados_ativo_2["Retorno"] = dados_ativo_2["Close"].pct_change()
dados_ativo_3["Retorno"] = dados_ativo_3["Close"].pct_change()```

### Volatilidade dos retornos diários

```volatilidade_ativo_1 = dados_ativo_1["Retorno"].std()*np.sqrt(252)
volatilidade_ativo_2 = dados_ativo_2["Retorno"].std()*np.sqrt(252)
volatilidade_ativo_3 = dados_ativo_3["Retorno"].std()*np.sqrt(252)```

### Volatilidade no período em percentual

```print(f"Volatilidade anualizada do {ativo_1}: {volatilidade_ativo_1:.2%}")
print(f"Volatilidade anualizada do {ativo_2}: {volatilidade_ativo_2:.2%}")
print(f"Volatilidade anualizada do {ativo_3}: {volatilidade_ativo_3:.2%}")```

### Plotando os Gráficos

```fig, axs = plt.subplots(3,1, figsize = (12,12))```

### Gráfico dos preços de fechamento diário

```axs[0].plot(dados_ativo_1["Close"], label=ativo_1, color="Green")
axs[0].plot(dados_ativo_2["Close"], label=ativo_2, color="Red")
axs[0].plot(dados_ativo_3["Close"], label=ativo_3, color="Yellow")
axs[0].set_title("Preço de Fechamento Diário")
axs[0].legend()```

### Gráfico dos Retornos Diários

```axs[1].plot(dados_ativo_1["Retorno"], label = ativo_1, color = "Green")  
axs[1].plot(dados_ativo_2["Retorno"], label = ativo_2, color = "Red")
axs[1].plot(dados_ativo_3["Retorno"], label = ativo_3, color = "Yellow")
axs[1].set_title("Retorno Diário")
axs[1].legend()```

### Gráfico das volatilidades dos retornos diários

```axs[2].bar([0,1,2], [volatilidade_ativo_1, volatilidade_ativo_2, volatilidade_ativo_3], color= ["Green", "Red", "Yellow"])
axs[2].set_xticks([0,1,2])
axs[2].set_xticklabels([ativo_1, ativo_2, ativo_3])
axs[2].set_title("Volatilidade dos Retornos Diários")
axs[2].legend()```

### Plotando os gráficos

```plt.tight_layout()
plt.show()```
