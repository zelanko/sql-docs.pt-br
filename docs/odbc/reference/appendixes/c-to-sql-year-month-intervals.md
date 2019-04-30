---
title: 'C para SQL: Ano-mês | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d12727f9298eb63fe10b44c48b9d3b7996a839d5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159285"
---
# <a name="c-to-sql-year-month-intervals"></a>C para SQL: Intervalos de ano-mês
Os identificadores para os tipos de dados ODBC C ano-mês intervalo são:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 A tabela a seguir mostra o ODBC SQL para o ano-mês dados de intervalo C podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Comprimento de bytes da coluna > = comprimento de byte do caractere<br /><br /> Comprimento de bytes da coluna < caracteres de comprimento de bytes [a]<br /><br /> Valor de dados não é um literal de intervalo válido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Comprimento de caracteres da coluna > = comprimento de caracteres de dados<br /><br /> Comprimento de caracteres da coluna < caracteres de comprimento de dados [a]<br /><br /> Valor de dados não é um literal de intervalo válido|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|Conversão de um único campo de intervalo não resultou em truncamento de dígitos inteiros<br /><br /> Conversão resultou em truncamento de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Valor de dados foi convertido sem truncamento de todos os campos<br /><br /> Um ou mais campos de valor de dados foram truncados durante conversão|n/d<br /><br /> 22015|  
  
 [a] tipos de dados de intervalo de todos os C podem ser convertido em um tipo de dados de caractere.  
  
 [b] se o campo de tipo na estrutura de intervalo é, de modo que o intervalo é de um único campo (SQL_YEAR ou SQL_MONTH), o tipo de intervalo de C pode ser convertido em qualquer numérico exato (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL ou SQL_NUMERIC).  
  
 A conversão padrão de um intervalo de tipo C é o intervalo de ano-mês tipo SQL correspondente.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados de intervalo de C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados C de intervalo. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento na **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento **SQLPutData** e o *ParameterValuePtr* argumento em **SQLBindParameter**.
