---
title: Sequência de escape de junção externa | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303607"
---
# <a name="outer-join-escape-sequence"></a>Sequência de escape de junção externa
O ODBC usa sequências de escape para junções externas. A sintaxe dessa sequência de escape é a seguinte:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é a seguinte:  
  
 *ODBC-externo-junção-escape* :: =  
  
 *ODBC-ESC-Initiator* OJ *externo-junção ODBC-ESC-terminador*  
  
 *externa-junção* :: = *table-name* [*correlação-nome*] {Left &#124; direita &#124; Full}  
  
 JUNÇÃO externa {*table-name* [*Correlation-Name*] &#124; *OUTER-JOIN*} on  
  
 *procurando*  
  
 *problema*  
  
 *correlação-nome* :: = *nome definido pelo usuário*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-terminador* :: =}  
  
 Para determinar quais partes dessa instrução têm suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_OJ_CAPABILITIES. Para junções externas, a *condição de pesquisa* deve conter apenas a condição de junção entre os *nomes de tabela*especificados.
