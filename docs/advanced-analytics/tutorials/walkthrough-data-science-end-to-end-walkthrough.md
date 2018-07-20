---
title: Passo a passo de ciência de dados de ponta a ponta para R e SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d4f38fd424c881392d48b0a6a24feb7f7e27ee0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086498"
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>Passo a passo de ciência de dados de ponta a ponta para R e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste passo a passo, você deve desenvolver uma solução de ponta a ponta para modelagem de previsão com base no suporte de recurso do R no SQL Server 2016 ou SQL Server 2017.

Este passo a passo baseia-se em um conjunto de dados público conhecido, o conjunto de dados de táxi de Nova York. Você usa uma combinação de código R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e funções SQL personalizadas para criar um modelo de classificação que indica a probabilidade de que o driver pode receber uma gorjeta em uma corrida de táxi específica. Você também implantar seu modelo de R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar dados de servidor para gerar pontuações com base no modelo.

Este exemplo pode ser estendido para todos os tipos de problemas da vida real, como prever as respostas dos clientes a campanhas de vendas ou prever gastos ou participação em eventos. Porque o modelo pode ser invocado a partir de um procedimento armazenado, você pode inseri-lo facilmente em um aplicativo.

Porque o passo a passo foi projetada para apresentar os desenvolvedores do R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R é usado sempre que possível. No entanto, isso não significa que o R é necessariamente a melhor ferramenta para cada tarefa. Em muitos casos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá fornecer um desempenho melhor, especialmente para tarefas como agregação de dados e engenharia de recursos.  Essas tarefas podem se beneficiar particularmente dos novos recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como índices columnstore com otimização de memória. Tentamos para destacar as otimizações possíveis ao longo do caminho.

## <a name="target-audience"></a>Público-alvo

Este passo a passo é destinado a desenvolvedores do R ou do SQL. Ele fornece uma introdução sobre como o R pode ser integrado em fluxos de trabalho empresariais usando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  Você deve estar familiarizado com as operações de banco de dados, como criação de tabelas e bancos de dados, importação de dados e execução de consultas.

+ Todos os scripts SQL e R são incluídos.
+ Talvez você precise modificar cadeias de caracteres nos scripts, para ser executado em seu ambiente. Você pode fazer isso com qualquer editor de códigos, tais como [Visual Studio Code](https://code.visualstudio.com/Download).

## <a name="prerequisites"></a>Prerequisites

É recomendável que você faça este passo a passo em um laptop ou outro computador que tenha as bibliotecas Microsoft R instaladas. Você deve ser capaz de estabelecer uma conexão, na mesma rede, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador com SQL Server e a linguagem R habilitado.

Você pode executar o passo a passo em um computador que tem ambos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um ambiente de desenvolvimento de R, mas nós não recomendamos essa configuração para um ambiente de produção.

Se você quiser executar os comandos de R de um computador remoto, como um laptop ou outro computador da rede, você deve instalar as bibliotecas Microsoft R Open. Você pode instalar o Microsoft R Client ou Microsoft R Server. O computador remoto deve ser capaz de conectar-se para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.

Se você precisar colocar o cliente e servidor no mesmo computador, certifique-se de instalar um conjunto separado de bibliotecas do Microsoft R para uso no envio de script R de um cliente "remoto". Não use as bibliotecas do R que são instaladas para uso pela instância do SQL Server para essa finalidade.

## <a name="add-r-to-sql-server"></a>Adicionar o R para o SQL Server

Você deve ter acesso a uma instância do SQL Server com suporte para o R instalado. Este passo a passo foi originalmente desenvolvido para ervidor SQL 2016 e testado em 2017, portanto, você deve ser capaz de usar qualquer uma das seguintes versões do SQL Server. (Há algumas pequenas diferenças nas funções de RevoScaleR entre as versões.)

+ [Instalar os serviços SQL Server 2017 Machine Learning](../install/sql-machine-learning-services-windows-install.md)
+ [Instalar o SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

## <a name="install-an-r-development-environment"></a>Instalar um ambiente de desenvolvimento de R

Para este passo a passo, é recomendável que você use um ambiente de desenvolvimento de R. Aqui estão algumas sugestões:

- **Ferramentas do R para Visual Studio** (RTVS) é um plug-in que fornece o Intellisense, depuração e suporte para o Microsoft R. você pode usá-lo com o R Server e serviços do SQL Server Machine Learning. Para baixar, consulte [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/).

- **Microsoft R Client** é uma ferramenta de desenvolvimento leve que dá suporte ao desenvolvimento em R usando o pacote RevoScaleR. Para fazer isso, veja [Começar a usar o cliente do Microsoft R](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client).

- O**RStudio** é um dos ambientes mais populares para desenvolvimento do R. Para obter mais informações, consulte [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/).

    Você não pode concluir este tutorial usando uma instalação genérica do RStudio ou em outro ambiente; Você também deve instalar os pacotes R e bibliotecas de conectividade do Microsoft R Open. Para obter mais informações, consulte [Configurar um cliente de ciência de dados](../r/set-up-a-data-science-client.md).

- Ferramentas básicas de R (R.exe, RTerm.exe, RScripts.exe) também são instaladas por padrão, quando você instala o R no SQL Server ou cliente do R. Se você não quiser instalar um IDE, você pode usar essas ferramentas.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>Obter permissões na instância do SQL Server e banco de dados

Para se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados.  Você pode usar um logon SQL ou a autenticação integrada do Windows. Peça ao administrador de banco de dados para configurar as seguintes permissões para a conta, no banco de dados em que você usar o r:

- Criar banco de dados, tabelas, funções e procedimentos armazenados
- Gravar dados em tabelas
- Capacidade de executar script R (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

Para este passo a passo, usamos o logon do SQL **RTestUser**. Em geral, é recomendável que você usa a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para algumas finalidades de demonstração.

## <a name="next-steps"></a>Próximas etapas

[Preparar os dados usando o PowerShell](walkthrough-prepare-the-data.md)
