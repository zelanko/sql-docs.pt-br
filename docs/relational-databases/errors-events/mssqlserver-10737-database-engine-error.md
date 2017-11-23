---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44e9b7014746f35ece1c48d4542d284c69d158d1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|10737|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|Texto da mensagem|Em uma instrução ALTER TABLE REBUILD ou ALTER INDEX REBUILD, quando uma partição é especificada em uma cláusula DATA_COMPRESSION, especifique PARTITION=ALL. A cláusula PARTITION=ALL é usada para reforçar que todas as partições da tabela ou do índice serão reconstruídas, mesmo que apenas um subconjunto seja especificado na cláusula DATA_COMPRESSION.|  
  
## <a name="user-action"></a>Ação do usuário  
Adicione a cláusula PARTITION=ALL à instrução ALTER TABLE ou ALTER INDEX. Se preferir, recompile uma partição específica e use REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF}).  
  
