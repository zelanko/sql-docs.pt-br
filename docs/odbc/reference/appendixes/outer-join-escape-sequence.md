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
ms.topic: article
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71205972831d4a0370a0905aeaa8f94d9639894e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
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
