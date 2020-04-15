---
title: 'C a SQL: Intervalos de um ano | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306607"
---
# <a name="c-to-sql-year-month-intervals"></a>C para SQL: intervalos de ano-mês
Os identificadores para os tipos de dados ODBC C do intervalo de um ano são:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados c do intervalo de um ano podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Comprimento do byte da coluna >= Comprimento do byte do caractere<br /><br /> Comprimento do byte da coluna < comprimento do byte do personagem[a]<br /><br /> O valor dos dados não é um intervalo válido literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Comprimento do caractere da coluna >= Comprimento do caractere dos dados<br /><br /> Comprimento do caractere da coluna < comprimento do caractere dos dados[a]<br /><br /> O valor dos dados não é um intervalo válido literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|A conversão de um intervalo de campo único não resultou em truncação de dígitos inteiros<br /><br /> A conversão resultou em truncação de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|O valor dos dados foi convertido sem truncação de quaisquer campos<br /><br /> Um ou mais campos de valor de dados foram truncados durante a conversão|n/d<br /><br /> 22015|  
  
 [a] Todos os tipos de dados de intervalo C podem ser convertidos em um tipo de dados de caracteres.  
  
 [b] Se o campo de tipo na estrutura do intervalo for tal que o intervalo seja um único campo (SQL_YEAR ou SQL_MONTH), o tipo C do intervalo pode ser convertido para qualquer numérico exato (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL ou SQL_NUMERIC).  
  
 A conversão padrão de um tipo de intervalo C é para o tipo SQL de intervalo de ano correspondente.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados do intervalo C e assume que o tamanho do buffer de dados é o tamanho do tipo de dados do intervalo C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
