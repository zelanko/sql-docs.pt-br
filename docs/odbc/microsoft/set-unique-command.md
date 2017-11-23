---
title: Comando exclusivo do conjunto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6c028638a17d5b6ba98b2d0b9cf41de9549484e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="set-unique-command"></a>Comando exclusivo do conjunto
Especifica se os registros com valores de chave duplicados de índice são mantidos em um arquivo de índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que qualquer registro com um valor de chave de índice duplicados não serão incluídas no arquivo de índice. Apenas o primeiro registro com o valor original da chave de índice está incluído no arquivo de índice.  
  
 OFF  
 (Padrão). Especifica que os registros com valores de chave de índice duplicados serão incluídas no arquivo de índice.  
  
## <a name="remarks"></a>Comentários  
 Um arquivo de índice retém sua configuração de exclusivo definido quando você emitir a REINDEXAÇÃO. Para obter mais informações, consulte [índice](../../odbc/microsoft/index-command.md).
