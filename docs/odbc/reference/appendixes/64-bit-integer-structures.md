---
title: Estruturas de inteiro de 64 bits | Microsoft Docs
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
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f397923b652bf889dae70e14c39e2f3a8865c7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905321"
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
