---
title: Limitações de instrução ALTER tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be0319a29c0193d460e9ce54616897de3d940443
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32897831"
---
# <a name="alter-table-statement-limitations"></a>Limitações de declaração de tabela de alteração
Quando o driver Paradox ou dBASE é usado, depois que um índice foi criado e adicionado um novo registro, a estrutura da tabela não pode ser alterada pela instrução ALTER TABLE, a menos que o índice é descartado e o conteúdo da tabela será excluído.  
  
 Não há suporte para instruções ALTER TABLE para os drivers de texto ou do Microsoft Excel.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não há suporte para instruções ALTER TABLE; somente leitura e acrescente as instruções são permitidas.
