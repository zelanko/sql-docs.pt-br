---
title: Estruturas de inteiro de 64 bits | Microsoft Docs
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
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b267e536535d0df75e1f7c048baa31099c97a704
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="64-bit-integer-structures"></a>Estruturas de inteiro de 64 bits
O tipo de C para os identificadores de tipo de dados SQL_C_SBIGINT e SQL_C_UBIGINT na Microsoft C compiladores é _int64. Quando um compilador que um compilador Microsoft® C é usado, o tipo C pode ser diferente. Se o compilador dá suporte a inteiros de 64 bits nativo, o driver ou o aplicativo deve definir ODBCINT64 para ser do tipo inteiro de 64 bits nativo. Se o compilador não oferecer suporte a inteiros de 64 bits nativo, um aplicativo ou driver pode definir as estruturas a seguir para garantir que ele tenha acesso a esses dados:  
  
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
  
 Essas estruturas devem ser alinhadas a um limite de 8 bytes, como um inteiro de 64 bits é alinhado com o limite de 8 bytes.
