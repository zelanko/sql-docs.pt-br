---
title: 'C para SQL: Timestamp | Microsoft Docs'
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
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bbb6396dc1a49d984834ec6f105b3a9ba42d95c4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-timestamp"></a>C para SQL: Timestamp
O identificador para o tipo de dados ODBC C de carimbo de hora é:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de C do carimbo de hora podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de bytes da coluna > = comprimento de bytes de caracteres<br /><br /> 19 < = comprimento de bytes da coluna < bytes de comprimento de caracteres<br /><br /> Coluna de comprimento de byte < 19<br /><br /> Valor de dados não é um carimbo de hora válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caracteres da coluna > = comprimento de caracteres de dados<br /><br /> 19 < = comprimento de caracteres da coluna < comprimento dos dados de caracteres<br /><br /> 19 < comprimento de caracteres da coluna<br /><br /> Valor de dados não é um carimbo de hora válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Campos de hora são zero<br /><br /> Campos de hora são diferentes de zero<br /><br /> Valor de dados não contém uma data válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Campos de frações de segundo forem zero [a]<br /><br /> Campos de frações de segundo são diferentes de zero [a]<br /><br /> Valor de dados não tem uma hora válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Campos de frações de segundo são truncados não<br /><br /> Campos de frações de segundo são truncados<br /><br /> Valor de dados não é um carimbo de hora válido|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [a] a data em que os campos da estrutura de carimbo de hora são ignorados.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TIMESTAMP, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando dados de carimbo de hora C são convertidos em dados de SQL de caractere, os dados de caracteres resultante estão no "*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[. *f...* ] "formato.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados timestamp C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados timestamp C. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento na **SQLPutData** e *ParameterValuePtr* argumento **SQLBindParameter**.

