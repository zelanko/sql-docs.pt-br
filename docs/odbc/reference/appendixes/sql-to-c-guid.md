---
description: 'SQL para C: GUID'
title: 'SQL to C: GUID | Microsoft Docs'
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
ms.openlocfilehash: 3a0285850372d78bbe0a24c8707e14e4f5672fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456497"
---
# <a name="sql-to-c-guid"></a>SQL para C: GUID
O identificador para o tipo de dados SQL ODBC GUID é:  
  
 SQL_GUID  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL do GUID podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento de byte de caractere|Dados|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caractere|Dados|36|n/d|  
||*BufferLength* < 37|Indefinido|Indefinido|22003|  
|SQL_C_BINARY|Comprimento de bytes de \< =  *BufferLength* de dados|Dados|Comprimento dos dados em bytes|n/d|  
||Comprimento de bytes de dados > *BufferLength*|Indefinido|Indefinido|22003|  
|SQL_C_GUID|Nenhum [a]|Dados|16 [b]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.
