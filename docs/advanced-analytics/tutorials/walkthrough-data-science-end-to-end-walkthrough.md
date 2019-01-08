---
title: Tutorial para cientistas de dados usando a linguagem R - aprendizagem de máquina do SQL Server
description: Tutorial que mostra como criar uma solução de R de ponta a ponta para análise no banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7fbed76272903fb7a9b6eee037a070677411a0f5
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596417"
---
# <a name="tutorial-in-database-analytics-for-data-scientists-using-r"></a>Tutorial: Análise no banco de dados para cientistas de dados usando o R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste tutorial para cientistas de dados, Aprenda a criar a solução de ponta a ponta para modelagem de previsão com base no suporte de recurso do R no SQL Server 2016 ou SQL Server 2017. Este tutorial usa um [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) banco de dados no SQL Server. 

Você usa uma combinação de código R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e funções SQL personalizadas para criar um modelo de classificação que indica a probabilidade de que o driver pode receber uma gorjeta em uma corrida de táxi específica. Você também implantar seu modelo de R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar dados de servidor para gerar pontuações com base no modelo.

Este exemplo pode ser estendido para todos os tipos de problemas da vida real, como prever as respostas dos clientes a campanhas de vendas ou prever gastos ou participação em eventos. Porque o modelo pode ser invocado a partir de um procedimento armazenado, você pode inseri-lo facilmente em um aplicativo.

Porque o passo a passo foi projetada para apresentar os desenvolvedores do R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R é usado sempre que possível. No entanto, isso não significa que o R é necessariamente a melhor ferramenta para cada tarefa. Em muitos casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá fornecer um desempenho melhor, especialmente para tarefas como agregação de dados e engenharia de recursos.  Essas tarefas podem se beneficiar particularmente dos novos recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como índices columnstore com otimização de memória. Tentamos para destacar as otimizações possíveis ao longo do caminho.

## <a name="prerequisites"></a>Prerequisites

+ [Serviços do SQL Server 2017 Machine Learning com a integração do R](../install/sql-machine-learning-services-windows-install.md#verify-installation) ou [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [Permissões de banco de dados](../security/user-permission.md) e um logon de usuário de banco de dados do SQL Server

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [Banco de dados de demonstração de táxi de NYC](demo-data-nyctaxi-in-sql.md)

+ Um IDE R como RStudio ou a ferramenta interna do RGUI incluído com o R

É recomendável que você faça este passo a passo em uma estação de trabalho do cliente. Você deve ser capaz de estabelecer uma conexão, na mesma rede, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador com SQL Server e a linguagem R habilitado. Para obter instruções sobre configuração de estação de trabalho, consulte [configurar um cliente de ciência de dados para o desenvolvimento de R](../r/set-up-a-data-science-client.md).

Como alternativa, você pode executar o passo a passo em um computador que tem ambos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um ambiente de desenvolvimento de R, mas nós não recomendamos essa configuração para um ambiente de produção. Se você precisar colocar o cliente e servidor no mesmo computador, certifique-se de instalar um segundo conjunto de bibliotecas do Microsoft R para o envio de script R de um cliente "remoto". Não use as bibliotecas do R que estão instaladas nos arquivos de programa da instância do SQL Server. Especificamente, se você estiver usando um computador, você precisa da biblioteca RevoScaleR em um desses locais para oferecer suporte a operações de cliente e servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ Server\MSSQL14 SQL do C:\Program Files\Microsoft. MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Pacotes R adicionais

Este passo a passo requer várias bibliotecas de R que não são instaladas por padrão como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Você deve instalar os pacotes no cliente onde você desenvolve a solução e no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador em que você implantar a solução.

### <a name="on-a-client-workstation"></a>Em uma estação de trabalho do cliente

Em seu ambiente de R, copie as seguintes linhas e executar o código em uma janela de Console (Rgui ou um IDE). Alguns pacotes também instalam os pacotes necessários. Ao todo, 32 pacotes são instalados. Você deve ter uma conexão de internet para concluir esta etapa.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>No servidor

Você tem várias opções para instalar pacotes no SQL Server. Por exemplo, o SQL Server fornece [gerenciamento de pacotes R](../r/install-additional-r-packages-on-sql-server.md) recurso que permite que os administradores de banco de dados, criar um repositório de pacotes e atribuir os direitos para instalar seus próprios pacotes de usuário. No entanto, se você for um administrador no computador, você pode instalar novos pacotes usando o R, desde que você instale a biblioteca correta.

> [!NOTE]
> No servidor, **não** instale em uma biblioteca de usuário, mesmo se for solicitado. Se você instalar em uma biblioteca do usuário, a instância do SQL Server não pode localizar ou executar os pacotes. Para obter mais informações, consulte [instalar novos pacotes de R no SQL Server](../r/install-additional-r-packages-on-sql-server.md).

1. No computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Se você tiver instalado o SQL Server R Services usando os padrões, Rgui.exe pode ser encontrado em C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES\bin\x64).

2. Em um prompt do R, execute os seguintes comandos do R:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  Este exemplo usa a função grep do R para pesquisar o vetor dos caminhos disponíveis e localizar o caminho que inclui "Arquivos de programas". Para obter mais informações, consulte [ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep).

  Se você acha que os pacotes já estão instalados, verifique a lista de pacotes instalados executando `installed.packages()`.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explore e resuma os dados](walkthrough-view-and-summarize-data-using-r.md)