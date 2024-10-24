Aqui está a tradução e formatação ajustada para a documentação no GitHub em português:

---

# Cliente VC

[Japanese](/README_ja.md) [Korean](/README_ko.md) [Russian](/README_ru.md)

## Novidades!
- Lançamos um produto irmão, o cliente de Texto para Fala.
  - Você pode gerar voz com uma interface simples.
  - Para mais detalhes, clique [aqui](https://github.com/w-okada/ttsclient).
- Código de Treinamento Beatrice V2 Liberado!!!
  - [Repositório de Código de Treinamento](https://huggingface.co/fierce-cats/beatrice-trainer)
  - [Versão Colab](https://github.com/w-okada/beatrice-trainer-colab)
- v.2.0.65-beta
  - [AQUI](https://github.com/w-okada/voice-changer/tree/v.2)
  - nova funcionalidade: Suporte ao Beatrice v2 beta.1, possibilitando uma conversão de voz de qualidade ainda maior.
- v.2.0.61-alpha
  - [AQUI](https://github.com/w-okada/voice-changer/tree/v.2)
  - Funcionalidade:
    - Agora é possível especificar a duração do crossfade.
  - Correção:
    - Corrigido um problema em que os elementos não utilizados de um modelo ainda afetavam o desempenho durante a mesclagem, definindo seus valores como zero.
- v.2.0.60-alpha
  - Funcionalidade:
    - [Modo escuro](https://github.com/w-okada/voice-changer/issues/1306)
    - [Reintrodução do pytorch rmvpe](https://github.com/w-okada/voice-changer/issues/1319)
    - [Seleção de Modo Exclusivo WASAPI](https://github.com/w-okada/voice-changer/issues/1305)
- v.2.0.58-alpha
  - [AQUI](https://github.com/w-okada/voice-changer/tree/v.2)
  - Funcionalidade:
    - Transmissão SIO
    - ngrok embutido (experimental)
  - Melhorias:
    - Ajustes para celulares.
  - Correção:
    - Texto corrompido em mensagens CUI no macOS.
- v.2.0.55-alpha
  - [AQUI](https://github.com/w-okada/voice-changer/tree/v.2)
  - Melhorias:
    - Redução da carga de CPU no RVC
    - Suporte para WebSocket
  - Alteração:
    - Ativação da opção `no_cui` no batch de inicialização.

# O que é o Cliente VC?

1. Este é um software cliente para realizar conversão de voz em tempo real usando diversas IAs de Conversão de Voz (VC). As IAs suportadas para conversão de voz são as seguintes:

- [MMVC](https://github.com/isletennos/MMVC_Trainer) (somente v1)
- [so-vits-svc](https://github.com/svc-develop-team/so-vits-svc) (somente v1)
- [RVC (Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI)
- [DDSP-SVC](https://github.com/yxlllc/DDSP-SVC) (somente v1)
- [Beatrice JVS Corpus Edition](https://prj-beatrice.com/) * experimental, (***Licença NÃO MIT***) veja [readme](https://github.com/w-okada/voice-changer/blob/master/server/voice_changer/Beatrice/) * Apenas para Windows, dependente de CPU (somente v1)
  - [Beatrice v2](https://prj-beatrice.com/) (somente para v2)

2. Distribuir a carga executando o Voice Changer em outro PC
   O conversor de voz em tempo real deste aplicativo funciona em uma configuração cliente-servidor. Executando o servidor MMVC em um PC separado, você pode utilizá-lo minimizando o impacto em outros processos que exigem muitos recursos, como jogos.

![image](https://user-images.githubusercontent.com/48346627/206640768-53f6052d-0a96-403b-a06c-6714a0b7471d.png)

3. Compatibilidade multiplataforma
   Suporta Windows, Mac (incluindo Apple Silicon M1), Linux e Google Colaboratory.

## Softwares Relacionados
- [Real-time Voice Changer VCClient](https://github.com/w-okada/voice-changer)
- [Software de Texto-para-Fala TTSClient](https://github.com/w-okada/ttsclient)
- [Software de Reconhecimento de Voz em Tempo Real ASRClient](https://github.com/w-okada/asrclient)

# Como Usar

Este é um aplicativo para realizar mudanças de voz com MMVC e so-vits-svc.

Ele pode ser usado de duas maneiras principais, em ordem de dificuldade:

- Usando um binário pré-construído
- Configurando um ambiente com Docker ou Anaconda e usando-o

## (1) Uso com binários pré-construídos

- Você pode baixar e executar binários executáveis.

- Consulte [aqui](tutorials/tutorial_rvc_en_latest.md) para o tutorial. ([solução de problemas](https://github.com/w-okada/voice-changer/blob/master/tutorials/trouble_shoot_communication_ja.md))

- Agora é fácil testá-lo no [Google Colaboratory](https://github.com/w-okada/voice-changer/tree/v.2/w_okada's_Voice_Changer_version_2_x.ipynb) (é necessária uma conta ngrok). Você pode iniciá-lo a partir do botão 'Open in Colab' no canto superior esquerdo.

<img src="https://github.com/w-okada/voice-changer/assets/48346627/3f092e2d-6834-42f6-bbfd-7d389111604e" width="400" height="150">

- Oferecemos versões para Windows e Mac no [Hugging Face](https://huggingface.co/wok000/vcclient000/tree/main)
- **v2 para Windows**
  - Baixe e utilize `vcclient_win_std_xxx.zip`. Você pode realizar a conversão de voz utilizando um processador de alto desempenho sem uma GPU ou utilizando DirectML para aproveitar GPUs (AMD, Nvidia). A versão v2 suporta tanto torch quanto onnx.
  - Se você tiver uma GPU Nvidia, pode alcançar uma conversão de voz mais rápida utilizando `vcclient_win_cuda_xxx.zip`.
- **v2 para Mac (Apple Silicon)**
  - Baixe e utilize `vcclient_mac_xxx.zip`.
- **v1**
  - Se você estiver usando Windows com GPU Nvidia, baixe ONNX (cpu, cuda) ou PyTorch (cpu, cuda).
  - Se você estiver usando Windows com GPU AMD/Intel, baixe ONNX (cpu, DirectML) e PyTorch (cpu, cuda). As GPUs AMD/Intel são ativadas apenas para modelos ONNX.
  - Em ambos os casos, o suporte a GPU só é ativado se suportado pelo PyTorch e Onnxruntime.
  - Se você não estiver usando uma GPU no Windows, baixe ONNX (cpu, cuda) e PyTorch (cpu, cuda).

- Para usuários do Windows, após descompactar o arquivo zip baixado, execute o arquivo `start_http.bat` correspondente ao seu VC.

- Para usuários do Mac, após descompactar o arquivo baixado, clique duas vezes no arquivo `startHttp.command` correspondente ao seu VC. Se uma mensagem indicando que o desenvolvedor não pode ser verificado for exibida, pressione a tecla de controle e clique para executá-lo novamente (ou clique com o botão direito para executar).

- Se você estiver conectando-se remotamente, utilize o arquivo `.command` (Mac) ou `.bat` (Windows) com HTTPS em vez de HTTP.

- O codificador do DDSP-SVC suporta apenas hubert-soft.

- [Baixe no Hugging Face](https://huggingface.co/wok000/vcclient000/tree/main)

## (2) Uso após configurar o ambiente com Docker ou Anaconda

Clone este repositório e use-o. Configurar o WSL2 é essencial para Windows. Além disso, é necessário configurar ambientes virtuais como Docker ou Anaconda no WSL2. No Mac, é necessário configurar ambientes virtuais Python, como o Anaconda. Embora seja necessária preparação, esse método oferece o melhor desempenho em vários ambientes. **<font color="red"> Mesmo sem uma GPU, ele pode funcionar bem com uma CPU relativamente nova </font>(consulte a seção sobre desempenho em tempo real abaixo).**

[Vídeo explicativo sobre a instalação do WSL2 e Docker](https://youtu.be/POo_Cg0eFMU)

[Vídeo explicativo sobre a instalação do WSL2 e Anaconda](https://youtu.be/fba9Zhsukqw)

Para executar o Docker, veja [iniciar docker](docker_vcclient/README_en.md).

Para executar no Anaconda venv, veja [guia do desenvolvedor](README_dev_en.md).

Para executar no Linux usando uma GPU AMD, veja [guia de configuração no Linux](tutorials/tutorial_anaconda_amd_rocm.md).

# Assinatura do Software

Este software não é assinado pelo desenvolvedor. Uma mensagem de aviso aparecerá,
