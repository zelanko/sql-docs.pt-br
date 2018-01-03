---
title: 'SQL para c: tempo | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b9879b2a051045fb4ecc6aeb75b92020b187652
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-time"></a>SQL para c: tempo
O identificador para a hora em que o tipo de dados SQL ODBC é:  
  
 SQL_TYPE_TIME  
  
 A tabela a seguir mostra o ODBC C para o qual os dados SQL de tempo podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> *9* <= *BufferLength* < = comprimento de bytes de caracteres<br /><br /> *BufferLength* < 9|data<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> *9* <= *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 9|data<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nenhum [b]|data|6 [d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum [b]|Dados [c]|16 [d]|n/d|  
  
 [a] as frações de segundo de tempo são truncados.  
  
 [b] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [c] os campos de data da estrutura de carimbo de hora são definidos como a data atual e o campo de frações de segundos da estrutura de carimbo de hora é definido como zero.  
  
 [d] este é o tamanho do tipo de dados C correspondente.  
  
 Quando dados SQL time são convertidos em dados de caractere C, a cadeia de caracteres resultante é a "*hh*:*mm*:*ss*" formato. Esse formato não é afetado pela configuração de país Windows®.
