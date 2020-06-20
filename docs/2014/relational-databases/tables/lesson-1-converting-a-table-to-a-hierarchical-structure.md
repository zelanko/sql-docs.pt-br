---
title: 'Lição 1: Convertendo uma tabela em uma estrutura hierárquica | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd6f1d123bca9f9f0c10288e0b58dd075c7b0949
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068056"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lição 1: Convertendo uma tabela em uma estrutura hierárquica
  Os clientes que possuem tabelas que usam autojunções para expressar relações hierárquicas podem converter as tabelas em uma estrutura hierárquica usando esta lição como guia. É relativamente fácil fazer a migração dessa representação para outra usando `hierarchyid`. Depois da migração, os usuários terão uma representação hierárquica compacta e fácil de entender, que poderá ser indexada de várias formas para proporcionar consultas eficientes.  
  
 Esta lição examina uma tabela existente, cria uma tabela contendo uma coluna `hierarchyid`, popula a tabela com os dados da tabela de origem e, depois, demonstra três estratégias de indexação. Eis os tópicos desta lição:  
  
-   [Examinando a estrutura atual da tabela Employee](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [Populando uma tabela com dados hierárquicos existentes](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [Otimizando a tabela NewOrg](lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [Resumo: conversão de uma tabela em uma estrutura hierárquica](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Esta lição exige o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Examinando a estrutura atual da tabela Employee](lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Criando e gerenciando dados em uma tabela hierárquica](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
