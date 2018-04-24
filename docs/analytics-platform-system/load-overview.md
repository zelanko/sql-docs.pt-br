---
title: Carregando dados em Parallel Data Warehouse | Microsoft Docs
description: Você pode carregar ou inserir dados no SQL Server Parallel Data Warehouse (PDW) usando o utilitário bcp, Integration Services, dwloader ou a instrução SQL INSERT.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3fed89686683616164132cf0322e3709eab78f32
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Carregando dados em Parallel Data Warehouse
Você pode carregar ou inserir dados no SQL Server Parallel Data Warehouse (PDW) usando o Integration Services, [utilitário bcp](../tools/bcp-utility.md), **dwloader** carregador de linha de comando ou a instrução SQL INSERT.  

## <a name="loading-environment"></a>Ambiente de carregamento  
Para carregar dados, você precisa de um ou mais servidores de carregamento. Você pode usar seu próprio ETL existente ou outros servidores, ou você pode adquirir novos servidores. Para obter mais informações, consulte [adquirir e configurar um servidor ao carregar](acquire-and-configure-loading-server.md). Essas instruções incluem um [carregar planilha de planejamento de capacidade de servidor](loading-server-capacity-planning-worksheet.md) para ajudá-lo a planejar a solução certa para carregamento.  
  
## <a name="load-with-dwloader"></a>Carregar com dwloader  
Usando o [dwloader carregador de linha de comando](dwloader.md) é a maneira mais rápida para carregar dados no PDW.  
  
![Processo de carregamento](media/loading-process.png "processo de carregamento")  
  
dwloader carrega dados diretamente para os nós de computação sem passar os dados por meio do nó de controle. Para carregar dados, dwloader primeiro se comunica com o nó de controle para obter informações de contato para os nós de computação. dwloader configura um canal de comunicação com cada nó de computação e, em seguida, envia partes de 256KB de dados para os nós de computação de forma round robin.  
  
Em cada nó de computação, o serviço de movimentação de dados (DMS) recebe e processa as partes dos dados. Processamento de dados inclui converter cada linha em formato nativo do SQL Server e calcular o hash de distribuição para determinar o nó de computação para o qual cada linha pertence.  
  
Depois de processar as linhas, DMS usa uma movimentação de ordem aleatória para transferir a cada linha para o nó de computação correto e a instância do SQL Server. Como o SQL Server recebe as linhas, lotes-los de acordo com o **– b** definir o parâmetro tamanho do lote na dwloader e, em seguida, em massa carrega o lote.  

## <a name="load-with-prepared-statements"></a>Carregar com instruções preparadas

Você pode usar as instruções preparadas para carregar dados em tabelas replicadas e distribuídas. Quando os dados de entrada não coincide com o tipo de dados de destino, uma conversão implícita é executada. As conversões implícitas com suporte pelo PDW instruções preparadas são um subconjunto das conversões suportadas pelo SQL Server. Ou seja, apenas um subconjunto de conversões têm suporte, mas as conversões com suporte correspondem conversões implícitas do SQL Server. Independentemente se a tabela de destino a ser carregado é definida como uma tabela replicada ou distribuída, conversões implícitas são aplicadas (se necessário) para todas as colunas existentes na tabela de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Description|  
|--------|---------------|  
|Crie o banco de dados de preparo.|[Criar o banco de dados de preparo](staging-database.md)|  
|Carregar serviços de integração.|[Carregar com o Integration Services](load-with-ssis.md)|  
|Entenda as conversões de tipo para dwloader.|[Regras de conversão de tipo de dados do dwloader](dwloader-data-type-conversion-rules.md)|  
|Carregar dados com dwloader.|[Carregador de linha de comando de dwloader](dwloader.md)|  
|Entenda as conversões de tipo para inserção.|[Carregar dados com INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
