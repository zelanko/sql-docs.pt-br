---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14e593ef1dba6a6bed7c5d8a7a1fa42e642ee7d7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428365"
---
# <a name="mssqlserver10737"></a>MSSQLSERVER_10737
    
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
  
  
