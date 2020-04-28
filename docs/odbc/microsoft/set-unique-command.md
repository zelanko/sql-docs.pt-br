---
title: Definir comando exclusivo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d3d37509450d1305891100b37bfd1ad026166e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300836"
---
# <a name="set-unique-command"></a>Comando SET UNIQUE
Especifica se os registros com valores de chave de índice duplicados são mantidos em um arquivo de índice.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 Especifica que qualquer registro com um valor de chave de índice duplicado não seja incluído no arquivo de índice. Somente o primeiro registro com o valor da chave de índice original é incluído no arquivo de índice.  
  
 OFF  
 (Padrão.) Especifica que os registros com valores de chave de índice duplicados sejam incluídos no arquivo de índice.  
  
## <a name="remarks"></a>Comentários  
 Um arquivo de índice mantém sua configuração SET UNIQUE quando você emite reindexação. Para obter mais informações, consulte [index](../../odbc/microsoft/index-command.md).
