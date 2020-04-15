---
title: Dígitos decimais | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285156"
---
# <a name="decimal-digits"></a>Dígitos decimais
Os *dígitos decimais* dos tipos de dados decimais e numéricos são definidos como o número máximo de dígitos à direita do ponto decimal, ou a escala dos dados. Para colunas ou parâmetros de número de ponto flutuante aproximados, a escala é indefinida porque o número de dígitos à direita do ponto decimal não é fixo. Para dados de data ou intervalo que contenham um componente de segundos, os dígitos decimais são definidos como o número de dígitos à direita do ponto decimal no componente segundos dos dados.  
  
 Para os tipos de dados SQL_DECIMAL e SQL_NUMERIC, a escala máxima geralmente é a mesma que a precisão máxima. No entanto, algumas fontes de dados impõem um limite separado na escala máxima. Para determinar as escalas mínima e máxima permitidas para um tipo de dados, um aplicativo chama **SQLGetTypeInfo**.  
  
 Os dígitos decimais definidos para cada tipo de dados SQL conciso são mostrados na tabela a seguir.  
  
|Tipo SQL|Dígitos decimais|  
|--------------|--------------------|  
|Todos os tipos de caracteres e binários[a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|O número definido de dígitos à direita do ponto decimal. Por exemplo, a escala de uma coluna definida como NUMERIC(10,3) é 3. Este pode ser um número negativo para suportar o armazenamento de números muito grandes sem usar notação exponencial; por exemplo, "12000" poderia ser armazenado como "12" com uma escala de -3.|  
|Todos os tipos numéricos exatos que não SQL_DECIMAL e SQL_NUMERIC[a]|0|  
|Todos os tipos de dados aproximados[a]|n/d|  
|SQL_TYPE_DATE e todos os tipos de intervalo sem componente de segundos[a]|n/d|  
|Todos os tipos de datas, exceto SQL_TYPE_DATE, e todos os tipos de intervalo com um componente de segundos|O número de dígitos à direita do ponto decimal na parte de segundos do valor (segundos fracionados). Este número não pode ser negativo.|  
|SQL_GUID|n/d|  
  
 [a] O argumento *DecimalDigits* do **SQLBindParameter** é ignorado para este tipo de dados.  
  
 Os valores retornados para os dígitos decimais não correspondem aos valores em qualquer campo descritor. Os valores podem vir tanto do SQL_DESC_SCALE quanto do campo SQL_DESC_PRECISION, dependendo do tipo de dados, conforme mostrado na tabela a seguir.  
  
|Tipo SQL|Campo descritor correspondente a<br /><br /> dígitos decimais|  
|--------------|----------------------------------------------------------|  
|Todos os tipos de caracteres e binários|n/d|  
|Todos os tipos numéricos exatos|SCALE|  
|SQL_BIT|n/d|  
|Todos os tipos numéricos aproximados|n/d|  
|Todos os tipos de data-hora|PRECISION|  
|Todos os tipos de intervalo com um componente de segundos|PRECISION|  
|Todos os tipos de intervalo sem componente de segundos|n/d|
