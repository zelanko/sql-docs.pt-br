---
title: 'Tutorial do R: Desenvolver um modelo no SQL'
description: Saiba como criar uma solução de ponta a ponta para modelagem preditiva com base no suporte a recursos do R no SQL Server 2016 ou SQL Server 2017.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: afd34354290134d0973c1105a902b96c4bbdd706
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469997"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>Tutorial: Desenvolvimento de SQL para cientistas de dados do R
[!INCLUDE [SQL Server 2016](../../includes/applies-to-version/sqlserver2016.md)]

Neste tutorial para cientistas de dados, saiba como criar uma solução de ponta a ponta para modelagem preditiva com base no suporte a recursos do R no SQL Server 2016 ou SQL Server 2017. Este tutorial usa um banco de dados [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) no SQL Server. 

Você usará uma combinação de código do R, dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e funções SQL personalizadas para criar um modelo de classificação que indica a probabilidade de o motorista receber uma gorjeta em uma corrida de táxi específica. Você também implantará seu modelo do R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar dados do servidor para gerar pontuações com base no modelo.

Este exemplo foi escolhido porque pode ser estendido para todos os tipos de problemas reais, como prever as respostas dos clientes a campanhas de vendas ou prever gastos ou público em eventos. Como o modelo pode ser invocado por meio de um procedimento armazenado, você pode inseri-lo facilmente em um aplicativo.

Considerando que o passo a passo foi criado para apresentar os desenvolvedores do R ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], o R é usado sempre que possível. Porém, isso não significa que o R é necessariamente a melhor ferramenta para cada tarefa. Em muitos casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá fornecer um desempenho melhor, especialmente para tarefas como agregação de dados e engenharia de recursos.  Essas tarefas podem se beneficiar particularmente dos novos recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como índices columnstore com otimização de memória. Vamos tentar apontar otimizações possíveis ao longo do caminho.

## <a name="prerequisites"></a>Pré-requisitos

+ [Serviços de Machine Learning SQL Server com integração ao R](../install/sql-machine-learning-services-windows-install.md#verify-installation) ou [Serviços de R do SQL Server 2016](../install/sql-r-services-windows-install.md)

+ [Permissões de banco de dados](../security/user-permission.md) e logon do usuário do Banco de Dados do SQL Server

+ [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)

+ [Banco de dados de demonstração de Táxi de Nova York](demo-data-nyctaxi-in-sql.md)

+ Um IDE do R, como RStudio ou a ferramenta RGUI interna incluída com o R

É recomendável que você faça este passo a passo em uma estação de trabalho cliente. Você deve ser capaz de se conectar, na mesma rede, a um computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o SQL Server e a linguagem R habilitada. Para obter instruções sobre a configuração da estação de trabalho, confira [Configurar um cliente de ciência de dados para o desenvolvimento de R](../r/set-up-a-data-science-client.md).

Como alternativa, você pode executar a instrução em um computador que tenha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um ambiente de desenvolvimento do R, mas não recomendamos essa configuração para um ambiente de produção. Se você precisar colocar o cliente e o servidor no mesmo computador, instale um segundo conjunto de bibliotecas do Microsoft R para enviar o script R de um cliente "remoto". Não use as bibliotecas do R instaladas nos arquivos de programas da instância do SQL Server. Especificamente, se você estiver usando um computador, precisará da biblioteca RevoScaleR em ambos os locais para dar suporte a operações de cliente e servidor.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> Se você estiver usando o [Machine Learning Server](/machine-learning-server/) ou a [Máquina Virtual de Ciência de Dados](/azure/machine-learning/data-science-virtual-machine/), em vez do cliente R, o caminho para RevoScaleR será C:\Arquivos de Programas\Microsoft\ML Server\R_SERVER\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>Pacotes do R adicionais

Este passo a passo exige várias bibliotecas do R que não são instaladas por padrão como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. É necessário instalar os pacotes no cliente em que você desenvolve a solução e no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você implanta a solução.

### <a name="on-a-client-workstation"></a>Em uma estação de trabalho cliente

Em seu ambiente do R, copie as linhas a seguir e execute o código em uma janela do Console (Rgui ou um IDE). Alguns pacotes também instalam pacotes necessários. Ao todo, cerca de 32 pacotes são instalados. Você deve ter uma conexão com a Internet para concluir esta etapa.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>No servidor

Você tem várias opções para instalar pacotes no SQL Server. Por exemplo, o SQL Server fornece o recurso de [gerenciamento de pacotes do R](../package-management/install-additional-r-packages-on-sql-server.md) que permite aos administradores de banco de dados criar um repositório de pacotes e atribuir ao usuário os direitos para instalar seus próprios pacotes. No entanto, se você for um administrador no computador, poderá instalar novos pacotes usando o R, desde que os instale na biblioteca correta.

> [!NOTE]
> No servidor, **não** instale em uma biblioteca de usuário, mesmo se solicitado. Se você instalar em uma biblioteca de usuário, a instância do SQL Server não poderá localizar nem executar os pacotes. Para saber mais, confira [Como instalar novos pacotes do R no SQL Server](../package-management/install-additional-r-packages-on-sql-server.md).

1. No computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abra RGui.exe **como administrador**.  Se você tiver instalado o SQL Server R Services usando os padrões, Rgui.exe poderá ser encontrado em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64.

2. Em um prompt do R, execute os seguintes comandos do R:
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  Este exemplo usa a função grep do R para pesquisar o vetor dos caminhos disponíveis e encontrar o caminho que inclui "Arquivos de Programas". Para obter mais informações, confira [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep).

  Se você acha que os pacotes já estão instalados, verifique a lista de pacotes instalados executando `installed.packages()`.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Explorar e resumir os dados](walkthrough-view-and-summarize-data-using-r.md)