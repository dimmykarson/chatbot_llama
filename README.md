
# Chatbot RAG com Modelo LLaMA e Chroma Vector Store

Este projeto implementa um chatbot que utiliza a técnica de **RAG (Retrieval-Augmented Generation)** para fornecer respostas baseadas em dados contextuais armazenados localmente. Ele usa o modelo **LLaMA 3.2-3B-Instruct**, fornecido pela Hugging Face, para geração de respostas, juntamente com a biblioteca **LangChain** para realizar buscas semânticas através de uma loja de vetores (**Chroma Vector Store**).

## Descrição Geral

O RAG combina a recuperação de informações relevantes com a geração de respostas, oferecendo mais precisão e atualidade nas respostas fornecidas pelo chatbot. O modelo LLaMA foi escolhido por ser eficiente e open-source, enquanto o Chroma é usado para armazenar e recuperar vetores (representações semânticas) de documentos. 

Os documentos são carregados de arquivos PDF, processados e divididos em fragmentos menores para otimizar as buscas e garantir que o modelo LLM consiga processá-los adequadamente.

## Estrutura do Projeto

- **Modelo de linguagem**: LLaMA 3.2-3B-Instruct, hospedado no Hugging Face.
- **Loja de vetores**: Chroma Vector Store para busca semântica eficiente.
- **Embedding**: `thuan9889/llama_embedding_model_v1`, para gerar vetores de documentos. Você pode ajustar esse modelo para outro, como [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) igualmente eficiente. Ou pode buscar um proprietário, como o da OpenAI.
- **Documentos**: Arquivos PDF que são processados e armazenados na loja de vetores após serem convertidos em representações vetoriais.
- **Prompt personalizado**: Um prompt empático e focado em fornecer respostas sobre autismo com precisão e concisão.

## Como o RAG Funciona

1. **Recuperação (Retrieval)**: O sistema busca informações relevantes de uma base de dados (vector store) quando uma pergunta é feita.
2. **Geração (Generation)**: O modelo LLaMA então utiliza essas informações recuperadas para gerar uma resposta contextualizada.

## Dependências

Este projeto utiliza as seguintes bibliotecas e ferramentas:

- **LangChain**: Para estruturar cadeias de conversação e realizar buscas semânticas.
- **Chroma Vector Store**: Para armazenar e buscar representações vetoriais de documentos.
- **Hugging Face**: Para acessar o modelo de linguagem LLaMA e embeddings.
- **PyPDFLoader**: Para carregar e processar documentos PDF.
- **SQLite**: Para gerenciamento de banco de dados no Chroma.

### Configuração do Token da API do Hugging Face

Para acessar os modelos hospedados na Hugging Face, é necessário ter uma chave de API válida. Siga os passos abaixo para configurar corretamente o projeto:

1. **Obtenha sua chave de API**:
   - Acesse [Hugging Face](https://huggingface.co/) e faça login na sua conta.
   - Vá até o seu perfil e clique em "Settings" (Configurações).
   - No menu lateral, selecione "Access Tokens" (Tokens de Acesso).
   - Crie ou copie seu token de acesso, que será usado para autenticar suas requisições.

2. **Crie o arquivo `.env`**:
   - Na raiz do seu projeto, crie um arquivo chamado `.env`.
   - Dentro desse arquivo, adicione a seguinte linha, substituindo `your_huggingface_token` pelo token de acesso que você obteve:

   ```bash
   HUGGINGFACEHUB_API_TOKEN=your_huggingface_token



### Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/dimmykarson/chatbot_llama.git
   cd chatbot_llama

2. Instale as dependências:

    ```bash
    pip install -r requirements.txt


3. (Opicional) Se você estiver em um sistema Linux ou MacOS, execute a correção do SQLite:

    ```bash
    __import__('pysqlite3')
    import sys
    sys.modules['sqlite3'] = sys.modules.pop('pysqlite3')


4. Solicite acesso ao modelo LLaMA 3.2-3B-Instruct na Hugging Face em: [Hugging Face](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct) - Importante: pode levar algumas horas para ser liberado.

5. Certifique-se de ter os documentos PDF para serem processados, armazenados na pasta files


### Como Usar

1. Carregue os documentos PDF para o chatbot processar:

    ```bash
    pages = []
    for path in files:
        loader = PyPDFLoader(os.path.join(dir, path))
        pages.extend(loader.load())

2. Crie os embeddings e armazene os dados no Chroma Vector Store:

    ```bash
    vectordb = Chroma.from_documents(
        documents=documents,
        embedding=embedding_model,
        persist_directory=dir_vector_store
    )


3. Execute o chatbot com o loop de perguntas:

    ```bash
    while True:
        question = input('Pergunta: ')
        if question.upper() in ['SAIR', "Q"]:
            break
        response = chat_chain.invoke({'query': question})
        print("Resposta:", response['result'])


### Considerações Finais

Esse modelo não possui fine-tuning específico para autismo, portanto, as respostas podem ser mais generalizadas. Para melhorar a precisão, seria necessário treinar o modelo com um conjunto de dados especializado.

Sinta-se à vontade para ajustar o projeto conforme necessário, e entre em contato caso tenha dúvidas ou sugestões.

## Licença

Este projeto é licenciado sob a Licença MIT. Isso significa que você pode usar, copiar, modificar, mesclar, publicar, distribuir, sublicenciar e/ou vender cópias do software, desde que inclua o aviso de direitos autorais e a permissão da licença em todas as cópias ou partes substanciais do software.

Confira os detalhes da licença abaixo:

MIT License

Copyright (c) 2024 Dimmy Magalhães

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.



