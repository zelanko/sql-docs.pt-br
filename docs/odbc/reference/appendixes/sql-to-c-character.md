---
title: 'SQL em c: caractere | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db139b1307fa1817e0b9ed709be5ee5db2086756
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-character"></a>SQL em c: caractere
Os identificadores para os tipos de dados SQL ODBC caracteres são:  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 A tabela a seguir mostra o ODBC C para o qual os dados SQL de caractere podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Comprimento em bytes de dados < *BufferLength*<br /><br /> Comprimento em bytes de dados > = *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Comprimento dos dados de caracteres < *BufferLength*<br /><br /> Comprimento dos dados de caracteres > = *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Os dados convertidos sem truncamento [b]<br /><br /> Os dados convertidos com truncamento de dígitos fracionários [a]<br /><br /> Conversão de dados pode resultar em perda de dígitos de inteiro (em vez de frações) [a]<br /><br /> Dados não são um *literal numérico*[b].|data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Número de bytes do tipo de dados C<br /><br /> Número de bytes do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Dados estão dentro do intervalo do tipo de dados ao qual o número é convertido [a]<br /><br /> Dados estão fora do intervalo do tipo de dados ao qual o número é convertido [a]<br /><br /> Dados não são um *literal numérico*[b].|data<br /><br /> Indefinido<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|Dados são 0 ou 1<br /><br /> Dados for maiores que 0, menor que 2 e não é igual a 1<br /><br /> Dados são menor que 0 ou maior que ou igual a 2<br /><br /> Dados não são um *literal numérico*|data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|1 [b]<br /><br /> 1 [b]<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Valor de dados é uma opção válida *valor de data*[a]<br /><br /> Valor de dados é uma opção válida *valor de carimbo de hora*; parte de hora for zero [a]<br /><br /> Valor de dados é uma opção válida *valor de carimbo de hora*; parte de hora é diferente de zero [a], [c]<br /><br /> Valor de dados não é válido *valor de data* ou *valor de carimbo de hora*[a]|data<br /><br /> data<br /><br /> Dados truncados<br /><br /> Indefinido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Valor de dados é uma opção válida *valor de tempo e as frações de segundo valor é 0*[a]<br /><br /> Valor de dados é uma opção válida *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte de segundos é zero [a], [d]<br /><br /> Valor de dados é uma opção válida *valor de carimbo de hora*; fracionários parte de segundos é diferente de zero [a], [d] [e]<br /><br /> Valor de dados não é válido *valor de hora* ou *valor de carimbo de hora*[a]|data<br /><br /> data<br /><br /> Dados truncados<br /><br /> Indefinido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|Valor de dados é uma opção válida *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte segundos não truncado [a]<br /><br /> Valor de dados é uma opção válida *valor de carimbo de hora ou um valor de tempo válido*; fracionários parte segundos truncado [a]<br /><br /> Valor de dados é uma opção válida *valor de data*[a]<br /><br /> Valor de dados é uma opção válida *valor de hora*[a]<br /><br /> Valor de dados não é válido *valor de data*, *valor de hora*, ou *valor de carimbo de hora*[a]|data<br /><br /> Dados truncados<br /><br /> Dados [f]<br /><br /> Dados [g]<br /><br /> Indefinido|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo de C|Valor de dados é uma opção válida *o valor de intervalo*; sem truncamento<br /><br /> Valor de dados é uma opção válida *o valor de intervalo*; truncamento de um ou mais campos à direita<br /><br /> Os dados são o intervalo válido. precisão significativa do campo principal é perdido<br /><br /> O valor de dados não é um valor do intervalo válido|data<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] este é o tamanho do tipo de dados C correspondente.  
  
 [c] a parte da hora de *valor de carimbo de hora* será truncado.  
  
 [d] a parte da data de *valor de carimbo de hora* será ignorado.  
  
 [e] parte fracionária de segundos do carimbo de hora é truncado.  
  
 [f] os campos de hora da estrutura de carimbo de hora são definidos como zero.  
  
 [g] os campos de data da estrutura de carimbo de hora são definidos como a data atual.  
  
 Quando dados de SQL de caractere são convertidos em numérico, data, hora, timestamp ou dados de intervalo C, espaços à direita e são ignorados.
