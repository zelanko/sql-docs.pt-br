---
title: 'SQL para C: Time | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296376"
---
# <a name="sql-to-c-time"></a>SQL para C: hora
O identificador para o tipo de dados ODBC SQL de tempo é:  
  
 SQL_TYPE_TIME  
  
 A tabela a seguir mostra os tipos de dados ODBC C para o qual os dados SQL podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento do byte do caractere<br /><br /> *9* <= *Comprimento de buffer* <= Comprimento do byte do caractere<br /><br /> *Comprimento do buffer* < 9|Dados<br /><br /> Dados truncados[a]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Comprimento do > comprimento* do caractere do buffer<br /><br /> *9* <= *BufferLength* <= Comprimento do caractere<br /><br /> *Comprimento do buffer* < 9|Dados<br /><br /> Dados truncados[a]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nenhum[b]|Dados|6[d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum[b]|Dados[c]|16[d]|n/d|  
  
 [a] Os segundos fracionados do tempo são truncados.  
  
 [b] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [c] Os campos de data da estrutura do carimbo de tempo são definidos para a data atual, e o campo de segundos fracionados da estrutura do carimbo de tempo é definido como zero.  
  
 [d] Este é o tamanho do tipo de dados C correspondente.  
  
 Quando os dados SQL são convertidos em dados do caractere C, a seqüência resultante está no formato "*hh*:*mm*:*ss*". Este formato não é afetado pela configuração de país ® Windows.
