---
title: "Limitações de instrução ALTER tabela | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c50ea6550e9dfb255c87886e4e0375240bcd2ae
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="alter-table-statement-limitations"></a>Limitações de declaração de tabela de alteração
Quando o driver Paradox ou dBASE é usado, depois que um índice foi criado e adicionado um novo registro, a estrutura da tabela não pode ser alterada pela instrução ALTER TABLE, a menos que o índice é descartado e o conteúdo da tabela será excluído.  
  
 Não há suporte para instruções ALTER TABLE para os drivers de texto ou do Microsoft Excel.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o mecanismo de banco de dados Borland, não há suporte para instruções ALTER TABLE; somente leitura e acrescente as instruções são permitidas.

