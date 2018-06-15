---
title: 'SQL para c: data | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d99ebd45ffa463ccfd66bd751dd7415b35a8f5d1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908861"
---
# <a name="sql-to-c-date"></a>SQL para c: data
O identificador para a data do tipo de dados SQL ODBC:  
  
 SQL_TYPE_DATE  
  
 A tabela a seguir mostra o ODBC C para o qual a data de dados do SQL pode ser convertida de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> 11 < = *BufferLength* < = comprimento de bytes de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> 11 < = *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nenhum [a]|data|6 [c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum [a]|Dados [b]|16 [c]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] os campos de hora da estrutura de carimbo de hora são definidos como zero.  
  
 [c] este é o tamanho do tipo de dados C correspondente.  
  
 Quando a data de dados do SQL é convertida em dados de caractere C, a cadeia de caracteres resultante é a "*aaaa*-*mm*-*dd*" formato. Esse formato não é afetado pela configuração de país Windows®.
