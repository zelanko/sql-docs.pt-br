---
title: 'SQL a C: GUID | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0f247bc4cb411d535050d7c78e0ea42cc144b0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296456"
---
# <a name="sql-to-c-guid"></a>SQL para C: GUID
O identificador para o tipo de dados GUID ODBC SQL é:  
  
 SQL_GUID  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados GUID SQL podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento do byte do caractere|Dados|36|n/d|  
||*Comprimento do buffer* < 37|Indefinido|Indefinido|22003|  
|SQL_C_WCHAR|*Comprimento do > comprimento* do caractere do buffer|Dados|36|n/d|  
||*Comprimento do buffer* < 37|Indefinido|Indefinido|22003|  
|SQL_C_BINARY|Comprimento de byte de dados \< =  *BufferLength*|Dados|Comprimento dos dados em bytes|n/d|  
||Comprimento de byte de dados > *BufferLength*|Indefinido|Indefinido|22003|  
|SQL_C_GUID|Nenhum[a]|Dados|16[b]|n/d|  
  
 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.
