---
title: Carregando dados
description: Você pode carregar ou inserir dados em SQL Server data warehouse paralelo (PDW) usando Integration Services, utilitário bcp, dwloader ou a instrução SQL INSERT.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401046"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Carregando dados em data warehouse paralelos
Você pode carregar ou inserir dados em SQL Server data warehouse paralelo (PDW) usando Integration Services, [utilitário bcp](../tools/bcp-utility.md), carregador de linha de comando **dwloader** ou a instrução SQL INSERT.  

## <a name="loading-environment"></a>Carregando ambiente  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL ou outros servidores existentes ou pode comprar novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor de carregamento](acquire-and-configure-loading-server.md). Essas instruções incluem uma [planilha de planejamento de capacidade do servidor de carregamento](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para o carregamento.  
  
## <a name="load-with-dwloader"></a>Carregar com dwloader  
Usar o [carregador de linha de comando dwloader](dwloader.md) é a maneira mais rápida de carregar dados no PDW.  
  
![Processo de carregamento](media/loading-process.png "Processo de carregamento")  
  
o dwloader carrega dados diretamente nos nós de computação sem passar os dados por meio do nó de controle. Para carregar dados, o dwloader primeiro se comunica com o nó de controle para obter informações de contato para os nós de computação. o dwloader configura um canal de comunicação com cada nó de computação e, em seguida, envia blocos de 256KB de dados para os nós de computação de forma Round Robin.  
  
Em cada nó de computação, o DMS (serviço de movimentação de dados) recebe e processa as partes dos dados. O processamento dos dados inclui a conversão de cada linha em SQL Server formato nativo e a computação do hash de distribuição para determinar o nó de computação ao qual cada linha pertence.  
  
Depois de processar as linhas, DMS usa uma movimentação em ordem aleatória para transferir cada linha para o nó de computação e a instância de SQL Server corretas. Conforme SQL Server recebe as linhas, ele os coloca em lotes de acordo com o parâmetro de tamanho de lote **-b** definido em dwloader e, em seguida, carrega o lote em massa.  

## <a name="load-with-prepared-statements"></a>Carregar com instruções preparadas

Você pode usar instruções preparadas para carregar dados em tabelas distribuídas e replicadas. Quando os dados de entrada não correspondem ao tipo de dados de destino, uma conversão implícita é executada. As conversões implícitas com suporte pelas instruções preparadas do PDW são um subconjunto de conversões com suporte pelo SQL Server. Ou seja, há suporte apenas para um subconjunto de conversões, mas as conversões com suporte correspondem SQL Server conversões implícitas. Independentemente de a tabela de destino ser carregada ser definida como uma tabela distribuída ou replicada, conversões implícitas são aplicadas (se necessário) a todas as colunas existentes na tabela de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Crie o banco de dados de preparo.|[Criar o banco de dados de preparo](staging-database.md)|  
|Carregar com Integration Services.|[Carregar com Integration Services](load-with-ssis.md)|  
|Entenda as conversões de tipo para dwloader.|[Regras de conversão de tipo de dados para dwloader](dwloader-data-type-conversion-rules.md)|  
|Carregar dados com dwloader.|[Carregador de linha de comando dwloader](dwloader.md)|  
|Compreenda as conversões de tipo para inserção.|[Carregar dados com INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
