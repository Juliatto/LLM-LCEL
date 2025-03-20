### Projeto README - LangChain Translator

#### Índice

1. **Descrição**
2. **Instalação**
3. **Uso**
4. **Blocos de Código**
   - 4.1 Importação das Bibliotecas
   - 4.2 Carregamento das Variáveis de Ambiente
   - 4.3 Criação do Modelo Groq
   - 4.4 Parser de Saída
   - 4.5 Prompt Template
   - 4.6 Execução da Cadeia (Chain)
5. **Glossário**
6. **Contribuições**
7. **Licença**

---

#### Descrição

Este projeto utiliza o LangChain para traduzir frases para diferentes idiomas utilizando um modelo específico do Groq. Ele é configurado para carregar variáveis de ambiente e utilizar uma API key para acesso ao serviço de tradução.

---

#### Instalação

Para utilizar este projeto localmente, siga os passos abaixo:

1. Clone o repositório:
   ```
   git clone https://github.com/seu-usuario/nome-do-repositorio.git
   cd nome-do-repositorio
   ```

2. Instale as dependências do projeto:
   ```
   pip install -r requirements.txt
   ```

---

#### Uso

Para executar o projeto, certifique-se de ter configurado corretamente as variáveis de ambiente com sua API key do Groq. Execute o script Python conforme necessário para traduzir frases de um idioma para outro.

---

#### Blocos de Código

##### 4.1 Importação das Bibliotecas

```python
from langchain_core.messages import HumanMessage, SystemMessage
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_groq import ChatGroq
from dotenv import load_dotenv, find_dotenv
import os
```

Este bloco importa todas as bibliotecas necessárias para o funcionamento do projeto, incluindo as partes essenciais do LangChain e o dotenv para carregar variáveis de ambiente.

##### 4.2 Carregamento das Variáveis de Ambiente

```python
load_dotenv(find_dotenv())
groq_api_key = os.getenv("GROQ_API_KEY")
```

Aqui, as variáveis de ambiente são carregadas, incluindo a chave de API do Groq, que é necessária para autenticação.

##### 4.3 Criação do Modelo Groq

```python
llm = ChatGroq(
    model="Gemma2-9b-It",  # Modelo de LLM utilizado
    groq_api_key=groq_api_key,  # Chave de API do Groq
)
```

Este trecho cria uma instância do modelo de LLM do Groq para realizar a tradução.

##### 4.4 Parser de Saída

```python
parser = StrOutputParser()
```

O parser de saída é utilizado para interpretar a saída do modelo LLM e formatá-la de acordo com as necessidades do sistema.

##### 4.5 Prompt Template

```python
generic_template = "Translate the following sentence into {language}"

prompt = ChatPromptTemplate.from_messages(
    [
        ("system", generic_template),
        ("user", "{text}")
    ]
)
```

O prompt template define o formato da interação com o usuário, indicando como o sistema solicita e recebe frases para tradução.

##### 4.6 Execução da Cadeia (Chain)

```python
chain = prompt | llm | parser

print(chain.invoke({'language': 'German', 'text': 'hello' }))
```

Neste bloco, a cadeia de execução (chain) é montada, combinando o template do prompt, o modelo de LLM e o parser de saída para realizar a tradução de uma frase específica.

---

#### Glossário

- **LLM**: Linguistic Language Model, modelo de linguagem que realiza tarefas como tradução de texto.
- **Groq**: Plataforma ou serviço que provê modelos de LLM para diferentes aplicações.
- **Parser de Saída**: Componente que interpreta e formata a saída do modelo de LLM para uso pelo sistema.
- **Prompt Template**: Estrutura que define como o sistema interage com o usuário para coletar informações.

---

#### Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para reportar problemas, sugerir melhorias ou fazer pull requests diretamente no repositório.

---

#### Licença

