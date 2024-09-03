import pandas as pd
import matplotlib.pyplot as plt

# Carregar o arquivo Excel
file_path = r'C:\Users\GuilhermeGoncalvesDa\Downloads\grafico logistica\BD_Logistica.xlsx'
df = pd.read_excel(file_path)

# Convertendo a coluna de data para o tipo datetime
df['Data Emissão Pedido'] = pd.to_datetime(df['Data Emissão Pedido'])

# Extraindo o ano da data de emissão
df['Ano'] = df['Data Emissão Pedido'].dt.year

# Contando o número de pedidos por ano e status
df_grouped = df.groupby(['Ano', 'Status']).size().unstack(fill_value=0)

# Criando o gráfico
df_grouped.plot(kind='line', marker='o', color=['#1f77b4', '#ff7f0e', '#2ca02c'])

# Títulos e rótulos
plt.title('Pedidos por Ano e Status de Entrega')
plt.xlabel('Ano')
plt.ylabel('Número de Pedidos')
plt.xticks(df_grouped.index)
plt.grid(True)

# Exibir o gráfico
plt.show()
