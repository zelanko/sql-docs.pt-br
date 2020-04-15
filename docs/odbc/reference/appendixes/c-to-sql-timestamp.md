---
title: 'C para SQL: Carimbo de tempo | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283746"
---
# <a name="c-to-sql-timestamp"></a>C para SQL: carimbo de data/hora
O identificador para o tipo de dados ODBC C do carimbo de tempo é:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados do carimbo de tempo C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento do byte da coluna >= Comprimento do byte do caractere<br /><br /> 19 <= Comprimento do byte da coluna < comprimento do byte do caractere<br /><br /> Comprimento do byte da coluna < 19<br /><br /> O valor dos dados não é um carimbo de tempo válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento do caractere da coluna >= Comprimento do caractere dos dados<br /><br /> 19 <= Comprimento do caractere da coluna < Comprimento do caractere dos dados<br /><br /> Comprimento do caractere da coluna < 19<br /><br /> O valor dos dados não é um carimbo de tempo válido|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Os campos do tempo são zero<br /><br /> Os campos de tempo não são zero<br /><br /> O valor dos dados não contém uma data válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Os campos de segundos fracionados são zero[a]<br /><br /> Os campos de segundos fracionados não são zero[a]<br /><br /> O valor dos dados não contém um tempo válido|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Os campos de segundos fracionados não são truncados<br /><br /> Os campos de segundos fracionados são truncados<br /><br /> O valor dos dados não é um carimbo de tempo válido|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [a] Os campos de data da estrutura do carimbo de data são ignorados.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TIMESTAMP, consulte [C Data Types](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados do carimbo de tempo C são convertidos em dados SQL de caracteres, os dados de caractereresultantes estão no "*yyyy*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*]" Formato.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados do carimbo de tempo C e assume que o tamanho do buffer de dados é o tamanho do tipo de dados do carimbo de tempo C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
