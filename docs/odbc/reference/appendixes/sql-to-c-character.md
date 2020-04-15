---
title: 'SQL para C: Personagem | Microsoft Docs'
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
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296666"
---
# <a name="sql-to-c-character"></a>SQL para C: caractere

Os identificadores para os tipos de dados ODBC SQL de caracteresão são os seguintes:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de caracteres podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|Strlen_or_indptr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Comprimento de byte de dados < *BufferLength*<br /><br /> Comprimento de byte de dados >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Comprimento do caractere dos dados < *BufferLength*<br /><br /> Comprimento do caractere dos dados >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Dados convertidos sem truncação[b]<br /><br /> Dados convertidos com truncação de dígitos fracionados[a]<br /><br /> A conversão de dados resultaria em perda de dígitos inteiros (em oposição ao fracionado)[a]<br /><br /> Os dados não são *numéricos-literais*[b]|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Número de bytes do tipo de dados C<br /><br /> Número de bytes do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido[a]<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido[a]<br /><br /> Os dados não são *numéricos-literais*[b]|Dados<br /><br /> Indefinido<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menos de 2, e não são iguais a 1<br /><br /> Os dados são inferiores ou superiores a 0 ou igual a 2<br /><br /> Os dados não são *numéricos-literais*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|1[b]<br /><br /> 1[b]<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Duração dos dados|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|O valor dos dados é um *valor de data*válido [a]<br /><br /> O valor dos dados é um *valor de carimbo de data-hora*válido; porção de tempo é zero[a]<br /><br /> O valor dos dados é um *valor de carimbo de data-hora*válido; porção de tempo não é zero[a],[c]<br /><br /> O valor dos dados não é um *valor de data* válido ou um valor de carimbo de *hora*[a]|Dados<br /><br /> Dados<br /><br /> Dados truncados<br /><br /> Indefinido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|O valor dos dados é um valor de tempo válido *e o valor de segundos fracionados é 0*[a]<br /><br /> O valor dos dados é um *valor de carimbo de data-hora*válido ou um valor de tempo válido; a porção de segundos fracionados é zero[a],[d]<br /><br /> O valor dos dados é um *valor de carimbo de data-hora*válido; a porção de segundos fracionados não é zero[a],[d],[e]<br /><br /> O valor dos dados não é um *valor de tempo* válido ou um valor de carimbo de *hora*[a]|Dados<br /><br /> Dados<br /><br /> Dados truncados<br /><br /> Indefinido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> Indefinido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|O valor dos dados é um *valor de carimbo de data-hora*válido ou um valor de tempo válido; porção de segundos fracionados não truncado[a]<br /><br /> O valor dos dados é um *valor de carimbo de data-hora*válido ou um valor de tempo válido; porção de segundos fracionados truncado[a]<br /><br /> O valor dos dados é um *valor de data*válido [a]<br /><br /> O valor dos dados é um *valor de tempo*válido [a]<br /><br /> O valor dos dados não é um *valor de data*válido, valor de *tempo*ou valor de carimbo *de hora*[a]|Dados<br /><br /> Dados truncados<br /><br /> Dados[f]<br /><br /> Dados[g]<br /><br /> Indefinido|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos os tipos de intervalo C|O valor dos dados é um *valor de intervalo*válido; sem truncação<br /><br /> O valor dos dados é um *valor de intervalo*válido; truncação de um ou mais campos de trilha<br /><br /> Os dados são intervalos válidos; liderando campo precisão significativa é perdido<br /><br /> O valor dos dados não é um valor de intervalo válido|Dados<br /><br /> Dados truncados<br /><br /> Indefinido<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.  
  
 [c] A parte de tempo do valor do *carimbo de tempo* é truncada.  
  
 [d] A parte da data do *valor do carimbo de data* é ignorada.  
  
 [e] A parte de segundos fracionados do carimbo de tempo é truncada.  
  
 [f] Os campos de tempo da estrutura do carimbo de tempo são definidos como zero.  
  
 [g] Os campos de data da estrutura do carimbo de data são definidos para a data atual.  

**Espaços extras**

Os espaços de liderança e de arrasto são ignorados quando os dados de caracteres SQL são convertidos para qualquer um dos seguintes tipos:

- date
- numeric
- time
- timestamp
- dados do intervalo C
