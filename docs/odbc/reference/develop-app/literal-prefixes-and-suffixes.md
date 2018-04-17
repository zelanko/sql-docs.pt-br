---
title: Literal prefixos e sufixos | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d1d836c086747cba5b42b0db5a1919575afcfaa2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="literal-prefixes-and-suffixes"></a>Literal prefixos e sufixos
Em uma instrução SQL, uma *literal* é uma representação de caracteres de um valor de dados reais. Por exemplo, a instrução a seguir, ABC, FFFF e 10 são literais:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literais para alguns tipos de dados exigem especiais prefixos e sufixos. No exemplo anterior, o literal de caractere (ABC) requer uma aspa simples (') como um prefixo e um sufixo, o literal binário (FFFF) requer que os caracteres 0x como um prefixo e o literal de inteiro (10) não exige um prefixo ou sufixo.  
  
 Para todos os tipos de dados exceto data, hora e os carimbos de hora, aplicativos interoperáveis devem usar os valores retornados nas colunas no conjunto de resultados criados pelo LITERAL_PREFIX e LITERAL_SUFFIX **SQLGetTypeInfo**. Data, hora, timestamp e literais de intervalo de data e hora, aplicativos interoperáveis devem usar as sequências de escape discutidas na seção anterior.
