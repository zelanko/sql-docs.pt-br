---
title: "C para SQL: numérico | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2cbdbbd3da828d5a995dbd9bff9c6b95aed1420a
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-numeric"></a>C para SQL: numérico
Os identificadores para os tipos de dados ODBC C numéricos são:  
  
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
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados numéricos de C podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Número de dígitos < = comprimento de bytes da coluna<br /><br /> Número de dígitos > bytes de coluna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Número de caracteres < = comprimento de caracteres da coluna<br /><br /> Número de caracteres > comprimento de caracteres da coluna|n/d<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|Convertido sem truncamento de dados ou com truncados de dígitos fracionários<br /><br /> Os dados convertidos com truncamento de dígitos inteiros|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Dados estão dentro do intervalo do tipo de dados ao qual o número é convertido<br /><br /> Dados estão fora do intervalo do tipo de dados ao qual o número é convertido|n/d<br /><br /> 22003|  
|SQL_BIT|Dados são 0 ou 1<br /><br /> Dados for maiores que 0, menor que 2 e não é igual a 1<br /><br /> Dados são menor que 0 ou maior que ou igual a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|Dados não truncados.<br /><br /> Dados truncados.|n/d<br /><br /> 22015|  
  
 [a] essas conversões são suportados apenas para os tipos de dados numérico exato (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG ou SQL_C_NUMERIC). Eles não têm suporte para os tipos de dados numérico aproximado (SQL_C_FLOAT ou SQL_C_DOUBLE). Tipos de dados numéricos exatos de C não podem ser convertidos para um tipo SQL cuja precisão de intervalo não é um único campo de intervalo.  
  
 [b] para o caso de "n / a", um driver pode opcionalmente retornar SQL_SUCCESS_WITH_INFO e 01S07 quando há um truncamento fracionário.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados de tipos de dados numéricos do C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados numérico do C. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento na **SQLPutData** e *ParameterValuePtr* argumento **SQLBindParameter**.
