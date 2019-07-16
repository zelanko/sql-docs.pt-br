---
title: Carregar dados no Parallel Data Warehouse | Microsoft Docs
description: Você pode carregar ou inserir dados no SQL Server Parallel Data Warehouse (PDW) usando o utilitário bcp, Integration Services, dwloader ou a instrução SQL INSERT.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b046839b7c4932b43230d28cc106db1e2ea5d5a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960699"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Carregar dados no Parallel Data Warehouse
Você pode carregar ou inserir dados no SQL Server Parallel Data Warehouse (PDW) usando os serviços de integração [utilitário bcp](../tools/bcp-utility.md), **dwloader** carregador de linha de comando ou a instrução SQL INSERT.  

## <a name="loading-environment"></a>Carregando ambiente  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL existente ou outros servidores, ou você pode comprar novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor carregando](acquire-and-configure-loading-server.md). Essas instruções incluem um [carregamento de planilha de planejamento de capacidade de servidor](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para o carregamento.  
  
## <a name="load-with-dwloader"></a>Carregar com dwloader  
Usando o [dwloader carregador de linha de comando](dwloader.md) é a maneira mais rápida de carregar dados em PDW.  
  
![Processo de carregamento](media/loading-process.png "processo de carregamento")  
  
dwloader carrega os dados diretamente para os nós de computação sem passar os dados por meio do nó de controle. Para carregar dados, dwloader pela primeira vez se comunica com o nó de controle para obter informações de contato para os nós de computação. dwloader configura um canal de comunicação com cada nó de computação e, em seguida, envia partes de 256KB de dados para os nós de computação de forma round-robin.  
  
Em cada nó de computação, o serviço de movimentação de dados (DMS) recebe e processa as partes dos dados. Processamento de dados inclui conversão de cada linha em formato nativo do SQL Server e computar o hash de distribuição para determinar o nó de computação para o qual cada linha pertence.  
  
Depois de processar as linhas, o DMS usa uma movimentação de ordem aleatória para transferir cada linha para o nó de computação correto e a instância do SQL Server. Como o SQL Server recebe as linhas, ele processa em lotes-los de acordo com o **-b** definir o parâmetro de tamanho de lote na dwloader e, em seguida, em massa carrega o lote.  

## <a name="load-with-prepared-statements"></a>Carregar com instruções preparadas

Você pode usar as instruções preparadas para carregar dados em tabelas replicadas e distribuídas. Quando os dados de entrada não corresponder ao tipo de dados de destino, uma conversão implícita é executada. As conversões implícitas com suporte pelo PDW instruções preparadas são um subconjunto de conversões com suporte pelo SQL Server. Ou seja, apenas um subconjunto de conversões que têm suporte, mas as conversões com suporte correspondem conversões implícitas do SQL Server. Independentemente se a tabela de destino a ser carregado é definida como uma tabela distribuída ou replicada, as conversões implícitas são aplicadas (se necessário) para todas as colunas que existem na tabela de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Crie o banco de dados de preparo.|[Criar o banco de dados de preparo](staging-database.md)|  
|Carregar com o Integration Services.|[Carregar com o Integration Services](load-with-ssis.md)|  
|Entenda as conversões de tipo de dwloader.|[Regras de conversão de tipo de dados do dwloader](dwloader-data-type-conversion-rules.md)|  
|Carregar dados com dwloader.|[Carregador de linha de comando do dwloader](dwloader.md)|  
|Entenda as conversões de tipo de inserção.|[Carregar dados com INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
