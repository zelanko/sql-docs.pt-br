---
title: "Mergulho profundo de ciência de dados: usando os RevoScaleR pacotes com o SQL Server | Microsoft Docs"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 003434a055ab73afb288ea5801130ce1c06aa9c5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>Mergulho profundo de ciência de dados: usando os RevoScaleR pacotes com o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tutorial demonstra como usar os pacotes de R aprimorados fornecidos [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para trabalhar com dados do SQL Server e criar soluções de R escalonáveis, usando o servidor como um contexto de computação para análises de dados grandes de alto desempenho.

Você aprenderá a criar um contexto de computação remota, mover dados entre contextos de computação local e remoto e execute o código R em um servidor SQL remoto. Você também aprenderá como analisar e plotar dados localmente e no servidor remoto e como criar e implantar modelos.

> [!NOTE]
> 
> Este tutorial funciona especificamente com dados do SQL Server no Windows e usa os contextos de computação no banco de dados. Se você quiser usar o R em outros contextos, como Teradata, Linux ou Hadoop, consulte estes tutoriais do Microsoft R Server: 
> + [Usar servidor de R com sparklyr](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [Explorar R e ScaleR em 25 funções](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)
> + [Introdução ao ScaleR no Hadoop MapReduce](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>Visão geral

Para utilizar a potência de processamento e a flexibilidade do pacote RevoScaleR, neste tutorial, você move dados e troca de contextos de computação com frequência. Para ilustrar, aqui estão algumas das tarefas neste tutorial:

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Importar os dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções do pacote RevoScaleR.
+ Modelo de treinamento e pontuação é realizada usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contexto de computação. 
+ Usar funções de RevoScaleR para criar um novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabelas para salvar os resultados de pontuação.
+ Crie dois gráficos no servidor e contexto de computação local.
+ Treinar um modelo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados, executar R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
+ Extrair um subconjunto de dados e salvá-lo como um arquivo XDF para reutilização em análise na sua estação de trabalho local.
+ Obter novos dados para pontuação, abrindo uma conexão ODBC para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. A pontuação é feita na estação de trabalho local.
+ Criar uma função personalizada de R e executá-lo no servidor do contexto de computação para executar uma simulação.

### <a name="article-list-and-time-required"></a>Lista de artigos e o tempo necessário

Este tutorial leva cerca de 75 minutos para ser concluída, não incluindo o programa de instalação.

1. [Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Criar objetos de dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definir e usar contextos de computação](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Criar e executar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Criar modelos de R](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Novos dados de pontuação](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Transformar dados usando o R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Carregar dados em memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Criar novas tabelas do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analisar dados no contexto de computação local](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Mover dados do SQL Server usando arquivos XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Criar uma simulação simples](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Público-alvo

Este tutorial foi desenvolvido para cientistas de dados ou para pessoas que já estão um pouco familiarizadas com R e as tarefas de ciência de dados, como resumos e criação de modelo.  No entanto, todo o código é fornecido, mesmo se você for novo para R, você pode executar o código e acompanhar, supondo que você tenha os ambientes de cliente e servidor necessários.

Você também deve estar familiarizado com [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e saber como acessar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados usando ferramentas como estes:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Ferramentas de banco de dados no Visual Studio 
+ A versão gratuita [extensão mssql para o código do Visual Studio](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode).
  
> [!TIP]
> Salve seu espaço de trabalho do R entre as lições para que você possa facilmente selecionar a seção em que parou.

### <a name="prerequisites"></a>Prerequisites

- **SQL Server com suporte para R**
  
    Instalar o SQL Server 2016 e habilitar R Services (no banco de dados). Ou, instale o SQL Server 2017 e habilitar serviços de aprendizado de máquina e escolher a linguagem R.
  
-  **Permissões de banco de dados**
  
    Para executar as consultas usadas para treinar o modelo, você deve ter privilégios **db_datareader** no banco de dados em que os dados são armazenados. Para executar R, o usuário deve ter a permissão EXECUTE ANY EXTERNAL SCRIPT.

-   **Computador de desenvolvimento de ciência de dados**
  
    Você deve instalar os pacotes de RevoScaleR e provedores relacionados no computador usado como o ambiente de desenvolvimento de R. A maneira mais fácil de fazer isso é instalar o cliente do Microsoft R, Microsoft R Server (autônomo) ou servidor de aprendizado de máquina (autônomo). 
      
    > [!NOTE] 
    > Não há suporte para outras versões do Revolution R Enterprise ou Revolution R Open.
    > 
    > Uma distribuição de software livre do R não pode ser usada neste tutorial, porque apenas as funções RevoScaleR podem usar contextos de computação remota.
  
-   **Pacotes do R adicionais**
  
    Neste tutorial, você pode instalar os seguintes pacotes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, e **e1071** . Instruções são fornecidas como parte do tutorial.
  
    Todos os pacotes devem ser instalados em dois locais: no computador que você usa para o desenvolvimento de soluções de R e no computador do SQL Server onde os scripts de R são executadas. Se você não tem permissão para instalar os pacotes no computador do servidor, peça ao administrador. 
    
    **Não instale os pacotes em uma biblioteca do usuário.** Os pacotes devem ser instalados na biblioteca de pacote de R que é usada pela instância do SQL Server.

Para obter mais informações, consulte [pré-requisitos para instruções passo a passo de ciência de dados](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-step"></a>Próxima etapa

[Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

