---
title: 'C to SQL: timestamp | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa75299f4d8e8f15293064d0bf3fb3979fe382d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037697"
---
# <a name="c-to-sql-timestamp"></a>C para SQL: carimbo de data/hora
O identificador do tipo de dados de carimbo de data/hora ODBC C é:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados de carimbo de data/hora C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de byte de coluna >= comprimento de byte de caractere<br /><br /> 19 <= comprimento de byte de coluna < comprimento de byte de caractere<br /><br /> Comprimento de byte de coluna < 19<br /><br /> O valor dos dados não é um carimbo de data/hora válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caractere de coluna >= comprimento de caractere de dados<br /><br /> 19 <= comprimento de caractere de coluna < comprimento de caractere de dados<br /><br /> Comprimento de caractere de coluna < 19<br /><br /> O valor dos dados não é um carimbo de data/hora válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Os campos de hora são zero<br /><br /> Os campos de hora são diferentes de zero<br /><br /> O valor dos dados não contém uma data válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Os campos de segundos fracionários são zero [a]<br /><br /> Os campos de segundos fracionários são diferentes de zero [a]<br /><br /> O valor dos dados não contém uma hora válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Os campos de segundos fracionários não estão truncados<br /><br /> Os campos de segundos fracionários estão truncados<br /><br /> O valor dos dados não é um carimbo de data/hora válido|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [a] os campos de data da estrutura de carimbo de data/hora são ignorados.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura de SQL_C_TIMESTAMP, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados C do carimbo de data/hora são convertidos em dados SQL de caractere, os dados de caractere resultantes estão no "*aaaa*-*mm*-*DD* *hh*:*mm*:*SS*[.* f...*] " ao.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados timestamp C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados timestamp C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
