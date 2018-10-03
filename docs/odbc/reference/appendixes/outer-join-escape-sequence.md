---
title: Sequência de Escape de junção externa | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba08d33efca6fa90531f89bd57a307f42f343ebd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817580"
---
# <a name="outer-join-escape-sequence"></a>Sequência de escape de junção externa
ODBC usa sequências de escape de junções externas. A sintaxe dessa sequência de escape é da seguinte maneira:  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é:  
  
 *Outer-join-escape ODBC* :: =  
  
 *Iniciador do ODBC-esc* oj *junção externa ODBC esc terminador*  
  
 *junção externa* :: = *nome da tabela* [*nome de correlação*] {esquerda &#124; direita &#124; completo}  
  
 JUNÇÃO externa {*nome da tabela* [*nome de correlação*] &#124; *junção externa*} ON  
  
 *pesquisa-*  
  
 *Condição*  
  
 *nome de correlação* :: = *nome definido pelo usuário*  
  
 *Iniciador do ODBC-esc* :: = {  
  
 *Terminador de esc ODBC* :: =}  
  
 Para determinar quais partes dessa instrução têm suporte, um aplicativo chama **SQLGetInfo** com o tipo de informação SQL_OJ_CAPABILITIES. Junções externas, *critério de pesquisa* deve conter apenas a condição de junção entre especificado *nomes de tabela*.
