---
title: 'SQL para C: Data | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe0c30f0f0fbf0ea695d79387fdec3694a54ebca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151270"
---
# <a name="sql-to-c-date"></a>SQL para C: Date
O identificador para a data do tipo de dados SQL do ODBC:  
  
 SQL_TYPE_DATE  
  
 A tabela a seguir mostra o ODBC C para o qual a data de dados do SQL pode ser convertida de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> 11 < = *BufferLength* < = comprimento de byte do caractere<br /><br /> *BufferLength* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> 11 < = *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|None [a]|Dados|6[c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|None [a]|Dados [b]|16[c]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] os campos de hora da estrutura de carimbo de hora são definidos como zero.  
  
 [c] esse é o tamanho do tipo de dados C correspondente.  
  
 Quando a data de dados do SQL é convertida em dados de caractere C, a cadeia de caracteres resultante está no "*aaaa*-*mm*-*dd*" formato. Esse formato não é afetado pela configuração de país Windows®.
