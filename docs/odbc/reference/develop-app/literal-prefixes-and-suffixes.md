---
title: Prefixos e Sufixos Literais | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d52ca54c329353e3d9dc67ca35d89b2d28cedf74
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287978"
---
# <a name="literal-prefixes-and-suffixes"></a>Prefixos e sufixos de literais
Em uma declaração SQL, um *literal* é uma representação de caráter de um valor de dados real. Por exemplo, na seguinte declaração, ABC, FFFF e 10 são literais:  
  
```  
SELECT CharCol, BinaryCol, IntegerCol FROM MyTable  
   WHERE CharCol = 'ABC' AND BinaryCol = 0xFFFF AND IntegerCol = 10  
```  
  
 Literais para alguns tipos de dados requerem prefixos e sufixos especiais. No exemplo anterior, o caractere literal (ABC) requer uma única marca de cotação (') como prefixo e sufixo, o literal binário (FFFF) requer os caracteres 0x como prefixo, e o inteiro literal (10) não requer um prefixo ou sufixo.  
  
 Para todos os tipos de dados, exceto data, hora e carimbo sumário, os aplicativos interoperáveis devem usar os valores retornados nas colunas LITERAL_PREFIX e LITERAL_SUFFIX no conjunto de resultados criado pelo **SQLGetTypeInfo**. Para literações de data, hora, carimbo de tempo e intervalo de data, os aplicativos interoperáveis devem usar as seqüências de fuga discutidas na seção anterior.
