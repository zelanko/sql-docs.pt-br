---
title: Estruturas de inteiro de 64 bits | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac1a80e94d225b26cf879b27bdb0e138e0b0d1d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306328"
---
# <a name="64-bit-integer-structures"></a>Estruturas de inteiro de 64 bits
O tipo de C para os identificadores de tipo de dados SQL_C_SBIGINT e SQL_C_UBIGINT nos compiladores Microsoft C é _int64. Quando um compilador em vez de um compilador C da Microsoft® é usado, o tipo C pode ser diferente. Se o compilador dá suporte a inteiros de 64 bits nativamente, o driver ou o aplicativo deve definir ODBCINT64 para ser do tipo inteiro de 64 bits nativo. Se o compilador não dá suporte nativamente inteiros de 64 bits, um aplicativo ou driver pode definir as estruturas a seguir para garantir que ele tenha acesso a esses dados:  
  
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
  
 Essas estruturas devem ser alinhadas a um limite de 8 bytes, como um inteiro de 64 bits é alinhado ao limite de 8 bytes.
