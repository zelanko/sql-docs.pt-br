---
title: 'SQL to C: Date | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296526"
---
# <a name="sql-to-c-date"></a>SQL para C: data
O identificador para o tipo de dados SQL ODBC de data é:  
  
 SQL_TYPE_DATE  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento de byte de caractere<br /><br /> 11 <= *BufferLength* <= comprimento de byte de caractere<br /><br /> *BufferLength* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caractere<br /><br /> 11 <= *BufferLength* <= comprimento do caractere<br /><br /> *BufferLength* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nenhum [a]|Dados|6 [c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum [a]|Dados [b]|16 [c]|n/d|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] os campos de tempo da estrutura de carimbo de data/hora são definidos como zero.  
  
 [c] Este é o tamanho do tipo de dados C correspondente.  
  
 Quando os dados SQL de data são convertidos em dados de caractere C, a cadeia de caracteres resultante está no formato "*aaaa*-*mm*-*DD*". Esse formato não é afetado pela configuração de país do Windows®.
