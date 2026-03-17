# Projeto_integracao_com_ia

# Assistente de Voz com Whisper, ChatGPT e gTTS no Google Colab 🎙️🤖

Este projeto é um assistente de voz interativo desenvolvido em Python para ser executado diretamente no Google Colab. Ele capta o áudio do usuário pelo microfone do navegador, transcreve a fala em texto, processa uma resposta inteligente utilizando a inteligência artificial da OpenAI e retorna a resposta em formato de áudio.

O código também inclui uma base de dados simulada (um dicionário) de uma loja de eletrônicos, servindo como base para a criação de um bot de atendimento de estoque.

## 🚀 Funcionalidades

* **Gravação de Áudio via Web:** Utiliza JavaScript injetado no Colab para acessar o microfone do usuário e gravar comandos de voz.
* **Reconhecimento de Fala (ASR):** Transcreve o áudio gravado para texto utilizando o modelo `Whisper` da OpenAI.
* **Processamento de Linguagem Natural (NLP):** Envia a transcrição para a API do `ChatGPT` (modelo `gpt-3.5-turbo`) para gerar respostas contextuais.
* **Síntese de Voz (TTS):** Converte o texto de resposta do ChatGPT de volta em áudio usando a biblioteca `gTTS` (Google Text-to-Speech) e reproduz automaticamente no Colab.

## 🛠️ Tecnologias e Bibliotecas Utilizadas

* **Python 3**
* **Google Colab** (Bibliotecas `google.colab` e `IPython.display`)
* **JavaScript** (API `MediaRecorder` para captura de áudio no browser)
* **[OpenAI Whisper](https://github.com/openai/whisper):** Para transcrição de áudio.
* **[OpenAI API](https://pypi.org/project/openai/):** Para comunicação com o modelo LLM do ChatGPT.
* **[gTTS](https://pypi.org/project/gTTS/):** Para a síntese de texto em fala.

## ⚙️ Como Executar o Projeto

Como o script depende de interações específicas com a interface web para acesso ao microfone, **ele deve ser executado no Google Colab**.

1.  **Abra o Google Colab:** Crie um novo notebook ou importe este arquivo `.ipynb`.
2.  **Instale as dependências:**
    Execute a seguinte célula para instalar os pacotes necessários:
    ```bash
    !pip install git+[https://github.com/openai/whisper.git](https://github.com/openai/whisper.git) -q
    !pip install openai gTTS
    ```
3.  **Configuração da Chave da API:**
    No código principal, localize a variável `api_key` e insira sua chave da OpenAI. Se você deixar a string vazia (`""`), o programa pedirá que você digite a chave durante a execução.
4.  **Execute o fluxo principal:**
    Rode a célula que contém o loop de execução (`while True:`).
5.  **Interação:**
    * Digite `1` quando o prompt solicitar.
    * Autorize o uso do microfone no seu navegador.
    * Fale por até 15 segundos.
    * Aguarde o processamento e ouça a resposta gerada pela IA!

## 📁 Estrutura do Código

O script principal está dividido nas seguintes funções:
* `record(sec)`: Aciona o JavaScript para gravar o áudio e salva como `.wav`.
* `whisper_traducao(arquivo_de_voz)`: Carrega o modelo Whisper e retorna o texto falado.
* `chatgpt_response(chave_api, trascription)`: Comunica-se com a OpenAI para gerar a resposta baseada na transcrição.
* `gtss_response(definition_response)`: Transforma a string de resposta em um novo arquivo `.wav` e o reproduz.
* `estoque_solucao(estoque, x)`: Função orquestradora que une todas as etapas em um fluxo contínuo.

## 📌 Próximos Passos (To-Do)

* Integrar o dicionário `estoque_loja` ao *System Prompt* do ChatGPT para que ele atue como um vendedor da loja, respondendo sobre preços e disponibilidade dos produtos listados.
* Implementar tratamento de erros para problemas de conexão com a API da OpenAI ou áudios vazios.
