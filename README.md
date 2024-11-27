# App de Previsão do Tempo

Aplicação REST utilizando APIs do hub rapidapi para o trabalho de Sistemas Distribuidos.

## **Relatório de Documentação da API REST**

### **1. Descrição Geral da API REST do Serviço Web Utilizado**

O projeto utiliza duas APIs REST fornecidas pelo RapidAPI:

1. **Meteostat API**: Serviço de previsão do tempo que fornece dados meteorológicos como temperatura média, mínima, máxima, precipitação e velocidade do vento com base na latitude e longitude de um ponto geográfico.
2. **GeoDB Cities API**: Serviço de geolocalização que permite buscar cidades pelo prefixo do nome, retornando informações como nome, latitude e longitude.

Ambos os serviços requerem autenticação via chaves da API (RapidAPI Key).

---

### **2. Descrição de Cada Chamada do Cliente à API**

### **2.1. Chamada: Busca de Cidades**

- **URL do Recurso**:**`https://wft-geo-db.p.rapidapi.com/v1/geo/cities`**
- **Método HTTP**:GET
- **Autenticação**:
    - **Header**:
        - **`X-RapidAPI-Key`**: 0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3.
        - **`X-RapidAPI-Host`**: **`wft-geo-db.p.rapidapi.com`**
- **Parâmetros**:
    - **`types`**: Define o tipo de local a buscar. No caso, "city".
    - **`namePrefix`**: Prefixo do nome da cidade (mínimo 3 caracteres).
- **Exemplo de Requisição**:
    
    ```bash
    curl -X GET "https://wft-geo-db.p.rapidapi.com/v1/geo/cities?types=city&namePrefix=San" \
    -H "X-RapidAPI-Key: 0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3" \
    -H "X-RapidAPI-Host: wft-geo-db.p.rapidapi.com"
    
    ```
    
- **Resposta Esperada**:
    
    ```json
    {
      "data": [
        {
          "city": "San Francisco",
          "latitude": 37.77493,
          "longitude": -122.41942
        },
      ]
    }
    
    ```
    

### **2.2. Chamada: Previsão do Tempo**

- **URL do Recurso**:**`https://meteostat.p.rapidapi.com/point/daily`**
- **Método HTTP**:GET
- **Autenticação**:
    - **Header**:
        - **`X-RapidAPI-Key`**: 0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3.
        - **`X-RapidAPI-Host`**: **`meteostat.p.rapidapi.com`**
- **Parâmetros**:
    - **`lat`**: Latitude do ponto geográfico.
    - **`lon`**: Longitude do ponto geográfico.
    - **`start`**: Data de início do período (formato **`YYYY-MM-DD`**).
    - **`end`**: Data de término do período (formato **`YYYY-MM-DD`**).
- **Exemplo de Requisição**:
    
    ```bash
    curl -X GET "https://meteostat.p.rapidapi.com/point/daily?lat=37.77493&lon=-122.41942&start=2023-10-29&end=2023-10-30" \
    -H "X-RapidAPI-Key: 0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3" \
    -H "X-RapidAPI-Host: meteostat.p.rapidapi.com"
    
    ```
    
- **Resposta Esperada**:
    
    ```json
    {
      "data": [
        {
          "tavg": 15.0,
          "tmin": 10.0,
          "tmax": 20.0,
          "prcp": 0.0,
          "wspd": 5.0
        }
      ]
    }
    
    ```
    

---

### **3. Instruções para a Execução de um Teste Operacional da Implementação**

### **Pré-requisitos:**

1. Instalar o Node.js e o Expo CLI.
2. Configurar as chaves da API no objeto **`apiCredentials`**:
    
    ```jsx
    const apiCredentials = {
      meteostat: { key: "0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3", 
      host: "meteostat.p.rapidapi.com" },
      geoDB: { key: "0c6eaa4026msh310d8c145e29a91p1fa6b6jsn3e580de12cc3",
      host: "wft-geo-db.p.rapidapi.com" 
      },
    };
    
    ```
    
3. Garantir conectividade com a internet.

### **Passos para Testar:**

1. **Instalar Dependências**: No diretório do projeto, execute:
    
    ```bash
    npm install
    
    ```
    
2. **Executar o Projeto**: Execute o comando:
    
    ```bash
    expo start
    
    ```
    
3. **Testar Funcionalidade**:
    - Na interface do aplicativo, busque por uma cidade inserindo ao menos três caracteres no campo de pesquisa.
    - Selecione a cidade desejada e clique no botão "Ver Previsão".
    - A previsão do tempo será exibida na tela.
4. **Validar Logs**:
    - Em caso de erro, confira os logs do console para mensagens como "Erro na chamada da API".

### Apresentação

Segue o link da apresentação: <https://youtu.be/__QWlU0fiuw>


