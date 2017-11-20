---
title: "Dígitos decimais | Microsoft Docs"
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
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4593b1faacfc235ce0ee5c54bc9ca70416444f5e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="decimal-digits"></a>Dígitos decimais
O *dígitos decimais* de dados decimais e numéricos tipos é definido como o número máximo de dígitos à direita da vírgula decimal, ou a escala dos dados. Para parâmetros ou colunas de número de ponto flutuantes aproximadas, a escala é indefinida porque o número de dígitos à direita da vírgula decimal não é fixo. Para datetime ou intervalo de dados que contém um componente de segundos, os dígitos decimais é definido como o número de dígitos à direita da vírgula decimal no componente de segundos de dados.  
  
 Para os tipos de dados SQL_DECIMAL e SQL_NUMERIC, a escala máxima é geralmente o mesmo que a precisão máxima. No entanto, algumas fontes de dados impõem um limite separado para a escala máxima. Para determinar as escalas de mínimas e máxima permitidas para um tipo de dados, um aplicativo chama **SQLGetTypeInfo**.  
  
 Os dígitos decimais definidos para cada tipo de dados SQL conciso é mostrado na tabela a seguir.  
  
|Tipo SQL|Dígitos decimais|  
|--------------|--------------------|  
|Todos os caracteres e tipos binários [a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número definido de dígitos à direita da vírgula decimal. Por exemplo, a escala de uma coluna definida como NUMERIC(10,3) é 3. Isso pode ser um número negativo para dar suporte ao armazenamento de números muito grandes sem usar a notação exponencial; Por exemplo, "12000" podem ser armazenadas como "12" com uma escala de – 3.|  
|Todos os tipos numéricos exatos que não sejam SQL_DECIMAL e SQL_NUMERIC [a]|0|  
|Todos os tipos de dados aproximados [a]|n/d|  
|SQL_TYPE_DATE e todos os tipos de intervalo com nenhum componente de segundos [a]|n/d|  
|Todos os tipos de data e hora, exceto SQL_TYPE_DATE e todos os tipos de intervalo com um componente de segundos|O número de dígitos à direita da vírgula decimal na parte de segundos do valor (frações de segundo). Esse número não pode ser negativo.|  
|SQL_GUID|n/d|  
  
 [a] o *DecimalDigits* argumento de **SQLBindParameter** é ignorada para esse tipo de dados.  
  
 Os valores retornados para os dígitos decimais não correspondem aos valores em qualquer um campo do descritor. Os valores podem vir do SQL_DESC_SCALE ou o campo SQL_DESC_PRECISION, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo de descritor correspondente<br /><br /> dígitos decimais|  
|--------------|----------------------------------------------------------|  
|Todos os caracteres e tipos binários|n/d|  
|Todos os tipos numéricos exatos|SCALE|  
|SQL_BIT|n/d|  
|Todos os tipos numéricos aproximados|n/d|  
|Todos os tipos de data e hora|PRECISION|  
|Todos os tipos de intervalo com um componente de segundos|PRECISION|  
|Todos os tipos de intervalo com nenhum componente de segundos|n/d|

