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
ms.openlocfilehash: 1a2ed3cffcb196cb09841df3b54fbfab53e22477
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056867"
---
# <a name="sql-to-c-guid"></a>SQL para C: GUID
O identificador para o tipo de dados SQL do ODBC GUID é:  
  
 SQL_GUID  
  
 A tabela a seguir mostra os tipos de dados para o qual os dados de GUID SQL podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres|Data|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres|Data|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_BINARY|Comprimento de bytes de dados \< =  *BufferLength*|Data|Comprimento dos dados em bytes|n/d|  
||Comprimento de bytes de dados > *BufferLength*|Indefinido|Indefinido|22003|  
|SQL_C_GUID|None [a]|Data|16[b]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] esse é o tamanho do tipo de dados C correspondente.
