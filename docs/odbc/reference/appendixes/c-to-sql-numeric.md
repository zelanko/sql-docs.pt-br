---
title: 'C a SQL: Numérico | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304727"
---
# <a name="c-to-sql-numeric"></a>C para SQL: numérico
Os identificadores para os tipos de dados Numéricos ODBC C são:  
  
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
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados numéricos C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Número de dígitos <= Comprimento do byte da coluna<br /><br /> Número de dígitos > comprimento do byte da coluna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Número de caracteres <= Comprimento do caractere da coluna<br /><br /> Número de caracteres > comprimento do caractere da Coluna|n/d<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|Dados convertidos sem truncação ou com truncadas de dígitos fracionados<br /><br /> Dados convertidos com truncação de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido|n/d<br /><br /> 22003|  
|SQL_BIT|Os dados são 0 ou 1<br /><br /> Os dados são maiores que 0, menos de 2, e não são iguais a 1<br /><br /> Os dados são inferiores ou superiores a 0 ou igual a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|Dados não truncados.<br /><br /> Dados truncados.|n/d<br /><br /> 22015|  
  
 [a] Essas conversões são suportadas apenas para os tipos exatos de dados numéricos (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC). Eles não são suportados para os tipos de dados numéricos aproximados (SQL_C_FLOAT ou SQL_C_DOUBLE). Os tipos exatos de dados C não podem ser convertidos em um tipo SQL de intervalo cuja precisão de intervalo não seja um único campo.  
  
 [b] Para o caso "n/a", o motorista pode retornar opcionalmente SQL_SUCCESS_WITH_INFO e 01S07 quando houver uma truncação fracionada.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados dos tipos de dados C numéricos e assume que o tamanho do buffer de dados é o tamanho do tipo de dados C numérico. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
