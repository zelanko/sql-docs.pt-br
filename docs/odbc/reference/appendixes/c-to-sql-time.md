---
title: 'C para SQL: Time | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ea11803847505698ea42d13727b6177f3a24bda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316524"
---
# <a name="c-to-sql-time"></a>C para SQL: Time
O identificador para o tipo de dados do ODBC C de tempo é:  
  
 SQL_C_TYPE_TIME  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de C de tempo podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de bytes da coluna > = 8<br /><br /> Coluna de comprimento de byte < 8<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caracteres da coluna > = 8<br /><br /> Coluna de comprimento < 8 caracteres<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Valor de dados é uma hora válida<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valor de dados é uma hora válida [a]<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22007|  
  
 [a] a data em que parte do que o carimbo de hora é definido como a data atual e os segundos fracionários que parte do que o carimbo de hora é definido como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TYPE_TIME, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados de tempo C são convertidos em dados de SQL de caractere, os dados de caracteres resultante estão no "*hh*:*mm*:*ss*" formato.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do momento em que tipo de dados de C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados C de tempo. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento na **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento **SQLPutData** e o *ParameterValuePtr* argumento em **SQLBindParameter**.
