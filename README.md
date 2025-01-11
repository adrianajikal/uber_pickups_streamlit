```markdown
# Uber Pickups Data Visualization

Este projeto utiliza o Streamlit para criar uma visualização interativa dos dados de pickups da Uber em diferentes locais e horários.

## Requisitos

Certifique-se de ter o **Python 3.7 ou superior** instalado. Além disso, instale as dependências listadas no arquivo `requirements.txt`.

## Instalação

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/uber-pickups.git
   ```

2. Navegue até a pasta do projeto:
   ```bash
   cd uber-pickups
   ```

3. Crie um ambiente virtual (opcional, mas recomendado):
   ```bash
   python -m venv myenv
   ```
   Ative o ambiente:
   - **Windows**: `myenv\Scripts\activate`
   - **macOS/Linux**: `source myenv/bin/activate`

4. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

## Como executar o aplicativo

1. Execute o script principal com o Streamlit:
   ```bash
   streamlit run uber_pickups.py
   ```

2. O navegador será aberto automaticamente. Se isso não acontecer, acesse o aplicativo manualmente no endereço mostrado no terminal (geralmente `http://localhost:8501`).

## Sobre o Script

### Código: `uber_pickups.py`

O script carrega dados de pickups da Uber e permite a visualização interativa de informações, como:
- Número de pickups em diferentes horários.
- Localização dos pickups.

### Recursos principais:
- **Carregamento de dados**: Utiliza a biblioteca Pandas para carregar e processar os dados.
- **Gráficos interativos**: Plotagens usando Streamlit.
- **Filtros por horário**: Selecione horários específicos para visualizar os pickups.

#### Estrutura do script:

```python
import streamlit as st
import pandas as pd
import numpy as np

# Título do aplicativo
st.title("Uber Pickups in NYC")

# Função para carregar dados
@st.cache
def load_data():
    data = pd.read_csv("uber-data.csv")
    data["date/time"] = pd.to_datetime(data["date/time"])
    return data

data_load_state = st.text("Loading data...")
data = load_data()
data_load_state.text("Loading data...done!")

# Visualizações
st.subheader("Raw data")
st.write(data.head())

st.subheader("Number of pickups by hour")
hist_values = np.histogram(data["date/time"].dt.hour, bins=24, range=(0, 24))[0]
st.bar_chart(hist_values)

hour_to_filter = st.slider("Hour", 0, 23, 17)
filtered_data = data[data["date/time"].dt.hour == hour_to_filter]

st.subheader(f"Map of pickups at {hour_to_filter}:00")
st.map(filtered_data)
```

## Dados

Os dados utilizados são armazenados no arquivo `uber-data.csv`. Certifique-se de incluir este arquivo na mesma pasta do script antes de executar o aplicativo.

## Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

