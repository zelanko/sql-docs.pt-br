---
title: 'C a SQL: Tempo | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304757"
---
# <a name="c-to-sql-time"></a>C para SQL: hora
O identificador para o tipo de dados ODBC C de tempo é:  
  
 SQL_C_TYPE_TIME  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para o qual os dados C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento do byte da coluna >= 8<br /><br /> Comprimento do byte da coluna < 8<br /><br /> O valor dos dados não é um tempo válido|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento do caractere da coluna >= 8<br /><br /> Comprimento do caractere da coluna < 8<br /><br /> O valor dos dados não é um tempo válido|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|O valor dos dados é um tempo válido<br /><br /> O valor dos dados não é um tempo válido|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é um tempo válido[a]<br /><br /> O valor dos dados não é um tempo válido|n/d<br /><br /> 22007|  
  
 [a] A parte da data do carimbo de tempo é definida para a data atual, e a parte de segundos fracionados do carimbo de tempo é definida como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura de SQL_C_TYPE_TIME, consulte [C Data Types](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados de C são convertidos em dados SQL de caracteres, os dados de caracteres resultantes estão no formato "*hh*:*mm*:*ss*".  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados c e assume que o tamanho do buffer de dados é o tamanho do tipo de dados da hora C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
