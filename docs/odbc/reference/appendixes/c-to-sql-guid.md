---
description: 'C para SQL: GUID'
title: 'C to SQL: GUID | Microsoft Docs'
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
ms.openlocfilehash: 3fca2ba20df65222eaf1ce6f4384f449a1524334
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499979"
---
# <a name="c-to-sql-guid"></a>C para SQL: GUID
O identificador para o tipo de dados ODBC de GUID C é:  
  
 SQL_C_GUID  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados GUID C podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Comprimento de byte de coluna >= 36|n/d|  
|SQL_VARCHAR|Comprimento de byte de coluna < 36|22001|  
|SQL_LONGVARCHAR|O valor dos dados não é um GUID válido|22018|  
|SQL_WCHAR|Comprimento de caractere de coluna >= 36|n/d|  
|SQL_WVARCHAR|Comprimento de caractere de coluna < 36|22001|  
|SQL_WLONGVARCHAR|O valor dos dados não é um GUID válido|22018|  
|SQL_GUID|Nenhum [a]|n/d|  
  
 [a] todos os valores hexadecimais são válidos como um GUID.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados GUID C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados GUID C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
