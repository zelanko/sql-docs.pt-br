---
title: 'C para SQL: tempo | Microsoft Docs'
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
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f1a59c15d2ebf1866d4543fa89662888154d4da
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-time"></a>C para SQL: tempo
O identificador para o tipo de dados do ODBC C de tempo é:  
  
 SQL_C_TYPE_TIME  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de C de tempo podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de bytes da coluna > = 8<br /><br /> Coluna de comprimento de byte < 8<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caracteres da coluna > = 8<br /><br /> Coluna de comprimento < 8 caracteres<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Valor de dados é uma hora válida<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valor de dados é uma hora válida [a]<br /><br /> Valor de dados não é uma hora válida|n/d<br /><br /> 22007|  
  
 [a] a data em que parte do carimbo de hora é definido como a data atual e os segundos fracionários parte do carimbo de hora é definido como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TYPE_TIME, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando dados de tempo C são convertidos em dados de SQL de caractere, os dados de caracteres resultante estão no "*hh*:*mm*:*ss*" formato.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do momento em que tipo de dados de C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados C de tempo. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento na **SQLPutData** e *ParameterValuePtr* argumento **SQLBindParameter**.
