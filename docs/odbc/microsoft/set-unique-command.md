---
title: Comando SET UNIQUE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063611"
---
# <a name="set-unique-command"></a>Comando SET UNIQUE
Especifica se os registros com valores de chave de índice duplicados são mantidos em um arquivo de índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que qualquer registro com um valor de chave de índice duplicados não sejam incluídos no arquivo de índice. O primeiro registro com o valor de chave de índice original está incluído no arquivo de índice.  
  
 OFF  
 (Padrão). Especifica que os registros com valores de chave de índice duplicados sejam incluídos no arquivo de índice.  
  
## <a name="remarks"></a>Comentários  
 Um arquivo de índice retém sua configuração de conjunto exclusivo quando você emitir a REINDEXAÇÃO. Para obter mais informações, consulte [índice](../../odbc/microsoft/index-command.md).
