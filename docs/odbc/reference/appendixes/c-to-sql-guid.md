---
title: 'C para SQL: GUID | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af0ed8307652ccf45e7fbfffb6c00355c8a8b004
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159356"
---
# <a name="c-to-sql-guid"></a>C para SQL: GUID
O identificador para o tipo de dados ODBC C do GUID é:  
  
 SQL_C_GUID  
  
 A tabela a seguir mostra o ODBC SQL para o qual os dados de GUID C podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Comprimento de bytes da coluna > = 36|n/d|  
|SQL_VARCHAR|Coluna de comprimento de byte < 36|22001|  
|SQL_LONGVARCHAR|Valor de dados não é um GUID válido|22018|  
|SQL_WCHAR|Comprimento de caracteres da coluna > = 36|n/d|  
|SQL_WVARCHAR|Coluna de comprimento < 36 caracteres|22001|  
|SQL_WLONGVARCHAR|Valor de dados não é um GUID válido|22018|  
|SQL_GUID|None [a]|n/d|  
  
 [a] todos os valores hexadecimais são válidos como um GUID.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados de tipo de dados C de GUID e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados GUID C. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento na **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento **SQLPutData** e o *ParameterValuePtr* argumento em **SQLBindParameter**.
