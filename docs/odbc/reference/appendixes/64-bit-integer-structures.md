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
ms.openlocfilehash: 93d9e6fd01d6b9ef98ebb10f6728ec4ba205fbb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996261"
---
# <a name="64-bit-integer-structures"></a>Estruturas de inteiro de 64 bits
O tipo C para os identificadores de tipo de dados SQL_C_SBIGINT e SQL_C_UBIGINT nos compiladores do Microsoft C é _int64. Quando um compilador diferente de um compilador Microsoft® C é usado, o tipo C pode ser diferente. Se o compilador der suporte a inteiros de 64 bits nativamente, o driver ou aplicativo deverá definir ODBCINT64 para ser o tipo inteiro de 64 bits nativo. Se o compilador não oferecer suporte a inteiros de 64 bits nativamente, um aplicativo ou driver poderá definir as seguintes estruturas para garantir que ele tenha acesso a esses dados:  
  
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
