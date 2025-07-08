# AI Stock Analyst: Alternativa Privada e Local ao Manus.

<p align="center">
<img align="center" src="./media/ai-stock-analyst_logo.png" width="300" height="300" alt="AI Stock Analyst Logo">
<p>

    English | [中文](./README_CHS.md) | [繁體中文](./README_CHT.md) | [Français](./README_FR.md) | [日本語](./README_JP.md) | [Português (Brasil)](./README_PTBR.md)

*Uma **alternativa 100% local ao Manus AI**, este assistente de voz com IA navega autonomamente na web, escreve código e planeja tarefas mantendo todos os dados no seu dispositivo. Feito para modelos de raciocínio locais, roda inteiramente no seu hardware, garantindo total privacidade e zero dependência da nuvem.*

[![Visite AI Stock Analyst](https://img.shields.io/static/v1?label=Website&message=AI%20Stock%20Analyst&color=blue&style=flat-square)](#) ![Licença](https://img.shields.io/badge/license-GPL--3.0-green) [![GitHub stars](https://img.shields.io/github/stars/ServOps117/agenticSeek?style=social)](https://github.com/ServOps117/agenticSeek/stargazers)

### Por que AI Stock Analyst?

* 🔒 Totalmente Local & Privado - Tudo roda na sua máquina — sem nuvem, sem compartilhamento de dados. Seus arquivos, conversas e buscas permanecem privados.

* 🌐 Navegação Inteligente na Web - O AI Stock Analyst pode navegar na internet sozinho — pesquisar, ler, extrair informações, preencher formulários — tudo sem as mãos.

* 💻 Assistente Autônomo de Programação - Precisa de código? Ele pode escrever, depurar e executar programas em Python, C, Go, Java e mais — tudo sem supervisão.

* 🧠 Seleção Inteligente de Agentes - Você pede, ele escolhe automaticamente o melhor agente para a tarefa. Como ter uma equipe de especialistas pronta para ajudar.

* 📋 Planeja & Executa Tarefas Complexas - De planejamento de viagens a projetos complexos — pode dividir grandes tarefas em etapas e concluí-las usando múltiplos agentes de IA.

* 🎙️ Ativado por Voz - Voz limpa, rápida e futurista, além de reconhecimento de fala, permitindo que você converse como se fosse sua IA pessoal de um filme de ficção científica. (Em desenvolvimento)

### **Demo**

> *Você pode pesquisar sobre o projeto AI Stock Analyst, aprender quais habilidades são necessárias, depois abrir o CV_candidates.zip e então me dizer quais combinam melhor com o projeto?*

https://github.com/user-attachments/assets/b8ca60e9-7b3b-4533-840e-08f9ac426316

Aviso: Esta demonstração, incluindo todos os arquivos que aparecem (ex: CV_candidates.zip), são totalmente fictícios. Não somos uma corporação, buscamos colaboradores open-source, não candidatos.

> 🛠⚠️️ **Trabalho Ativo em Progresso**

> 🙏 Este projeto começou como um projeto paralelo e não tem roteiro nem financiamento. Cresceu muito além do esperado ao aparecer no GitHub Trending. Contribuições, feedback e paciência são profundamente apreciados.

## Pré-requisitos

Certifique-se de ter chrome driver, docker e python3.10 instalados.

Para problemas relacionados ao chrome driver, veja a seção **Chromedriver**.

### 1. **Clone o repositório e configure**

```sh
git clone https://github.com/ServOps117/agenticSeek.git
cd agenticSeek
mv .env.example .env
```

### 2. Altere o conteúdo do arquivo .env

```sh
SEARXNG_BASE_URL="http://127.0.0.1:8080"
REDIS_BASE_URL="redis://redis:6379/0"
WORK_DIR="/Users/mlg/Documents/workspace_for_ai"
OLLAMA_PORT="11434"
LM_STUDIO_PORT="1234"
CUSTOM_ADDITIONAL_LLM_PORT="11435"
OPENAI_API_KEY='opcional'
DEEPSEEK_API_KEY='opcional'
OPENROUTER_API_KEY='opcional'
TOGETHER_API_KEY='opcional'
GOOGLE_API_KEY='opcional'
ANTHROPIC_API_KEY='opcional'
```

**As chaves de API são totalmente opcionais para quem optar por rodar LLM localmente. Que é o objetivo principal deste projeto. Deixe em branco se você tiver hardware suficiente**

As seguintes variáveis de ambiente configuram as conexões e chaves de API do seu aplicativo.

Atualize o arquivo `.env` com seus próprios valores conforme necessário:

- **SEARXNG_BASE_URL**: Deixe inalterado
- **REDIS_BASE_URL**: Deixe inalterado
- **WORK_DIR**: Caminho para seu diretório de trabalho local. O AI Stock Analyst poderá ler e interagir com esses arquivos.
- **OLLAMA_PORT**: Porta para o serviço Ollama.
- **LM_STUDIO_PORT**: Porta para o serviço LM Studio.
- **CUSTOM_ADDITIONAL_LLM_PORT**: Porta para qualquer serviço LLM adicional.

Todas as variáveis de ambiente de chave de API abaixo são **opcionais**. Só forneça se for usar APIs externas em vez de rodar LLMs localmente.

### 3. **Inicie o Docker**

Certifique-se de que o Docker está instalado e rodando no seu sistema. Você pode iniciar o Docker com os seguintes comandos:

- **No Linux/macOS:**  
        Abra um terminal e execute:
        ```sh
        sudo systemctl start docker
        ```
        Ou inicie o Docker Desktop pelo menu de aplicativos, se instalado.

- **No Windows:**  
        Inicie o Docker Desktop pelo menu Iniciar.

Você pode verificar se o Docker está rodando executando:
```sh
docker info
```
Se aparecerem informações sobre sua instalação do Docker, está funcionando corretamente.

---

## Configuração para rodar LLM localmente na sua máquina

**Requisitos de Hardware:**

Para rodar LLMs localmente, você precisará de hardware suficiente. No mínimo, uma GPU capaz de rodar Qwen/Deepseek 14B é necessária. Veja o FAQ para recomendações detalhadas de modelo/desempenho.

**Configure seu provedor local**

Inicie seu provedor local, por exemplo com ollama:

```sh
ollama serve
```

Veja abaixo a lista de provedores locais suportados.

**Atualize o config.ini**

Altere o arquivo config.ini para definir o provider_name para um provedor suportado e provider_model para um LLM suportado pelo seu provedor. Recomendamos modelos de raciocínio como *Qwen* ou *Deepseek*.

Veja o **FAQ** no final do README para hardware necessário.

```sh
[MAIN]
is_local = True # Se está rodando localmente ou com provedor remoto.
provider_name = ollama # ou lm-studio, openai, etc.
provider_model = deepseek-r1:14b # escolha um modelo compatível com seu hardware
provider_server_address = 127.0.0.1:11434
agent_name = Jarvis # nome da sua IA
recover_last_session = True # recuperar sessão anterior
save_session = True # lembrar sessão atual
speak = False # texto para fala
listen = False # fala para texto, apenas para CLI, experimental
jarvis_personality = False # usar personalidade "Jarvis" (experimental)
languages = en zh # Lista de idiomas, TTS usará o primeiro da lista
[BROWSER]
headless_browser = True # deixe inalterado a menos que use CLI no host.
stealth_mode = True # Usa selenium indetectável para reduzir detecção do navegador
```

**Aviso**:

- O formato do arquivo `config.ini` não suporta comentários.
Não copie e cole a configuração de exemplo diretamente, pois comentários causarão erros. Em vez disso, modifique manualmente o arquivo `config.ini` com suas configurações desejadas, sem comentários.

- *NÃO* defina provider_name como `openai` se estiver usando LM-studio para rodar LLMs. Use `lm-studio`.

- Alguns provedores (ex: lm-studio) exigem `http://` antes do IP. Exemplo: `http://127.0.0.1:1234`

**Lista de provedores locais**

| Provedor   | Local? | Descrição                                               |
|------------|--------|---------------------------------------------------------|
| ollama     | Sim    | Rode LLMs localmente facilmente usando ollama           |
| lm-studio  | Sim    | Rode LLM localmente com LM studio (`provider_name` = `lm-studio`)|
| openai     | Sim    | Use API compatível com openai (ex: servidor llama.cpp)  |

Próximo passo: [Inicie os serviços e rode o AI Stock Analyst](#Start-services-and-Run)

*Veja a seção **Problemas conhecidos** se tiver problemas*

*Veja a seção **Rodar com uma API** se seu hardware não rodar deepseek localmente*

*Veja a seção **Config** para explicação detalhada do arquivo de configuração.*

---

## Configuração para rodar com uma API

**Rodar com uma API é opcional, veja acima para rodar localmente.**

Defina o provedor desejado no `config.ini`. Veja abaixo a lista de provedores de API.

```sh
[MAIN]
is_local = False
provider_name = google
provider_model = gemini-2.0-flash
provider_server_address = 127.0.0.1:5000 # não importa
```
Aviso: Certifique-se de não haver espaço no final da linha no config.

Exporte sua chave de API: `export <<PROVIDER>>_API_KEY="xxx"`

Exemplo: exportar `TOGETHER_API_KEY="xxxxx"`

**Lista de provedores de API**
    
| Provedor   | Local? | Descrição                                               |
|------------|--------|---------------------------------------------------------|
| openai     | Depende| Use API do ChatGPT  |
| deepseek   | Não    | API Deepseek (não privado)                              |
| huggingface| Não    | API Hugging-Face (não privado)                          |
| togetherAI | Não    | Use API together AI (não privado)                       |
| google     | Não    | Use API google gemini (não privado)                     |

Observe que código/bash pode falhar com gemini, pois ignora nosso prompt de formatação, que é otimizado para deepseek r1. Modelos como gpt-4o também apresentam desempenho ruim com nosso prompt.

Próximo passo: [Inicie os serviços e rode o AI Stock Analyst](#Start-services-and-Run)

*Veja a seção **Problemas conhecidos** se tiver problemas*

*Veja a seção **Config** para explicação detalhada do arquivo de configuração.*

---

## Inicie os serviços e rode

Inicie os serviços necessários. Isso iniciará todos os serviços do docker-compose.yml, incluindo:
        - searxng
        - redis (necessário para searxng)
        - frontend
        - backend (se usar `full`)

```sh
./start_services.sh full # MacOS
start ./start_services.cmd full # Windows
```

**Aviso:** Este passo fará download e carregará todas as imagens Docker, o que pode levar até 30 minutos. Após iniciar os serviços, aguarde até que o serviço backend esteja totalmente rodando (você verá backend: <info> no log) antes de enviar mensagens. O backend pode demorar mais para iniciar.

Acesse `http://localhost:3000/` e você verá a interface web.

**Opcional:** Rode com a interface CLI:

Para rodar com CLI, instale os pacotes no host:

```sh
./install.sh
./install.bat # windows
```

Inicie os serviços:

```sh
./start_services.sh # MacOS
start ./start_services.cmd # Windows
```

Depois execute: `uv run cli.py`

---

## Uso

Certifique-se de que os serviços estão rodando com `./start_services.sh full` e acesse `localhost:3000` para a interface web.

Você também pode usar fala para texto definindo `listen = True` no config. Apenas para modo CLI.

Para sair, basta dizer/digitar `goodbye`.

Exemplos de uso:

> *Faça um jogo da cobrinha em python!*

> *Pesquise na web pelos melhores cafés em Rennes, França, e salve uma lista de três com seus endereços em rennes_cafes.txt.*

> *Escreva um programa Go para calcular o fatorial de um número, salve como factorial.go no seu workspace*

> *Procure na pasta summer_pictures por todos os arquivos JPG, renomeie com a data de hoje e salve a lista dos arquivos renomeados em photos_list.txt*

> *Pesquise online por filmes de ficção científica populares de 2024 e escolha três para assistir hoje à noite. Salve a lista em movie_night.txt.*

> *Pesquise na web pelos últimos artigos de notícias de IA de 2025, selecione três e escreva um script Python para extrair títulos e resumos. Salve o script como news_scraper.py e os resumos em ai_news.txt em /home/projects*

> *Sexta-feira, pesquise na web por uma API gratuita de preços de ações, registre-se com supersuper7434567@gmail.com e escreva um script Python para buscar os preços diários da Tesla usando a API, salvando os resultados em stock_prices.csv*

*Observe que o preenchimento de formulários ainda é experimental e pode falhar.*

Após digitar sua consulta, o AI Stock Analyst alocará o melhor agente para a tarefa.

Como este é um protótipo inicial, o sistema de roteamento de agentes pode não alocar sempre o agente certo para sua consulta.

Portanto, seja explícito no que deseja e como a IA deve proceder. Por exemplo, se quiser que faça uma busca na web, não diga:

`Você conhece alguns bons países para viajar sozinho?`

Em vez disso, peça:

`Faça uma busca na web e descubra quais são os melhores países para viajar sozinho`

---

## **Configuração para rodar o LLM em seu próprio servidor**

Se você tem um computador potente ou servidor, mas quer usar a partir do seu laptop, pode rodar o LLM em um servidor remoto usando nosso servidor LLM customizado.

No seu "servidor" que rodará o modelo de IA, obtenha o endereço IP

```sh
ip a | grep "inet " | grep -v 127.0.0.1 | awk '{print $2}' | cut -d/ -f1 # ip local
curl https://ipinfo.io/ip # ip público
```

Nota: Para Windows ou macOS, use ipconfig ou ifconfig para encontrar o IP.

Clone o repositório e entre na pasta `server/`.

```sh
git clone --depth 1 https://github.com/ServOps117/agenticSeek.git
cd agenticSeek/llm_server/
```

Instale os requisitos específicos do servidor:

```sh
pip3 install -r requirements.txt
```

Rode o script do servidor.

```sh
python3 app.py --provider ollama --port 3333
```

Você pode escolher entre usar `ollama` e `llamacpp` como serviço LLM.

Agora, no seu computador pessoal:

Altere o arquivo `config.ini` para definir `provider_name` como `server` e `provider_model` como `deepseek-r1:xxb`.
Defina `provider_server_address` para o IP da máquina que rodará o modelo.

```sh
[MAIN]
is_local = False
provider_name = server
provider_model = deepseek-r1:70b
provider_server_address = x.x.x.x:3333
```

Próximo passo: [Inicie os serviços e rode o AI Stock Analyst](#Start-services-and-Run)

---

## Fala para Texto

Aviso: fala para texto só funciona no modo CLI no momento.

Atualmente, fala para texto só funciona em inglês.

A funcionalidade de fala para texto está desativada por padrão. Para ativar, defina listen como True no arquivo config.ini:

```
listen = True
```

Quando ativado, o recurso escuta por uma palavra-chave de ativação, que é o nome do agente, antes de processar sua entrada. Você pode personalizar o nome do agente atualizando o valor `agent_name` no *config.ini*:

```
agent_name = Friday
```

Para melhor reconhecimento, recomendamos usar um nome comum em inglês como "John" ou "Emma" como nome do agente.

Quando o transcript começar a aparecer, diga o nome do agente em voz alta para ativá-lo (ex: "Friday").

Fale sua consulta claramente.

Finalize seu pedido com uma frase de confirmação para o sistema prosseguir. Exemplos de frases de confirmação incluem:
```
"do it", "go ahead", "execute", "run", "start", "thanks", "would ya", "please", "okay?", "proceed", "continue", "go on", "do that", "go it", "do you understand?"
```

## Configuração

Exemplo de config:
```
[MAIN]
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:11434
agent_name = Friday
recover_last_session = False
save_session = False
speak = False
listen = False
jarvis_personality = False
languages = en zh
[BROWSER]
headless_browser = False
stealth_mode = False
```

**Explicação**:

- is_local -> Roda o agente localmente (True) ou em servidor remoto (False).

- provider_name -> Provedor a ser usado (um de: `ollama`, `server`, `lm-studio`, `deepseek-api`)

- provider_model -> Modelo usado, ex: deepseek-r1:32b.

- provider_server_address -> Endereço do servidor, ex: 127.0.0.1:11434 para local. Qualquer valor para API não local.

- agent_name -> Nome do agente, ex: Friday. Usado como palavra-chave para TTS.

- recover_last_session -> Retoma da última sessão (True) ou não (False).

- save_session -> Salva dados da sessão (True) ou não (False).

- speak -> Ativa saída de voz (True) ou não (False).

- listen -> Ativa entrada por voz (True) ou não (False).

- jarvis_personality -> Usa personalidade tipo JARVIS (True) ou não (False). Apenas muda o prompt.

- languages -> Lista de idiomas suportados, necessário para o roteador de LLM funcionar corretamente. Evite muitos idiomas ou muito parecidos.

- headless_browser -> Roda navegador sem janela visível (True) ou não (False).

- stealth_mode -> Dificulta detecção de bot. Único contra é instalar manualmente a extensão anticaptcha.

- languages -> Lista de idiomas suportados. Necessário para o sistema de roteamento de agentes. Quanto maior a lista, mais modelos serão baixados.

## Provedores

Tabela de provedores disponíveis:

| Provedor   | Local? | Descrição                                               |
|------------|--------|---------------------------------------------------------|
| ollama     | Sim    | Rode LLMs localmente facilmente usando ollama           |
| server     | Sim    | Hospede o modelo em outra máquina, use localmente       |
| lm-studio  | Sim    | Rode LLM localmente com LM studio (`lm-studio`)         |
| openai     | Depende| Use API do ChatGPT (não privado) ou API compatível      |
| deepseek-api| Não   | API Deepseek (não privado)                              |
| huggingface| Não    | API Hugging-Face (não privado)                          |
| togetherAI | Não    | Use API together AI (não privado)                       |
| google     | Não    | Use API google gemini (não privado)                     |

Para selecionar um provedor, altere o config.ini:

```
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:5000
```
`is_local`: deve ser True para qualquer LLM rodando localmente, senão False.

`provider_name`: Selecione o provedor pelo nome, veja a lista acima.

`provider_model`: Defina o modelo a ser usado pelo agente.

`provider_server_address`: pode ser qualquer valor se não usar o provedor server.

# Problemas conhecidos

## Problemas com Chromedriver

**Erro conhecido #1:** *chromedriver incompatível*

`Exception: Failed to initialize browser: Message: session not created: This version of ChromeDriver only supports Chrome version 113
Current browser version is 134.0.6998.89 with binary path`

Isso ocorre se houver incompatibilidade entre seu navegador e a versão do chromedriver.

Você precisa baixar a versão mais recente:

https://developer.chrome.com/docs/chromedriver/downloads

Se estiver usando Chrome versão 115 ou superior, acesse:

https://googlechromelabs.github.io/chrome-for-testing/

E baixe o chromedriver correspondente ao seu sistema operacional.

![alt text](./media/chromedriver_readme.png)

Se esta seção estiver incompleta, abra uma issue.

## Problemas de adaptadores de conexão

```
Exception: Provider lm-studio failed: HTTP request failed: No connection adapters were found for '127.0.0.1:11434/v1/chat/completions'
```

Certifique-se de ter `http://` antes do IP do provedor:

`provider_server_address = http://127.0.0.1:11434`

## SearxNG base URL deve ser fornecida

```
raise ValueError("SearxNG base URL must be provided either as an argument or via the SEARXNG_BASE_URL environment variable.")
ValueError: SearxNG base URL must be provided either as an argument or via the SEARXNG_BASE_URL environment variable.
```

Talvez você não tenha movido `.env.example` para `.env`? Você também pode exportar SEARXNG_BASE_URL:

`export  SEARXNG_BASE_URL="http://127.0.0.1:8080"`

## FAQ

**P: Que hardware eu preciso?**  

| Tamanho do Modelo | GPU         | Comentário                                               |
|-------------------|-------------|---------------------------------------------------------|
| 7B                | 8GB Vram    | ⚠️ Não recomendado. Desempenho ruim, alucinações frequentes, agentes de planejamento podem falhar. |
| 14B               | 12 GB VRAM (ex: RTX 3060) | ✅ Usável para tarefas simples. Pode ter dificuldades com navegação web e planejamento. |
| 32B               | 24+ GB VRAM (ex: RTX 4090) | 🚀 Sucesso na maioria das tarefas, pode ainda ter dificuldades com planejamento |
| 70B+              | 48+ GB Vram (ex: mac studio) | 💪 Excelente. Recomendado para uso avançado. |

**P: Por que Deepseek R1 em vez de outros modelos?**  

Deepseek R1 se destaca em raciocínio e uso de ferramentas para seu tamanho. Achamos que é uma ótima escolha para nossas necessidades, outros modelos funcionam bem, mas Deepseek é nossa principal escolha.

**P: Recebo erro ao rodar `cli.py`. O que faço?**  

Certifique-se de que o local está rodando (`ollama serve`), seu `config.ini` corresponde ao provedor e as dependências estão instaladas. Se nada funcionar, abra uma issue.

**P: Pode rodar 100% localmente mesmo?**  

Sim, com Ollama, lm-studio ou provedores server, todo o reconhecimento de fala, LLM e TTS rodam localmente. Opções não locais (OpenAI ou outras APIs) são opcionais.

**P: Por que usar AI Stock Analyst se já tenho Manus?**

Começou como um projeto paralelo por interesse em agentes de IA. O diferencial é usar modelos locais e evitar APIs.
Nos inspiramos em Jarvis e Friday (filmes do Homem de Ferro) para torná-lo "legal", mas funcionalmente nos inspiramos mais no Manus, pois é isso que as pessoas querem: uma alternativa local ao Manus.
Ao contrário do Manus, o AI Stock Analyst prioriza independência de sistemas externos, dando mais controle, privacidade e evitando custos de API.

## Contribua

Procuramos desenvolvedores para melhorar o AI Stock Analyst! Veja as issues abertas ou discussões.

[Guia de contribuição](./docs/CONTRIBUTING.md)

[![Star History Chart](https://api.star-history.com/svg?repos=Fosowl/ai-stock-analyst&type=Date)](https://www.star-history.com/#Fosowl/ai-stock-analyst&Date)

## Mantenedores:

 > [Fosowl](https://github.com/Fosowl) | Horário de Paris 

 > [antoineVIVIES](https://github.com/antoineVIVIES) | Horário de Taipei 

 > [steveh8758](https://github.com/steveh8758) | Horário de Taipei 

## Agradecimentos Especiais:

 > [tcsenpai](https://github.com/tcsenpai) e [plitc](https://github.com/plitc) pela ajuda na dockerização do backend

