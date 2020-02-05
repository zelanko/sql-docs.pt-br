---
title: Extensão de implantação de aplicativo
titleSuffix: SQL Server big data clusters
description: Implante um script do Python ou R como um aplicativo nos Clusters de Big Data do SQL Server.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e05fa19c8453418c22829862801c5044e6c25d2b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73707148"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Como usar o Visual Studio Code para implantar aplicativos nos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar aplicativos em um cluster de Big Data do SQL Server usando o Microsoft Visual Studio Code com a extensão Implantação de Aplicativos.

## <a name="prerequisites"></a>Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Cluster de Big Data do SQL Server](big-data-cluster-overview.md)

## <a name="capabilities"></a>Funcionalidades

Esta extensão dá suporte às seguintes tarefas no Visual Studio Code:

- Autenticar com o cluster de Big Data do SQL Server.
- Recuperar um modelo de aplicativo do repositório do GitHub para implantação dos runtimes com suporte.
- Gerenciar modelos de aplicativos abertos no workspace do usuário.
- Implantar um aplicativo por meio de uma especificação no formato YAML.
- Gerenciar aplicativos implantados dentro do cluster de Big Data do SQL Server.
- Exibir todos os aplicativos que você implantou na barra lateral com informações adicionais.
- Gerar uma especificação de execução para consumir ou excluir o aplicativo do cluster.
- Consumir aplicativos implantados por meio de uma especificação de execução em YAML.

As seções a seguir descrevem o processo de instalação e fornecem uma visão geral de como a extensão funciona. 

### <a name="install"></a>Instalar

Primeiro, instale a extensão Implantação de Aplicativos no Visual Studio Code:

