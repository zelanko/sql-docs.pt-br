---
title: Comando exclusivo do conjunto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbdb92c553b5d4ff3eae3bf0f0c39fa834bcd913
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 Um arquivo de índice retém sua configuração de exclusivo definido quando você emitir a REINDEXAÇÃO. Para obter mais informações, consulte [índice](../../odbc/microsoft/index-command.md).
