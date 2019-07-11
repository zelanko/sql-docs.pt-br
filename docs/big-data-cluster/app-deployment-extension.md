---
title: Extensão de implantação do aplicativo
titleSuffix: SQL Server big data clusters
description: Implante um script Python ou R como um aplicativo no cluster de big data do SQL Server 2019 (visualização).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ba56ebb90d09866b7860c5f29dd2a26cf525fd9b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729306"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>Como usar o VS Code para implantar aplicativos em clusters de grandes dados do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como implantar aplicativos em um cluster de big data do SQL Server usando o Visual Studio Code com a extensão de implantação do aplicativo. Essa funcionalidade foi introduzida no CTP 2.3. 

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio Code](https://code.visualstudio.com/).
- [Cluster de big data do SQL Server](big-data-cluster-overview.md) CTP 2.3 ou posterior.

## <a name="capabilities"></a>Capacidades

Essa extensão oferece suporte as seguintes tarefas no Visual Studio Code:

- Autenticar com o cluster de big data do SQL Server.
- Recupere um modelo de aplicativo do repositório do GitHub para a implantação de tempos de execução com suporte.
- Gerencie modelos de aplicativo atualmente aberto no espaço de trabalho do usuário.
- Implante um aplicativo por meio de uma especificação de formato YAML.
- Gerencie aplicativos implantados dentro do cluster de big data do SQL Server.
- Exiba todos os aplicativos que você implantou na barra lateral com informações adicionais.
- Gere uma especificação de execução para consumir o aplicativo ou excluir o aplicativo do cluster.
- Consuma aplicativos implantados por meio de uma especificação de execução YAML.

As seções a seguir orientam, no entanto, o processo de instalação e fornece uma visão geral de como funciona a extensão. 

### <a name="install"></a>Instalar

Primeiro, instale a extensão de implantação do aplicativo no Visual Studio Code:

1. Baixe [extensão de implantar o aplicativo](https://aka.ms/app-deploy-vscode) para instalar a extensão como parte do código do VS.

1. Inicie o VS Code e navegue até a barra lateral de extensões.

1. Clique o `…` menu de contexto na parte superior de barra lateral e selecione `Install from vsix`.

   ![Instalar o VSIX](media/vs-extension/install_vsix.png)

1. Encontre o `sqlservbdc-app-deploy.vsix` arquivo que você baixou e escolha a que instalar.

Depois de implantar o aplicativo de cluster de big data do SQL Server extensão tiver sido instalada, ele solicitará que você recarregar o VS Code. Agora você deve ver o Pesquisador de aplicativo do SQL Server BDC na barra lateral do VS Code.

### <a name="app-explorer"></a>Gerenciador de aplicativo

Clique na extensão na barra lateral para carregar um painel lateral mostrando o Gerenciador do aplicativo. A seguinte captura de tela de exemplo do Gerenciador do aplicativo mostra não aplicativos ou as especificações de aplicativo disponíveis:

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>Nova Conexão

Para se conectar ao ponto de extremidade do cluster, use um dos seguintes métodos:

- Clique na barra de status na parte inferior que diz `SQL Server BDC Disconnected`.
- Ou clique no `New Connection` botão na parte superior com a seta que aponta para uma porta de entrada.

   ![Nova Conexão](media/vs-extension/connect_to_cluster.png)

VS Code solicitará o ponto de extremidade apropriado, o nome de usuário e a senha. Se fornecido as credenciais corretas e o ponto de extremidade do aplicativo, o VS Code notifica que já está conectado ao cluster e você verá quaisquer aplicativos implantados populados na barra lateral. Se você se conectar com êxito, seu ponto de extremidade e o nome de usuário serão salvos para `./sqldbc` como parte do perfil do usuário. Nenhuma senha ou tokens nunca serão salvo. Ao fazer logon novamente, o prompt de preencher previamente com o host salvo e o nome de usuário mas sempre exigem que você insira uma senha. Se você quiser se conectar a um ponto de extremidade de cluster diferente, basta clicar o `New Connection` novamente. A conexão será fechada automaticamente se você fechar o VS Code ou se você abrir um espaço de trabalho diferente e você precisará ser reconectado.

### <a name="app-template"></a>Modelo de aplicativo

Para implantar um novo aplicativo de um dos nossos modelos, clique no `New App Template` botão o `App Specifications` painel, em que você será solicitado para o nome, o tempo de execução e o que local você gostaria de colocar o novo aplicativo em seu computador local. É recomendável que você colocá-lo no seu espaço de trabalho atual do VS Code para que você pode usar a funcionalidade completa da extensão, mas você pode colocá-lo em qualquer lugar no sistema de arquivos local.

![Novo modelo de aplicativo](media/vs-extension/new_app_template.png)

Depois de concluído, um novo modelo de aplicativo é gerado automaticamente para você no local especificado e a implantação `spec.yaml` é aberto em seu espaço de trabalho. Se o diretório que você selecionou está em seu espaço de trabalho, você também verá listado sob o `App Specifications` painel:

![Modelo de aplicativo carregado](media/vs-extension/loading_app_template.png)

O modelo é um simples `Hello World` aplicativo que está disposto da seguinte maneira:

- **spec.yaml**
   - Informa o cluster como implantar seu aplicativo
- **run-spec.yaml**
   - Informa o cluster como você deseja chamar seu aplicativo
- **handler.py**
   - Isso é o seu arquivo de código fonte conforme especificado por `src` em `spec.yaml`
   - Ele tem uma função de chamada `handler` que é considerado o `entrypoint` do aplicativo, conforme mostrado no `spec.yaml`. Ele usa uma entrada de cadeia de caracteres denominada `msg` e retorna uma saída de cadeia de caracteres chamada `out`. Essas são especificadas nas `inputs` e `outputs` da `spec.yaml`.

Se você não quiser que um modelo gerado por scaffolding e simplesmente prefere uma `spec.yaml` para implantação de um aplicativo que você criou, clique o `New Deploy Spec` lado a `New App Template` botão e examinará o mesmo processo, mas você apenas receberá a `spec.yaml`, que você pode modificar a maneira escolhida.

### <a name="deploy-app"></a>Implantar aplicativo

Instantaneamente, você pode implantar esse aplicativo por meio das lentes de código `Deploy App` no `spec.yaml` ou pressione o botão de pasta do raio ao lado de `spec.yaml` arquivo no menu de especificações do aplicativo. A extensão será compactar todos os arquivos no diretório onde seu `spec.yaml` está localizado e implantar seu aplicativo no cluster. 

>[!NOTE]
>Verifique se todos os seus arquivos de aplicativo estão no mesmo diretório que seu `spec.yaml`. O `spec.yaml` deve estar no nível raiz do seu diretório de código de origem do aplicativo. 

![Implantar o botão do aplicativo](media/vs-extension/deploy_app_lightning.png)

![Implantar o aplicativo CodeLens](media/vs-extension/deploy_app_codelens.png)

Você será notificado quando o aplicativo está pronto para consumo de acordo com o estado do aplicativo na barra lateral:

![Aplicativo implantado](media/vs-extension/app_deploy.png)

![Barra do lado do aplicativo pronto para](media/vs-extension/app_ready_side_bar.png)

![Notificação de aplicativo pronto](media/vs-extension/app_ready_notification.png)

No painel do lado, você será capaz de ver os seguintes itens estão disponíveis para você:

Você pode exibir todos os aplicativos que você implantou na barra lateral com as seguintes informações:

- state
- version
- Parâmetros de entrada
- Parâmetros de saída
- links
  - swagger
  - details

Se você clicar `Links`, você verá que você pode acessar o `swagger.json` do seu aplicativo implantado, para que você possa escrever seus próprios clientes que chamam o seu aplicativo:

![swagger](media/vs-extension/swagger.png)

Ver [consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md) para obter mais informações.

### <a name="app-run"></a>Execução do aplicativo

Depois que o aplicativo estiver pronto, chame o aplicativo com o `run-spec.yaml` que foi fornecido como parte do modelo de aplicativo:

![Especificação de execução](media/vs-extension/run_spec.png)

Especifique qualquer cadeia de caracteres que você deseja no lugar de `hello` e, em seguida, novamente executá-lo por meio do link de Lente de código ou no botão de relâmpago na barra lateral do lado do `run-spec.yaml`. Se você não tiver uma especificação de execução por algum motivo, gere um do aplicativo implantado no cluster:

![Obter a especificação de execução](media/vs-extension/get_run_spec.png)

Depois que você tiver um e editou a sua satisfação, executá-lo. VS Code retorna os comentários apropriados quando o aplicativo terminar a execução:

![Saída do aplicativo](media/vs-extension/app_output.png)

Como você pode ver acima, a saída é determinada em um temporário `.json` arquivo no seu espaço de trabalho. Se você quiser manter essa saída, fique à vontade para salvá-lo, caso contrário, ele será excluído no fechamento. Se seu aplicativo não tem saída para imprimir um arquivo, você só receberá o `Successful App Run` notificação na parte inferior. Se você não tinha uma execução bem-sucedida, você receberá uma mensagem de erro apropriada que ajudarão você a determinar o que está errado.

Ao executar um aplicativo, há várias maneiras para passar parâmetros:

Você pode especificar todas as entradas necessárias por meio de um `.json`, que é:

- `inputs: ./example.json`

Ao chamar um aplicativo implantado, se quaisquer parâmetros de entrada são inato para o aplicativo ou usuário especificado e que o parâmetro de entrada é algo diferente de um primitivo, como uma matriz, vetor, dataframe, JSON complexo, etc. Especifique o tipo de parâmetro diretamente na linha quando chamar o aplicativo, ou seja:

- vetor
    - `inputs:`
        - `x: [1, 2, 3]`
- Matriz
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

Ou fornecer uma cadeia de caracteres como um caminho relativo ou absoluto para um `.txt`, `.json`, ou `.csv` que fornece a entrada necessária no formato que seu aplicativo requer. A análise do arquivo se baseia `Node.js Path library`, em que um caminho de arquivo é definido como um `string that contains a / or \ character`.

Se o parâmetro de entrada não for fornecido, conforme necessário, uma mensagem de erro apropriado será mostrada com o caminho de arquivo incorreto se recebeu um caminho de arquivo de cadeia de caracteres ou se esse parâmetro era inválido. A responsabilidade é fornecida para o criador do aplicativo para garantir que eles entendem os parâmetros que eles estão definindo.

Para excluir um aplicativo, simplesmente clique na Lixeira pode botão ao lado do aplicativo no `Deployed Apps` painel lateral.

## <a name="next-steps"></a>Próximas etapas

Explore como integrar aplicativos implantados no SQL Server em seus próprios aplicativos em clusters do big data [consumir aplicativos em clusters de big data](big-data-cluster-consume-apps.md) para obter mais informações. Você também pode consultar os exemplos adicionais neste [exemplos de implantar o aplicativo](https://aka.ms/sql-app-deploy) para experimentar com a extensão.

Para obter mais informações sobre clusters de grandes dados do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).


Nosso objetivo é tornar essa extensão útil para você e Agradecemos comentários. Envie-os para [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipe](https://aka.ms/sqlfeedback).