1. Baixe a [Extensão Implantação de Aplicativos](https://aka.ms/app-deploy-vscode) para instalar a extensão como parte do Visual Studio Code.

1. Inicie o Visual Studio Code e navegue até a barra lateral Extensões.

1. Clique no menu de contexto `…` na parte superior da barra lateral e selecione `Install from vsix`.

   ![Instalar o VSIX](media/vs-extension/install_vsix.png)

1. Localize o arquivo `sqlservbdc-app-deploy.vsix` que você baixou e escolha-o para ser instalado.

Depois que a extensão de implantação de aplicativos do cluster de Big Data do SQL Server for instalada, ela solicitará o recarregamento do Visual Studio Code. Você deverá ver o Gerenciador de Aplicativos do BDC do SQL Server na barra lateral do Visual Studio Code.

### <a name="app-explorer"></a>Gerenciador de Aplicativos

Clique na extensão na barra lateral para carregar um painel lateral mostrando o Gerenciador de Aplicativos. A seguinte captura de tela de exemplo do Gerenciador de Aplicativos mostra que não há aplicativos nem especificações de aplicativos disponíveis:

![Gerenciador de Aplicativos](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>Conectar-se ao cluster

Para se conectar ao ponto de extremidade do cluster, use um dos seguintes métodos:

- Clique na barra de status na parte inferior, que diz `SQL Server BDC Disconnected`.
- Ou clique no botão `Connect to Cluster` na parte superior, com a seta apontando para um porta.

O Visual Studio Code solicita o ponto de extremidade apropriado, o nome de usuário e a senha.

O ponto de extremidade para se conectar é o ponto de extremidade `Cluster Management Service` com a porta 30080.

Encontre também esse ponto de extremidade na linha de comando por meio de 

```
azdata bdc endpoint list
```

Uma das outras maneiras de obter essas informações é clicando com o botão direito do mouse em **Gerenciar** no servidor no Azure Data Studio, em que você encontrará os pontos de extremidade dos serviços listados.

![Ponto de extremidade do ADS](media/vs-extension/ads_end_point.png)

Depois de encontrar o ponto de extremidade a ser usado, conecte-se ao cluster.

![Nova Conexão](media/vs-extension/connect_to_cluster.png)

 Se o Visual Studio Code receber as credenciais e o ponto de extremidade do aplicativo corretos, ele notificará que você foi conectado ao cluster e você verá os aplicativos implantados populados na barra lateral. Se você se conectar com êxito, seu ponto de extremidade e nome de usuário serão salvos no `./sqldbc` como parte de seu perfil do usuário. Nenhuma senha ou tokens serão salvos. Ao fazer logon novamente, o prompt será preenchido com o host e o nome de usuário salvos, mas sempre exigirá que você insira uma senha. Se você quiser se conectar a um ponto de extremidade de cluster diferente, basta clicar novamente no `New Connection`. A conexão será fechada automaticamente se você fechar o Visual Studio Code ou se abrir outro workspace e você precisará se reconectar.

### <a name="app-template"></a>Modelo de Aplicativo

Você precisa *Abrir Workspace* no Visual Studio Code, em que salvará os artefatos do aplicativo.

Para implantar um novo aplicativo usando um de nossos modelos, clique no botão `New App Template` no painel `App Specifications`, em que será solicitado que você insira o nome, o runtime e em qual localização você gostaria de colocar o novo aplicativo no computador local. O nome e a versão fornecidos devem ser um rótulo de DNS-1035 e precisam consistir em caracteres alfanuméricos minúsculos ou '-', começar com um caractere alfabético e terminar com um caractere alfanumérico.

É recomendável colocá-lo em seu workspace atual do Visual Studio Code, de modo que você possa usar a funcionalidade completa da extensão, mas você pode colocá-lo em qualquer lugar no sistema de arquivos local.

![Novo Modelo de Aplicativo](media/vs-extension/new_app_template.png)

Após a conclusão, um novo modelo de aplicativo é gerado por meio de scaffold para você na localização especificada e a implantação `spec.yaml` é aberta em seu workspace. Se o diretório selecionado estiver em seu workspace, você também deverá vê-lo listado no painel `App Specifications`:

![Modelo de Aplicativo Carregado](media/vs-extension/loading_app_template.png)

O modelo é um aplicativo `helloworld` simples que é apresentado da seguinte maneira no painel Especificações do Aplicativo:

- **spec.yaml**
   - Instrui o cluster a implantar seu aplicativo
- **run-spec.yaml**
   - Informa ao cluster como você gostaria de chamar seu aplicativo

O código-fonte do aplicativo está na pasta Workspace.

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
  - detalhes

Se clicar em `Links`, verá que pode acessar o `swagger.json` do aplicativo implantado, de modo que possa gravar seus próprios clientes que chamam o aplicativo:

![Swagger](media/vs-extension/swagger.png)

Confira [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md) para obter mais informações.

### <a name="app-run"></a>Execução do Aplicativo

Quando o aplicativo estiver pronto, chame-o com o `run-spec.yaml` que foi fornecido como parte do modelo de aplicativo:

![Especificação de Execução](media/vs-extension/run_spec.png)

Especifique qualquer cadeia de caracteres que desejar no lugar de `hello` e, em seguida, execute-a novamente por meio do link de lente de código ou do botão de raio na barra lateral, ao lado de `run-spec.yaml`. Se não tiver uma especificação de execução por algum motivo, gere uma do aplicativo implantado no cluster:

![Obter Especificação de Execução](media/vs-extension/get_run_spec.png)

Após obter uma e editá-la conforme preferir, execute-a. O Visual Studio Code retorna os comentários apropriados quando o aplicativo conclui a execução:

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
- Objeto
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

Ou forneça uma cadeia de caracteres como um caminho de arquivo relativo ou absoluto para um `.txt`, `.json` ou `.csv` que forneça a entrada necessária no formato que seu aplicativo requer. A análise do arquivo se baseia em `Node.js Path library`, em que um caminho de arquivo é definido como um `string that contains a / or \ character`.

Se o parâmetro de entrada não for fornecido conforme necessário, uma mensagem de erro apropriada será mostrada com o caminho do arquivo incorreto se um caminho de arquivo de cadeia de caracteres tiver sido fornecido ou se esse parâmetro for inválido. O criador do aplicativo tem a responsabilidade de garantir que ele compreenda os parâmetros que está definindo.

Para excluir um aplicativo, basta clicar no botão de Lixeira ao lado do aplicativo no painel lateral `Deployed Apps`.

## <a name="next-steps"></a>Próximas etapas

Explore como integrar os aplicativos implantados no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] em seus próprios aplicativos em [Consumir aplicativos em clusters de Big Data](big-data-cluster-consume-apps.md) para obter mais informações. Você também pode consultar os exemplos adicionais em [Exemplos de Implantação de Aplicativo](https://aka.ms/sql-app-deploy) para fazer experimentos com a extensão.

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).


Nossa meta é tornar essa extensão útil para você e agradecemos por seus comentários. Envie-os para a [equipe [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback).
