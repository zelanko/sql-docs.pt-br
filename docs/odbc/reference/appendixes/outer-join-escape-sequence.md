---
title: Sequência de fuga de adesão externa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303607"
---
# <a name="outer-join-escape-sequence"></a>Sequência de escape de junção externa
ODBC usa seqüências de fuga para junções externas. A sintaxe desta seqüência de fuga é a seguinte:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação da BNF, a sintaxe é a seguinte:  
  
 *ODBC-outer-join-escape* ::=  
  
 *ODBC-esc-iniciador* oj *outer-join ODBC-esc-terminator*  
  
 *externa-juntar::=* *nome da tabela* *[correlação-nome*] {ESQUERDA &#124; DIREITA &#124; FULL}  
  
 OUTER JOIN{*nome de tabela* *[nome de correlação*] &#124; *adesão externa*} ON  
  
 *pesquisa-*  
  
 *Condição*  
  
 *nome de correlação* ::= *nome definido pelo usuário*  
  
 *ODBC-esc-iniciador* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar quais partes desta declaração são suportadas, um aplicativo chama **SQLGetInfo** com o SQL_OJ_CAPABILITIES tipo de informação. Para as adesões externas, *a condição de pesquisa* deve conter apenas a condição de adesão entre os nomes de *tabela*especificados .
