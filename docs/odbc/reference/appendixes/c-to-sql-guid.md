---
title: 'C a SQL: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306617"
---
# <a name="c-to-sql-guid"></a>C para SQL: GUID
O identificador para o tipo de dados GUID ODBC C é:  
  
 SQL_C_GUID  
  
 A tabela a seguir mostra os tipos de dados ODBC SQL para os quais os dados GUID C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Comprimento do byte da coluna >= 36|n/d|  
|SQL_VARCHAR|Comprimento do byte da coluna < 36|22001|  
|SQL_LONGVARCHAR|O valor dos dados não é um GUID válido|22018|  
|SQL_WCHAR|Comprimento do caractere da coluna >= 36|n/d|  
|SQL_WVARCHAR|Comprimento do caractere da coluna < 36|22001|  
|SQL_WLONGVARCHAR|O valor dos dados não é um GUID válido|22018|  
|SQL_GUID|Nenhum[a]|n/d|  
  
 [a] Todos os valores hexidecimais são válidos como GUID.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados GUID C e assume que o tamanho do buffer de dados é o tamanho do tipo de dados GUID C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* no **SQLPutData** e no buffer especificado com o *argumento StrLen_or_IndPtr* no **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* no **SQLPutData** e o argumento *ParameterValuePtr* no **SQLBindParameter**.
