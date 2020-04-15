---
title: 'C a SQL: Data | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa3df8aaee03472076b3241cb9bb60e2a307e28b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298844"
---
# <a name="c-to-sql-date"></a>C para SQL: data
O identificador para o tipo de dados Da data ODBC C é:  
  
 SQL_C_TYPE_DATE  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para que os dados da data C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento do byte da coluna >= 10<br /><br /> Comprimento do byte da coluna < 10<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento do caractere da coluna >= 10<br /><br /> Comprimento do caractere da coluna < 10<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|O valor dos dados é uma data válida<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é uma data válida[a]<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22007|  
  
 [a] A parte de tempo do carimbo de tempo é definida como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TYPE_DATE, consulte [C Data Types](../../../odbc/reference/appendixes/c-data-types.md), mais cedo neste apêndice.  
  
 Quando os dados da data C são convertidos em dados SQL de caracteres, os dados de caractereresultantes estão no formato "*yyyy*-*mm*-*dd*".  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados da data C e assume que o tamanho do buffer de dados é o tamanho do tipo de dados da data C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
