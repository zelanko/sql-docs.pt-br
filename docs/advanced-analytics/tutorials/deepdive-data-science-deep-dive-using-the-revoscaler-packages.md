---
title: "Aprofundamento da ciência de dados: usando os pacotes RevoScaleR | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51f4a782ad941d8b9a66ba00cbf2b3540478361c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR

Este tutorial demonstra como usar os pacotes de R aprimorados fornecidos [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para trabalhar com dados do SQL Server e criar soluções de R escalonáveis, usando o servidor como um contexto de computação para análises de dados grandes de alto desempenho.

Você aprenderá como criar um contexto de computação remota, mover dados entre contextos de computação local e remoto e execute o código R em um servidor SQL remoto. Você também aprenderá como analisar e plotar dados localmente e no servidor remoto e como criar e implantar modelos.

> [!NOTE]
> 
> Este tutorial funciona especificamente com dados do SQL Server no Windows e usa os contextos de computação no banco de dados. Se você quiser usar o R em outros contextos, como Teradata, Linux ou Hadoop, consulte estes tutoriais do Microsoft R Server: 
> + [Usar servidor de R com sparklyr](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explorar R e ScaleR em 25 funções](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)
> + [Introdução ao ScaleR no Hadoop MapReduce](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [Guia de Introdução do RevoScaleR Teradata obtendo](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>Visão geral

Para ilustrar o poder de processamento e a flexibilidade dos pacotes ScaleR, neste tutorial, você moverá dados e trocará contextos de computação com frequência.

+ Inicialmente, os dados são obtidos dos arquivos CSV ou XDF. Você importará os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando as funções no pacote RevoScaleR.
+ O treinamento e a pontuação do modelo serão executadas no contexto de computação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
    Você criará novas tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , usando as funções **rx** , para salvar os resultados da pontuação.
+ Você criará plotagens tanto no servidor quanto no contexto de computação local.
+ Para treinar o modelo, você usará os dados já armazenados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Todos os cálculos serão executados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
+ Você extrairá um subconjunto de dados e os salvará como um arquivo XDF para usá-los novamente em análises em sua estação de trabalho local.
+ Os novos dados usados durante o processo de pontuação são extraídos do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma conexão ODBC. Todos os cálculos são executados na estação de trabalho local.
+ Por fim, você executará uma simulação com base em uma função do R personalizada usando o contexto de computação do servidor.

### <a name="get-started-now"></a>Comece agora mesmo

Este tutorial leva cerca de 75 minutos para ser concluída, não incluindo o programa de instalação.

1. [Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [Criar Objetos de Dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [Definir e usar contextos de computação](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [Criar e executar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [Criar modelos de R](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [Novos dados de pontuação](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [Transformar dados usando R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [Carregar dados em memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [Executar análise de agrupamento usando rxDataStep](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [Analisar dados no contexto de computação Local;](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [Mover dados entre o SQL Server e o arquivo XDF](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [Criar um simples de simulação](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>Público-alvo

Este tutorial destina-se a cientistas de dados ou a pessoas que já estejam minimamente familiarizadas em tarefas de ciência de dados e do R, incluindo exploração, análise estatística e ajuste de modelos.  No entanto, todo o código é fornecido, mesmo se você for novo para R, você pode facilmente executar o código e acompanhar, supondo que você tenha os ambientes de cliente e servidor necessários.

Você também deve estar familiarizado com a sintaxe do [!INCLUDE[tsql](../../includes/tsql-md.md)] e saber como acessar um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou outras ferramentas de banco de dados, como o Visual Studio.
  
> [!TIP]
> Salve seu espaço de trabalho do R entre as lições para que você possa facilmente selecionar a seção em que parou.

### <a name="prerequisites"></a>Pré-requisitos

- **SQL Server com suporte para R**
  
    Instalar o SQL Server 2016 e habilitar R Services (no banco de dados). Ou, instale o SQL Server 2017 e habilitar serviços de aprendizado de máquina e escolher a linguagem R. O processo de instalação é descrito em [Manuais Online do SQL Server 2016](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx).
  
-  **Permissões de banco de dados**
  
    Para executar as consultas usadas para treinar o modelo, você deve ter privilégios **db_datareader** no banco de dados em que os dados são armazenados. Para executar R, o usuário deve ter a permissão EXECUTE ANY EXTERNAL SCRIPT.

-   **Computador de desenvolvimento de ciência de dados**
  
    Instale também os pacotes de RevoScaleR e provedores relacionados em seu ambiente de desenvolvimento de R. A maneira mais fácil de fazer isso é instalar o cliente do Microsoft R ou o Microsoft R Server (autônomo). Para obter mais informações, consulte [Configurar um cliente de ciência de dados](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)
      
    > [!NOTE] 
    > Não há suporte para outras versões do Revolution R Enterprise ou Revolution R Open.
    > 
    > Uma distribuição de software livre do R, como R 3.2.2, não funcionará neste tutorial, porque apenas as funções RevoScaleR podem usar contextos de computação remota.
  
-   **Pacotes do R adicionais**
  
    Para este tutorial, você precisará instalar os seguintes pacotes: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**e **e1071**. Instruções são fornecidas como parte do tutorial.
  
    Todos os pacotes devem ser instalados em dois locais: no computador que você usa para o desenvolvimento de soluções de R e no computador do SQL Server onde os scripts de R serão executados. Se você não tem permissão para instalar os pacotes no computador do servidor, peça ao administrador. **Não instale os pacotes em uma biblioteca do usuário.** É importante que os pacotes instalados na biblioteca de pacote de R que é usada pela instância do SQL Server.

Para obter mais informações, consulte [pré-requisitos para instruções passo a passo de ciência de dados](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).



## <a name="next-step"></a>Próxima etapa

[Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


