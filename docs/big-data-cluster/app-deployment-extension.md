---
title: Extensão de implantação de aplicativo
titleSuffix: SQL Server big data clusters
description: Implante um script Python ou R como um aplicativo no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (visualização).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 49a59650c406e3b48394da45ad0eeb4589fc4374
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653586"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Como usar Visual Studio Code para implantar aplicativos no[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar aplicativos em um cluster SQL Server Big Data usando o código Microsoft Visual Studio com a extensão de implantação de aplicativo. Essa capacidade foi introduzida no CTP 2.3. 

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server Big data cluster](big-data-cluster-overview.md) CTP 2,3 ou posterior

## <a name="capabilities"></a>Capacidades

Esta extensão dá suporte às seguintes tarefas no Visual Studio Code:

- Autenticar com o cluster de Big Data do SQL Server.
- Recuperar um modelo de aplicativo do repositório do GitHub para implantação dos tempos de execução com suporte.
- Gerenciar modelos de aplicativos abertos no workspace do usuário.
- Implantar um aplicativo por meio de uma especificação no formato YAML.
- Gerenciar aplicativos implantados dentro do cluster de Big Data do SQL Server.
- Exibir todos os aplicativos que você implantou na barra lateral com informações adicionais.
- Gerar uma especificação de execução para consumir ou excluir o aplicativo do cluster.
- Consumir aplicativos implantados por meio de uma especificação de execução em YAML.

As seções a seguir descrevem o processo de instalação e fornecem uma visão geral de como a extensão funciona. 

### <a name="install"></a>Instalar

Primeiro, instale a extensão de implantação de aplicativo no Visual Studio Code:

