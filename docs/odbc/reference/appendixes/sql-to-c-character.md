---
title: 'SQL para C: Caractere | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a649e1ec27261551b7a64e09310ce99b6140a15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056917"
---
# <a name="sql-to-c-character"></a>SQL para C: Caractere

Os identificadores para os tipos de dados SQL ODBC caracteres são os seguintes:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

A tabela a seguir mostra os tipos de dados para o qual os dados SQL de caractere podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Comprimento de bytes de dados < *BufferLength*<br /><br /> Comprimento de bytes de dados > = *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Comprimento dos dados de caractere < *BufferLength*<br /><br /> Comprimento dos dados de caracteres > = *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT  SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT  SQL_C_SLONG SQL_C_ULONG SQL_C_LONG  SQL_C_NUMERIC|Os dados convertidos sem truncamento [b]<br /><br /> Os dados convertidos com truncamento de dígitos fracionários [a]<br /><br /> Conversão de dados pode resultar em perda de dígitos de inteiro (em vez de fracionários) [a]<br /><br /> Dados não não um *literal numérico*[b].|Data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Número de bytes do tipo de dados C<br /><br /> Número de bytes do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Dados estão dentro do intervalo do tipo de dados ao qual o número é convertido [a]<br /><br /> Data está fora do intervalo do tipo de dados ao qual o número é convertido [a]<br /><br /> Dados não não um *literal numérico*[b].|Data<br /><br /> Indefinido<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|Dados são 0 ou 1<br /><br /> Dados forem maiores que 0, menor que 2 e não é igual a 1<br /><br /> Dados são menor que 0 ou maior que ou igual a 2<br /><br /> Dados não não um *literal numérico*|Data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|1[b]<br /><br /> 1[b]<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Valor de dados é válido *valor de data*[a]<br /><br /> Valor de dados é válido *valor de carimbo de hora*; parte de hora é zero [a]<br /><br /> Valor de dados é válido *valor de carimbo de hora*; parte de hora é diferente de zero [a], [c]<br /><br /> Valor de dados não é válido *valor de data* ou *valor de carimbo de hora*[a]|Data<br /><br /> Data<br /><br /> Dados truncados<br /><br /> Indefinido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Valor de dados é válido *valor de hora e os segundos fracionários que o valor é 0*[a]<br /><br /> Valor de dados é válido *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte de segundos é zero [a], [d]<br /><br /> Valor de dados é válido *valor de carimbo de hora*; fracionários parte de segundos é diferente de zero [a], [d] [e]<br /><br /> Valor de dados não é válido *valor de hora* ou *valor de carimbo de hora*[a]|Data<br /><br /> Data<br /><br /> Dados truncados<br /><br /> Indefinido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|Valor de dados é válido *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte segundos não truncado [a]<br /><br /> Valor de dados é válido *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte segundos truncado [a]<br /><br /> Valor de dados é válido *valor de data*[a]<br /><br /> Valor de dados é válido *valor de hora*[a]<br /><br /> Valor de dados não é válido *valor de data*, *valor de tempo*, ou *valor de carimbo de hora*[a]|Data<br /><br /> Dados truncados<br /><br /> Dados [f]<br /><br /> Dados [g]<br /><br /> Indefinido|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo de C|Valor de dados é válido *o valor de intervalo*; não há truncamento<br /><br /> Valor de dados é válido *o valor de intervalo*; o truncamento de um ou mais campos à direita<br /><br /> Dados são o intervalo válido. precisão significativa do campo inicial for perdida<br /><br /> O valor de dados não é um valor de intervalo válido|Data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] esse é o tamanho do tipo de dados C correspondente.  
  
 [c] a parte de hora a *valor de carimbo de hora* será truncado.  
  
 [d] a parte da data a *valor de carimbo de hora* será ignorado.  
  
 [e] parte fracionária de segundos do carimbo de hora será truncado.  
  
 [f] os campos de hora da estrutura de carimbo de hora são definidos como zero.  
  
 [g] os campos de data da estrutura de carimbo de hora são definidos como a data atual.  

**Espaços extras**

Espaços à direita e são ignoradas quando os dados de caractere SQL são convertidos em qualquer um dos seguintes tipos:

- date
- numeric
- time
- timestamp
- dados de intervalo C
