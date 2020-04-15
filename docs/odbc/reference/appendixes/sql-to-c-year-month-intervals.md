---
title: 'SQL para C: Intervalos de um ano | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296386"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL para C: intervalos de ano-mês

Os identificadores para os tipos de dados ODBC SQL de intervalo de um ano são os seguintes:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de intervalo de um ano podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|Strlen_or_indptr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|Porção de campos de arrasto não truncados<br /><br /> Porção de campos de arrasto truncados<br /><br /> A precisão líder do alvo não é grande o suficiente para conter dados da fonte|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|A precisão do intervalo era um único campo e os dados foram convertidos sem truncação<br /><br /> Precisão de intervalo era um único campo e truncado inteiro<br /><br /> A precisão do intervalo não era um único campo|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados em bytes<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Comprimento do byte do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Um tipo SQL de intervalo de um ano pode ser convertido para qualquer tipo de intervalo C de um ano.  
  
 [b] Se a precisão do intervalo for um único campo (um de ANO ou MÊS), o tipo SQL de intervalo pode ser convertido para qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversões padrão

A conversão padrão de um tipo SQL de intervalo é para o tipo de dados de intervalo C correspondente. Em seguida, o aplicativo vincula a coluna ou parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado do ARD) para apontar para a estrutura de SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura SQL_ INTERVAL_STRUCT como o argumento *TargetValuePtr* em uma chamada para **SQLGetData**).
