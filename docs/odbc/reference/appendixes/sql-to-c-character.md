---
description: 'SQL para C: caractere'
title: 'SQL to C: Character | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dff2b456e995aa344fcd928a48a5aaa09c484e89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456524"
---
# <a name="sql-to-c-character"></a>SQL para C: caractere

Os identificadores para os tipos de dados SQL ODBC de caracteres são os seguintes:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de caractere podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Comprimento de bytes de dados < *BufferLength*<br /><br /> Comprimento de bytes de dados >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Comprimento de caracteres de < de dados *BufferLength*<br /><br /> Comprimento de caracteres dos dados >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Dados convertidos sem truncamento [b]<br /><br /> Dados convertidos com truncamento de dígitos fracionários [a]<br /><br /> A conversão de dados resultaria em perda de dígitos inteiros (em oposição a fracionários) [a]<br /><br /> Os dados não são um *literal numérico*[b]|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Número de bytes do tipo de dados C<br /><br /> Número de bytes do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Os dados estão dentro do intervalo do tipo de dados ao qual o número está sendo convertido [a]<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido [a]<br /><br /> Os dados não são um *literal numérico*[b]|Dados<br /><br /> Indefinido<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menores que 2 e não iguais a 1<br /><br /> Os dados são menores que 0 ou maiores ou iguais a 2<br /><br /> Os dados não são um *literal numérico*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|1 [b]<br /><br /> 1 [b]<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|O valor dos dados é um *valor de data*válido [a]<br /><br /> O valor dos dados é um *valor de carimbo de data/hora*válido; a parte de hora é zero [a]<br /><br /> O valor dos dados é um *valor de carimbo de data/hora*válido; a parte de hora é diferente de zero [a], [c]<br /><br /> O valor dos dados não é um *valor de data* / *hora*válido|Dados<br /><br /> Dados<br /><br /> Dados truncados<br /><br /> Indefinido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|O valor dos dados é um valor *de hora válido e o valor de segundos fracionários é 0*[a]<br /><br /> O valor dos dados é um *valor de carimbo de data/hora válido ou um valor de tempo válido*; a parte de segundos fracionários é zero [a], [d]<br /><br /> O valor dos dados é um *valor de carimbo de data/hora*válido; a parte de segundos fracionários é diferente de zero [a], [d], [e]<br /><br /> O valor dos dados não é um valor *de tempo* / *carimbo de data/* hora válido [a]|Dados<br /><br /> Dados<br /><br /> Dados truncados<br /><br /> Indefinido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|O valor dos dados é um *valor de carimbo de data/hora válido ou um valor de tempo válido*; parte de segundos fracionários não truncada [a]<br /><br /> O valor dos dados é um *valor de carimbo de data/hora válido ou um valor de tempo válido*; parte de segundos fracionários truncada [a]<br /><br /> O valor dos dados é um *valor de data*válido [a]<br /><br /> O valor dos dados é um *valor de tempo*válido [a]<br /><br /> O valor dos dados não é um *valor de data/* hora válido, *tempo-* valor ou um *valor de timestamp*[a]|Dados<br /><br /> Dados truncados<br /><br /> Dados [f]<br /><br /> Dados [g]<br /><br /> Indefinido|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo de C|O valor dos dados é um *valor de intervalo*válido; sem truncamento<br /><br /> O valor dos dados é um *valor de intervalo*válido; truncamento de um ou mais campos à direita<br /><br /> Os dados são um intervalo válido; a precisão significativa do campo principal é perdida<br /><br /> O valor dos dados não é um valor de intervalo válido|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.  
  
 [c] a parte de tempo do *carimbo de data/* hora do valor é truncada.  
  
 [d] a parte de data do *carimbo-hora-valor* é ignorada.  
  
 [e] a parte de segundos fracionários do carimbo de data/hora está truncada.  
  
 [f] os campos de tempo da estrutura do carimbo de data/hora são definidos como zero.  
  
 [g] os campos de data da estrutura de carimbo de data/hora são definidos como a data atual.  

**Espaços extras**

Espaços à esquerda e à direita são ignorados quando os dados de caracteres SQL são convertidos em qualquer um dos seguintes tipos:

- date
- numeric
- time
- timestamp
- dados do intervalo C
