---
title: Prefixos e sufixos literais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 56ee50071f622c114bd6d8d04444e78c0fb69d67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915562"
---
# <a name="literal-prefixes-and-suffixes"></a>Prefixos e sufixos de literais
Em uma instrução SQL, um *literal* é uma representação de caractere de um valor de dados real. Por exemplo, na instrução a seguir, ABC, FFFF e 10 são literais:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Os literais para alguns tipos de dados exigem prefixos e sufixos especiais. No exemplo anterior, o literal de caractere (ABC) requer uma aspa simples (') como um prefixo e um sufixo, o literal binário (FFFF) requer os caracteres 0x como um prefixo e o literal inteiro (10) não requer um prefixo ou sufixo.  
  
 Para todos os tipos de dados, exceto Date, time e carimbos de data/hora, os aplicativos interoperáveis devem usar os valores retornados nas colunas LITERAL_PREFIX e LITERAL_SUFFIX no conjunto de resultados criado por **SQLGetTypeInfo**. Para os literais data, time, timestamp e DateTime Interval, os aplicativos interoperáveis devem usar as sequências de escape discutidas na seção anterior.
