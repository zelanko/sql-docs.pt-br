---
title: 'SQL para C: Carimbo de tempo | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296346"
---
# <a name="sql-to-c-timestamp"></a>SQL para C: carimbo de data/hora

O identificador para o tipo de dados ODBC SQL de carimbo de data e hora é o seguinte:

- SQL_TYPE_TIMESTAMP  

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de carimbo de tempo podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento do byte do caractere<br /><br /> 20 <= *TampãoComprimento* <= Comprimento do byte do caractere<br /><br /> *Comprimento de tampão* < 20|Dados<br /><br /> Dados truncados[b]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Comprimento do > comprimento* do caractere do buffer<br /><br /> 20 <= *<de comprimento de tampão* = comprimento do caractere<br /><br /> *Comprimento de tampão* < 20|Dados<br /><br /> Dados truncados[b]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|A parte de tempo do carimbo de tempo é zero[a]<br /><br /> A parte de tempo do carimbo de tempo não é zero[a]|Dados<br /><br /> Dados truncados[c]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|A porção de segundos fracionários do carimbo de tempo é zero[a]<br /><br /> A porção de segundos fracionários do carimbo de tempo não é zero[a]|Dados[d]<br /><br /> Dados truncados[d], [e]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|A porção de segundos fracionários do carimbo de tempo não é truncada[a]<br /><br /> A porção de segundos fracionários do carimbo de tempo é truncada[a]|Dados[e]<br /><br /> Dados truncados[e]|16[f]<br /><br /> 16[f]|n/d<br /><br /> 01S07|  

 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Os segundos fracionados do carimbo de tempo são truncados.  
  
 [c] A parte de tempo do carimbo de tempo é truncada.  
  
 [d] A parte da data do carimbo de data é ignorada.  
  
 [e] A parte de segundos fracionados do carimbo de tempo é truncada.  
  
 [f] Este é o tamanho do tipo de dados C correspondente.  

Quando os dados SQL do carimbo de tempo são convertidos em dados do caractere C, a seqüência resultante está no "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*]" formato, onde até nove dígitos podem ser usados para segundos fracionados. Este formato não é afetado pela configuração de país ® Windows. (Exceto pelo ponto decimal e segundos fracionados, todo o formato deve ser usado, independentemente da precisão do tipo de dados SQL do carimbo de tempo.)
