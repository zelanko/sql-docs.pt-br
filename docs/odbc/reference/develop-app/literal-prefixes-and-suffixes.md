---
title: Literais prefixos e sufixos | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915562"
---
# <a name="literal-prefixes-and-suffixes"></a>Prefixos e sufixos de literais
Em uma instrução SQL, uma *literal* é uma representação de caractere de um valor de dados reais. Por exemplo, a instrução a seguir, ABC, FFFF e 10 são literais:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literais para alguns tipos de dados exigem especiais prefixos e sufixos. No exemplo anterior, o literal de caractere (ABC) requer uma marca de aspas simples (') como um prefixo e um sufixo, o literal binário (FFFF) exige que os caracteres 0x como um prefixo e o literal de inteiro (10) não exige um prefixo ou sufixo.  
  
 Para todos os tipos de dados, exceto os carimbos de hora de data e hora, aplicativos interoperáveis devem usar os valores retornados nas colunas no conjunto de resultados criados pelo LITERAL_PREFIX e LITERAL_SUFFIX **SQLGetTypeInfo**. Data, hora, carimbo de hora e literais de intervalo de data e hora, os aplicativos interoperáveis devem usar as sequências de escape discutidas na seção anterior.
