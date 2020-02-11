---
title: 'SQL to C: intervalos de ano/mês | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68065041"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL para C: intervalos de ano-mês

Os identificadores para os tipos de dados SQL ODBC do intervalo de ano/mês são os seguintes:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL do intervalo do ano-mês podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|Parte dos campos à direita não truncada<br /><br /> Parte dos campos à direita truncada<br /><br /> A precisão inicial do destino não é grande o suficiente para manter os dados da origem|data<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|A precisão do intervalo era um único campo e os dados foram convertidos sem truncamento<br /><br /> A precisão do intervalo era um único campo e um todo truncado<br /><br /> A precisão do intervalo não era um campo único|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Comprimento dos dados em bytes<br /><br /> Tamanho do tipo de dados C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Comprimento de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) >= *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição a fracionários) >= *BufferLength*|data<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] um tipo de SQL de intervalo de ano/mês pode ser convertido em qualquer tipo de intervalo de ano/mês.  
  
 [b] se a precisão do intervalo for um único campo (um de ano ou mês), o tipo SQL de intervalo poderá ser convertido em qualquer numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversões padrão

A conversão padrão de um tipo SQL de intervalo é para o tipo de dados de intervalo de C correspondente. Em seguida, o aplicativo associa a coluna ou o parâmetro (ou define o campo SQL_DESC_DATA_PTR no registro apropriado do ARD) para apontar para a estrutura de SQL_INTERVAL_STRUCT inicializada (ou passa um ponteiro para a estrutura de INTERVAL_STRUCT SQL_ como o argumento *TargetValuePtr* em uma chamada para **SQLGetData**).
