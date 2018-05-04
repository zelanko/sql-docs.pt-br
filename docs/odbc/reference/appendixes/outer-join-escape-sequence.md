---
title: Sequência de Escape de junção externa | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d7ea1f4a349e2a0207481cb85ab898548bd98d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="outer-join-escape-sequence"></a>Sequência de Escape de junção externa
ODBC usa sequências de escape de junções externas. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Remarks  
 Na notação BNF, a sintaxe é:  
  
 *ODBC-outer-join-escape* :: =  
  
 *Iniciador de esc ODBC* oj *junção externa ODBC esc terminador*  
  
 *junção externa* :: = *nome de tabela* [*nome de correlação*] {esquerda &#124; direita &#124; completo}  
  
 JUNÇÃO externa {*nome de tabela* [*nome de correlação*] &#124; *junção externa*} ON  
  
 *pesquisa-*  
  
 *condição*  
  
 *nome de correlação* :: = *nome definido pelo usuário*  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar quais partes dessa instrução têm suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_OJ_CAPABILITIES. Junções externas, *critério de pesquisa* deve conter apenas a condição de junção entre especificado *nomes de tabela*.
