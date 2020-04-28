---
title: 'C to SQL: time | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 264ce7751072b79163923f0c141542680f7b02bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304757"
---
# <a name="c-to-sql-time"></a>C para SQL: hora
O identificador para o tipo de dados de tempo ODBC C é:  
  
 SQL_C_TYPE_TIME  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados de C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de byte de coluna >= 8<br /><br /> Comprimento de byte de coluna < 8<br /><br /> O valor dos dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caractere de coluna >= 8<br /><br /> Comprimento de caractere de coluna < 8<br /><br /> O valor dos dados não é uma hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|O valor dos dados é uma hora válida<br /><br /> O valor dos dados não é uma hora válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é uma hora válida [a]<br /><br /> O valor dos dados não é uma hora válida|n/d<br /><br /> 22007|  
  
 [a] a parte de data do carimbo de hora é definida como a data atual e a parte de segundos fracionários do carimbo de data/hora é definida como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura de SQL_C_TYPE_TIME, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados de tempo C são convertidos em dados SQL de caractere, os dados de caractere resultantes estão no formato "*hh*:*mm*:*SS*".  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados time C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados time C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
