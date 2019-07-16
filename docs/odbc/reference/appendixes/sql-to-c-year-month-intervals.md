---
title: 'SQL para C: Ano-mês | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c7412226dd0674022da022b0a0a63e5bf2063cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065041"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL para C: Intervalos de ano-mês

Os identificadores para os tipos de dados SQL ODBC ano-mês intervalo são as seguintes:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

A tabela a seguir mostra os tipos de dados para o ano-mês o intervalo de dados do SQL pode ser convertido de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|Parte de campos à direita não truncado<br /><br /> Parte de campos à direita truncado<br /><br /> A precisão do destino inicial não é grande o suficiente para manter os dados de origem|Data<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|Precisão de intervalo foi um único campo e os dados foi convertidos sem truncamento<br /><br /> Precisão de intervalo foi um único campo e truncado para inteiros<br /><br /> Precisão de intervalo não era um único campo|Data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados em bytes<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Bytes de comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) > = *BufferLength*|Data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento de caracteres < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) < *BufferLength*<br /><br /> Número de dígitos de inteiro (em vez de fracionários) > = *BufferLength*|Data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de ano-mês de um tipo SQL pode ser convertido em qualquer tipo de C do intervalo de ano / mês.  
  
 [b] se a precisão de intervalo é um único campo (um ano ou mês), o intervalo de tipo SQL pode ser convertido em qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversões padrão

A conversão padrão de um intervalo de tipo de SQL é o tipo de dados de intervalo de C correspondente. O aplicativo, em seguida, associa a coluna ou parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado da descartar) para apontar para a estrutura SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura de SQL _ INTERVAL_STRUCT como o *TargetValuePtr* argumento em uma chamada para **SQLGetData**).
