
# Cliente de Conversão de Voz em Tempo Real para RVC (v.1.5.3.13)

[English](/tutorials/tutorial_rvc_en_latest.md) [Korean/한국어](/tutorials/tutorial_rvc_ko_latest.md)

## Introdução

Este aplicativo é um software cliente para realizar conversão de voz em tempo real usando várias IAs de conversão de voz (VC - Voice Conversion). Ele suporta modelos como RVC, MMVCv13, MMVCv15, So-vits-svcv40, entre outros. Este documento foca na [RVC (Retrieval-based-Voice-Conversion)](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI) como exemplo para o tutorial de conversão de voz. As operações básicas são similares para todos os modelos.

A seguir, nos referiremos ao [Retrieval-based-Voice-Conversion-WebUI](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI) como RVC original e ao [RVC-WebUI](https://github.com/ddPn08/rvc-webui) criado por ddPn08 como ddPn08RVC.

## Observações Importantes

- O treinamento de modelos deve ser feito separadamente.
  - Se você deseja treinar seu próprio modelo, consulte o [RVC original](https://github.com/liujing04/Retrieval-based-Voice-Conversion-WebUI) ou o [ddPn08RVC](https://github.com/ddPn08/rvc-webui).
  - Para gravar áudio diretamente no navegador, utilize o [Aplicativo de Gravação no Github Pages](https://w-okada.github.io/voice-changer/).
    - [Vídeo Explicativo](https://youtu.be/s_GirFEGvaA)
  - Consulte as [Dicas para Treinamento](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/docs/training_tips_ja.md) para mais informações.

## Passos para Inicialização

### Versão para Windows

Descompacte o arquivo ZIP baixado e execute o `start_http.bat`.

Se você tiver uma versão anterior, certifique-se de descompactá-la em uma pasta separada.

### Versão para Mac

O processo de inicialização é o seguinte:

1. Descompacte o arquivo baixado.
2. Execute o **MMVCServerSIO** pressionando a tecla de controle enquanto clica (ou clique com o botão direito). Se aparecer uma mensagem indicando que o desenvolvedor não pode ser verificado, repita o processo. O terminal será aberto e o processo será concluído em alguns segundos.
3. Execute o **startHTTP.command** pressionando a tecla de controle enquanto clica (ou clique com o botão direito). Se a mensagem de verificação do desenvolvedor aparecer novamente, repita o procedimento. O terminal será aberto e o processo de inicialização começará.

**Nota**: Certifique-se de executar o **MMVCServerSIO** antes do **startHTTP.command**.

Se você tiver uma versão anterior, descompacte-a em uma pasta separada.

### Atenção ao Conectar-se Remotamente

Quando conectar-se remotamente, utilize o arquivo `.bat` (Windows) ou `.command` (Mac) onde o `http` foi substituído por `https`.

A interface será exibida em um navegador (apenas Chrome é suportado).

### Console

Ao executar o arquivo `.bat` (Windows) ou `.command` (Mac), uma tela semelhante à seguinte será exibida, e diversos dados serão baixados da internet na primeira inicialização. Dependendo do ambiente, pode levar entre 1 a 2 minutos.

![image](https://github.com/w-okada/voice-changer/assets/48346627/88a30097-2fb3-4c50-8bf1-19c41f27c481)

### Exibição da Interface Gráfica (GUI)

Após o download dos dados necessários, a seguinte tela será exibida. Se desejar, clique no ícone amarelo para recompensar o desenvolvedor com um café. Clique no botão "Start" para iniciar o processo.

![image](https://github.com/w-okada/voice-changer/assets/48346627/a8d12b5c-d1e8-4ca6-aed0-72cee6bb97c1)

## Exibição da GUI

Se a tela abaixo for exibida, a inicialização foi bem-sucedida.

![image](https://github.com/w-okada/voice-changer/assets/48346627/27add00d-5059-4cbf-a732-9deb6dc309ff)

## Início Rápido

### Como Usar

Após a inicialização, é possível realizar a conversão de voz imediatamente utilizando os dados baixados.

1. Clique na área de seleção de modelos e escolha o modelo desejado. A imagem do personagem associado ao modelo será exibida após o carregamento.
2. Selecione o microfone (entrada) e os alto-falantes (saída) que deseja utilizar. Se você não estiver familiarizado, recomendamos selecionar "client" e, em seguida, escolher seu microfone e alto-falantes. (Explicaremos a diferença entre "client" e "server" mais tarde).
3. Pressione o botão "Start" e, após alguns segundos de carregamento, a conversão de áudio começará. Fale no microfone, e o áudio convertido será reproduzido pelos alto-falantes.

![image](https://github.com/w-okada/voice-changer/assets/48346627/883b296e-e5ca-4571-8fed-dcf7495ebb92)

### Perguntas Frequentes sobre o Início Rápido

**Q1. O áudio está cortando.**

R1. Pode ser que o desempenho do seu PC não seja suficiente. Tente aumentar o valor de CHUNK (na imagem como A) para algo como 1024. Além disso, experimente definir o F0 Det para "dio" (na imagem como B).

![image](https://github.com/w-okada/voice-changer/assets/48346627/3c485d9b-53be-47c1-85d9-8663363b06f9)

**Q2. O áudio não está sendo convertido.**

R2. Consulte [aqui](https://github.com/w-okada/voice-changer/blob/master/tutorials/trouble_shoot_communication_ja.md) para identificar e resolver o problema.

**Q3. O tom da voz está incorreto.**

R3. Embora não explicado no início rápido, se o modelo suportar alteração de tom, você pode ajustá-lo com o controle "TUNE". Consulte as explicações detalhadas abaixo.

**Q4. A janela não está aparecendo ou seu conteúdo não está sendo exibido. O console mostra um erro como `ERR_CONNECTION_REFUSED`.**

R4. É possível que o antivírus esteja bloqueando. Aguarde ou exclua a pasta das verificações do antivírus, por sua conta e risco.

**Q5. O erro `[4716:0429/213736.103:ERROR:gpu_init.cc(523)] Passthrough is not supported` está aparecendo.**

R5. Este é um erro da biblioteca usada, mas não afeta o funcionamento. Pode ser ignorado.

**Q6. Minha GPU AMD não está sendo utilizada.**

R6. Use a versão DirectML. As GPUs AMD são habilitadas apenas para modelos ONNX. Verifique o uso da GPU no Monitor de Desempenho.

**Q7. O onxxruntime não está iniciando e exibe um erro.**

R7. O erro ocorre quando o caminho da pasta contém caracteres Unicode. Extraia o arquivo para um local sem Unicode (somente caracteres alfanuméricos).
