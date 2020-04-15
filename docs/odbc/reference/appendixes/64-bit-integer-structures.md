---
title: Estruturas de inteiros de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ecbe4dae4c1bd21ac3d542ee0d9b18169df0116
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307507"
---
# <a name="64-bit-integer-structures"></a>Estruturas de inteiro de 64 bits
O tipo C para os identificadores de SQL_C_SBIGINT e SQL_C_UBIGINT do tipo de dados nos compiladores Microsoft C é _int64. Quando um compilador diferente de um compilador C ® Microsoft é usado, o tipo C pode ser diferente. Se o compilador suportar inteiros de 64 bits nativamente, o driver ou aplicativo deve definir ODBCINT64 como o tipo inteiro nativo de 64 bits. Se o compilador não suportar inteiros de 64 bits nativamente, um aplicativo ou driver pode definir as seguintes estruturas para garantir que ele tenha acesso a esses dados:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 Essas estruturas devem ser alinhadas a um limite de 8 bytes porque um inteiro de 64 bits está alinhado ao limite de 8 bytes.
