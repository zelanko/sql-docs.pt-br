---
title: 'C to SQL: Numeric | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbc0a994ef95f2deca29c8a4cbb06f3167b0433f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304727"
---
# <a name="c-to-sql-numeric"></a>C para SQL: numérico
Os identificadores para os tipos de dados numéricos ODBC C são:  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados numéricos C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Número de dígitos <= comprimento de byte de coluna<br /><br /> Número de dígitos > comprimento de byte de coluna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Número de caracteres <= comprimento de caractere de coluna<br /><br /> Número de caracteres > comprimento de caractere de coluna|n/d<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|Dados convertidos sem truncamento ou com truncamento de dígitos fracionários<br /><br /> Dados convertidos com truncamento de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido|n/d<br /><br /> 22003|  
|SQL_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menores que 2 e não iguais a 1<br /><br /> Os dados são menores que 0 ou maiores ou iguais a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|Dados não truncados.<br /><br /> Dados truncados.|n/d<br /><br /> 22015|  
  
 [a] essas conversões são suportadas apenas para os tipos de dados numéricos exatos (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC). Eles não têm suporte para os tipos de dados numéricos aproximados (SQL_C_FLOAT ou SQL_C_DOUBLE). Os tipos de dados numéricos C exatos não podem ser convertidos em um tipo SQL de intervalo cuja precisão de intervalo não seja um único campo.  
  
 [b] para o caso de "n/a", um driver pode, opcionalmente, retornar SQL_SUCCESS_WITH_INFO e 01S07 quando houver um truncamento fracionário.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados dos tipos de dados numéricos C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados numérico C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
