---
title: Literal prefixos e sufixos | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], literal prefixes and suffixes
- literals [ODBC], prefixes and suffixes
ms.assetid: 29f468f2-f557-4a92-b31d-569c63cc6272
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ab92444e7d7c72063a1276c21acd5943ae649e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910601"
---
# <a name="literal-prefixes-and-suffixes"></a>Literal prefixos e sufixos
Em uma instrução SQL, uma *literal* é uma representação de caracteres de um valor de dados reais. Por exemplo, a instrução a seguir, ABC, FFFF e 10 são literais:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literais para alguns tipos de dados exigem especiais prefixos e sufixos. No exemplo anterior, o literal de caractere (ABC) requer uma aspa simples (') como um prefixo e um sufixo, o literal binário (FFFF) requer que os caracteres 0x como um prefixo e o literal de inteiro (10) não exige um prefixo ou sufixo.  
  
 Para todos os tipos de dados exceto data, hora e os carimbos de hora, aplicativos interoperáveis devem usar os valores retornados nas colunas no conjunto de resultados criados pelo LITERAL_PREFIX e LITERAL_SUFFIX **SQLGetTypeInfo**. Data, hora, timestamp e literais de intervalo de data e hora, aplicativos interoperáveis devem usar as sequências de escape discutidas na seção anterior.