1. Baixe a [extensão de implantação de aplicativo](https://aka.ms/app-deploy-vscode) para instalar a extensão como parte do Visual Studio Code.

1. Inicie o Visual Studio Code e navegue até a barra lateral extensões.

1. Clique no menu de contexto `…` na parte superior da barra lateral e selecione `Install from vsix`.

   ![Instalar o VSIX](media/vs-extension/install_vsix.png)

1. Localize o arquivo `sqlservbdc-app-deploy.vsix` que você baixou e escolha-o para ser instalado.

Depois que o SQL Server Big Data extensão de implantação do aplicativo de cluster for instalado, ele solicitará que você recarregue Visual Studio Code. Agora você deve ver o Gerenciador de aplicativos do BDC SQL Server na barra lateral Visual Studio Code.

### <a name="app-explorer"></a>Gerenciador de Aplicativos

Clique na extensão na barra lateral para carregar um painel lateral mostrando o Gerenciador de Aplicativos. A seguinte captura de tela de exemplo do Gerenciador de Aplicativos mostra que não há aplicativos nem especificações de aplicativos disponíveis:

![Gerenciador de Aplicativos](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>Conectar ao cluster

Para se conectar ao ponto de extremidade do cluster, use um dos seguintes métodos:

- Clique na barra de status na parte inferior, que diz `SQL Server BDC Disconnected`.
- Ou clique no botão `Connect to Cluster` na parte superior, com a seta apontando para um porta.

Visual Studio Code solicita o ponto de extremidade, o nome de usuário e a senha apropriados.

O ponto de extremidade para se `Cluster Management Service` conectar é o ponto de extremidade com a porta 30080.

Você também pode encontrar esse ponto de extremidade na linha de comando por meio de 

```
azdata bdc endpoint list
```

Uma das outras maneiras de obter essas informações é fazer com que clique com o botão direito do mouse em **gerenciar** no servidor em Azure Data Studio, onde você encontrará os pontos de extremidade dos serviços listados.

![Ponto de extremidade do ADS](media/vs-extension/ads_end_point.png)

Depois de encontrar o ponto de extremidade a ser usado, conecte-se ao cluster.

![Nova Conexão](media/vs-extension/connect_to_cluster.png)

 Se você tiver as credenciais corretas e o ponto de extremidade do aplicativo, Visual Studio Code notifica que você foi conectado ao cluster e verá todos os aplicativos implantados preenchidos na barra lateral. Se você se conectar com êxito, seu ponto de extremidade e nome de usuário serão salvos no `./sqldbc` como parte de seu perfil do usuário. Nenhuma senha ou tokens serão salvos. Ao fazer logon novamente, o prompt será preenchido com o host e o nome de usuário salvos, mas sempre exigirá que você insira uma senha. Se você quiser se conectar a um ponto de extremidade de cluster diferente, basta clicar novamente no `New Connection`. A conexão será fechada automaticamente se você fechar Visual Studio Code ou se você abrir um espaço de trabalho diferente e precisará se reconectar.

### <a name="app-template"></a>Modelo de Aplicativo

Você precisa *abrir o espaço de trabalho* no Visual Studio Code em que irá salvar os artefatos do aplicativo.

Para implantar um novo aplicativo usando um de nossos modelos, clique no botão `New App Template` no painel `App Specifications`, em que será solicitado que você insira o nome, o tempo de execução e em qual localização você gostaria de colocar o novo aplicativo no computador local. O nome e a versão que você fornece devem ser um rótulo de DNS-1035 e devem consistir em caracteres alfanuméricos minúsculos ou '-', começar com um caractere alfabético e terminar com um caractere alfanumérico.

É recomendável colocá-lo em seu espaço de trabalho Visual Studio Code atual para que você possa usar a funcionalidade completa da extensão, mas você pode colocá-lo em qualquer lugar no sistema de arquivos local.

![Novo Modelo de Aplicativo](media/vs-extension/new_app_template.png)

Após a conclusão, um novo modelo de aplicativo é gerado por meio de scaffold para você na localização especificada e a implantação `spec.yaml` é aberta em seu workspace. Se o diretório selecionado estiver em seu workspace, você também deverá vê-lo listado no painel `App Specifications`:

![Modelo de Aplicativo Carregado](media/vs-extension/loading_app_template.png)

O modelo é um aplicativo `helloworld` simples que é apresentado da seguinte maneira no painel especificações do aplicativo:

- **spec.yaml**
   - Instrui o cluster a implantar seu aplicativo
- **run-spec.yaml**
   - Informa ao cluster como você gostaria de chamar seu aplicativo

O código-fonte do aplicativo estaria na pasta do espaço de trabalho.

- **nome do arquivo de origem**
   - Este é seu arquivo de código-fonte, conforme especificado por `src` em `spec.yaml`
   - Ele tem uma função chamada `handler`, que é considerada o `entrypoint` do aplicativo, conforme mostrado em `spec.yaml`. Ele usa uma entrada de cadeia de caracteres chamada `msg` e retorna uma saída de cadeia de caracteres chamada `out`. Elas são especificadas em `inputs` e `outputs` do `spec.yaml`.

Se você não quiser um modelo com scaffold e preferir apenas um `spec.yaml` para implantação de um aplicativo já criado, clique no botão `New Deploy Spec` ao lado do botão `New App Template` e siga o mesmo processo, mas você receberá apenas o `spec.yaml`, que pode modificar como quiser.

### <a name="deploy-app"></a>Implantar o Aplicativo

Você pode implantar esse aplicativo instantaneamente por meio da lente de código `Deploy App` no `spec.yaml` ou pressionar o botão de pasta de raio ao lado do arquivo `spec.yaml` no menu Especificações do Aplicativo. A extensão descompactará todos os arquivos no diretório em que o `spec.yaml` está localizado e implantará seu aplicativo no cluster. 

>[!NOTE]
>Verifique se todos os arquivos do aplicativo estão no mesmo diretório que seu `spec.yaml`. O `spec.yaml` deve estar no nível raiz do diretório do código-fonte do aplicativo. 

![Botão Implantar Aplicativo](media/vs-extension/deploy_app_lightning.png)

![Implantar CodeLens do Aplicativo](media/vs-extension/deploy_app_codelens.png)

Você será notificado quando o aplicativo estiver pronto para consumo com base no estado do aplicativo na barra lateral:

![Aplicativo Implantado](media/vs-extension/app_deploy.png)

![Barra Lateral com Aplicativo Pronto](media/vs-extension/app_ready_side_bar.png)

![Notificação de Aplicativo Pronto](media/vs-extension/app_ready_notification.png)

No painel lateral, você verá o seguinte disponível:

Você poderá exibir todos os aplicativos que implantou na barra lateral com as seguintes informações:

- state
- version
- parâmetros de entrada
- parâmetros de saída
- links
  - swagger
  - details

Se você clicar `Links`em, verá que pode acessar o `swagger.json` de seu aplicativo implantado, para que você possa escrever seus próprios clientes que chamam seu aplicativo:

![Swagger](media/vs-extension/swagger.png)

Confira [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md) para obter mais informações.

### <a name="app-run"></a>Execução do Aplicativo

Quando o aplicativo estiver pronto, chame-o com o `run-spec.yaml` que foi fornecido como parte do modelo de aplicativo:

![Especificação de Execução](media/vs-extension/run_spec.png)

Especifique qualquer cadeia de caracteres que desejar no lugar de `hello` e, em seguida, execute-a novamente por meio do link de lente de código ou do botão de raio na barra lateral, ao lado de `run-spec.yaml`. Se não tiver uma especificação de execução por algum motivo, gere uma do aplicativo implantado no cluster:

![Obter Especificação de Execução](media/vs-extension/get_run_spec.png)

Após obter uma e editá-la conforme preferir, execute-a. Visual Studio Code retorna os comentários apropriados quando o aplicativo termina de executar:

![Saída do Aplicativo](media/vs-extension/app_output.png)

Como você pode ver acima, a saída é fornecida em um arquivo `.json` temporário em seu workspace. Se quiser manter essa saída, fique à vontade para salvá-la; caso contrário, ela será excluída no fechamento. Se o aplicativo não tiver nenhuma saída para imprimir em um arquivo, você só receberá a notificação `Successful App Run` na parte inferior. Se não tiver uma execução bem-sucedida, você receberá uma mensagem de erro apropriada que o ajudará a determinar o que está errado.

Ao executar um aplicativo, há várias maneiras de passar parâmetros:

Você pode especificar todas as entradas necessárias por meio de um `.json`, ou seja:

- `inputs: ./example.json`

Ao chamar um aplicativo implantado, se algum parâmetro de entrada for inato ao aplicativo ou usuário especificado e o parâmetro de entrada fornecido não for primitivo, como uma matriz, um vetor, um dataframe, um JSON complexo etc., especifique o tipo de parâmetro diretamente na linha ao chamar o aplicativo, isto é:

- Vetor
    - `inputs:`
        - `x: [1, 2, 3]`
- Matriz
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

Ou forneça uma cadeia de caracteres como um caminho de arquivo relativo ou absoluto para um `.txt`, `.json` ou `.csv` que forneça a entrada necessária no formato que seu aplicativo requer. A análise do arquivo se baseia em `Node.js Path library`, em que um caminho de arquivo é definido como um `string that contains a / or \ character`.

Se o parâmetro de entrada não for fornecido conforme necessário, uma mensagem de erro apropriada será mostrada com o caminho do arquivo incorreto se um caminho de arquivo de cadeia de caracteres tiver sido fornecido ou se esse parâmetro for inválido. O criador do aplicativo tem a responsabilidade de garantir que ele compreenda os parâmetros que está definindo.

Para excluir um aplicativo, basta clicar no botão de Lixeira ao lado do aplicativo no painel lateral `Deployed Apps`.

## <a name="next-steps"></a>Próximas etapas

Explore como integrar aplicativos implantados [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em seus próprios aplicativos em [aplicativos de consumo em Big data clusters](big-data-cluster-consume-apps.md) para obter mais informações. Você também pode consultar os exemplos adicionais em [Exemplos de Implantação de Aplicativo](https://aka.ms/sql-app-deploy) para fazer experimentos com a extensão.

Para obter mais informações [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]sobre o, consulte [o que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).


Nossa meta é tornar essa extensão útil para você e agradecemos por seus comentários. Envie-os para a [equipe [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback).
