---
title: MSSQLSERVER_10737 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10737 (Database Engine error)
ms.assetid: 208af6ed-b271-4ab8-803e-7666025385c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 12d33f5618d4f1478f5e09df536b2f0c695ddddc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781377"
---
# <a name="mssqlserver_10737"></a>MSSQLSERVER_10737
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|MSSQLSERVER|  
|ID do evento|10737|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REBUILD_PARTITION_ALL_NOT_SPECIFIED|  
|Texto da mensagem|Em uma instrução ALTER TABLE REBUILD ou ALTER INDEX REBUILD, quando uma partição é especificada em uma cláusula DATA_COMPRESSION, especifique PARTITION=ALL. A cláusula PARTITION=ALL é usada para reforçar que todas as partições da tabela ou do índice serão reconstruídas, mesmo que apenas um subconjunto seja especificado na cláusula DATA_COMPRESSION.|  
  
## <a name="user-action"></a>Ação do usuário  
Adicione a cláusula PARTITION=ALL à instrução ALTER TABLE ou ALTER INDEX. Se preferir, recompile uma partição específica e use REBUILD PARTITION = \<partition-number-expr> WITH (DATA_COMPRESSION={ON | OFF}).  
  
