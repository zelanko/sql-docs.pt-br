---
title: 'C para SQL: GUID | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45310bcea2a98d4c1dcb4c4ca782a84c7107ed6d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="c-to-sql-guid"></a>C para SQL: GUID
O identificador para o tipo de dados GUID ODBC C é:  
  
 SQL_C_GUID  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de GUID C podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Comprimento de bytes da coluna > = 36|n/d|  
|SQL_VARCHAR|Coluna de comprimento de byte < 36|22001|  
|SQL_LONGVARCHAR|Valor de dados não é um GUID válido|22018|  
|SQL_WCHAR|Comprimento de caracteres da coluna > = 36|n/d|  
|SQL_WVARCHAR|Coluna de comprimento < 36 caracteres|22001|  
|SQL_WLONGVARCHAR|Valor de dados não é um GUID válido|22018|  
|SQL_GUID|Nenhum [a]|n/d|  
  
 [a] todos os valores hexadecimais são válidos como um GUID.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados GUID C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados GUID C. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento na **SQLPutData** e *ParameterValuePtr* argumento **SQLBindParameter**.
