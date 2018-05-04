---
title: 'SQL em c: GUID | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], GUID
- data conversions from SQL to C types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: cf56c684-c261-4b89-994a-db14ab2241d6
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75bd143912da9bf523f9569f03d076102ba7499d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-guid"></a>SQL em c: GUID
O identificador para o tipo de dados GUID ODBC SQL é:  
  
 SQL_GUID  
  
 A tabela a seguir mostra o ODBC C para o qual os dados de GUID SQL podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres|data|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres|data|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_BINARY|Comprimento em bytes de dados \< =  *BufferLength*|data|Comprimento dos dados em bytes|n/d|  
||Comprimento em bytes de dados > *BufferLength*|Indefinido|Indefinido|22003|  
|SQL_C_GUID|Nenhum [a]|data|16 [b]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] este é o tamanho do tipo de dados C correspondente.
