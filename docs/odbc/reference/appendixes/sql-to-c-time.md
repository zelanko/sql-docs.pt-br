---
title: 'SQL para C: Tempo | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99f8219ef53f72b0d7ab1477bba5d24d441a3141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68065077"
---
# <a name="sql-to-c-time"></a>SQL para C: Time
O identificador para a hora em que o tipo de dados SQL ODBC é:  
  
 SQL_TYPE_TIME  
  
 A tabela a seguir mostra os tipos de dados para o qual os dados SQL de tempo podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> *9* <= *BufferLength* < = comprimento de byte do caractere<br /><br /> *BufferLength* < 9|Data<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> *9* <= *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 9|Data<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|None [b]|Data|6[d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|None [b]|Dados [c]|16[d]|n/d|  
  
 [a] as frações de tempo são truncadas.  
  
 [b] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [c] os campos de data da estrutura de carimbo de hora são definidos como a data atual, e o campo de frações de segundos da estrutura de carimbo de hora é definido como zero.  
  
 [d] esse é o tamanho do tipo de dados C correspondente.  
  
 Quando dados SQL de hora são convertidos em dados de caractere C, a cadeia de caracteres resultante está no "*hh*:*mm*:*ss*" formato. Esse formato não é afetado pela configuração de país Windows®.
