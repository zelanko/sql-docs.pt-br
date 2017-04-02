---
title: "Li&#231;&#227;o 1: Convertendo uma tabela em uma estrutura hier&#225;rquica | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "HierarchyID"
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Li&#231;&#227;o 1: Convertendo uma tabela em uma estrutura hier&#225;rquica
Os clientes que possuem tabelas que usam autojunções para expressar relações hierárquicas podem converter as tabelas em uma estrutura hierárquica usando esta lição como guia. É relativamente fácil fazer a migração dessa representação para outra usando **hierarchyid**. Depois da migração, os usuários terão uma representação hierárquica compacta e fácil de entender, que poderá ser indexada de várias formas para proporcionar consultas eficientes.  
  
Esta lição examina uma tabela existente, cria uma tabela contendo uma coluna **hierarchyid** , popula a tabela com os dados da tabela de origem e, depois, demonstra três estratégias de indexação. Eis os tópicos desta lição:  
  
-   [Examinando a estrutura atual da tabela Employee](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
-   [Populando uma tabela com dados hierárquicos existentes](../../relational-databases/tables/populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Otimizando a tabela NewOrg](../../relational-databases/tables/optimizing-the-neworg-table.md)  
  
-   [Resumo: convertendo uma tabela para uma estrutura hierárquica](../../relational-databases/tables/summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## Pré-requisitos  
Esta lição exige o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
## Próxima tarefa da lição  
[Examinando a estrutura atual da tabela Employee](../../relational-databases/tables/examining-the-current-structure-of-the-employee-table.md)  
  
## Próxima lição  
[Lição 2: Criando e gerenciando dados em uma tabela hierárquica](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  
