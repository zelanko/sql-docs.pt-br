---
title: "Sequência de Escape de junção externa | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d208b7de815f090e5f61d3d807912c53c4253e31
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="outer-join-escape-sequence"></a>Sequência de Escape de junção externa
ODBC usa sequências de escape de junções externas. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *ODBC-outer-join-escape* :: =  
  
 *Iniciador de esc ODBC* oj *junção externa ODBC esc terminador*  
  
 *junção externa* :: = *nome de tabela* [*nome de correlação*] {esquerda &#124; DIREITA &#124; COMPLETO}  
  
 OUTER JOIN {*nome de tabela* [*nome de correlação*] &#124; *junção externa*} ON  
  
 *pesquisa-*  
  
 *condição*  
  
 *nome de correlação* :: = *nome definido pelo usuário*  
  
 *Iniciador de esc ODBC* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar quais partes dessa instrução têm suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_OJ_CAPABILITIES. Junções externas, *critério de pesquisa* deve conter apenas a condição de junção entre especificado *nomes de tabela*.

