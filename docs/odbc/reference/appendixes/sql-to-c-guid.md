---
title: 'SQL para C: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21054bdb3f869a0f06349b32e481144b3582de4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63258823"
---
# <a name="sql-to-c-guid"></a>SQL para C: GUID
O identificador para o tipo de dados SQL do ODBC GUID é:  
  
 SQL_GUID  
  
 A tabela a seguir mostra os tipos de dados para o qual os dados de GUID SQL podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres|Dados|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres|Dados|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_BINARY|Comprimento de bytes de dados \< =  *BufferLength*|Dados|Comprimento dos dados em bytes|n/d|  
||Comprimento de bytes de dados > *BufferLength*|Indefinido|Indefinido|22003|  
|SQL_C_GUID|None [a]|Dados|16[b]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] esse é o tamanho do tipo de dados C correspondente.
