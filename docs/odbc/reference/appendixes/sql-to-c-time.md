---
title: 'SQL to C: time | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296376"
---
# <a name="sql-to-c-time"></a>SQL para C: hora
O identificador para o tipo de dados SQL ODBC de tempo é:  
  
 SQL_TYPE_TIME  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento de byte de caractere<br /><br /> *9* <= *BufferLength* <= comprimento de byte de caractere<br /><br /> *BufferLength* < 9|Dados<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caractere<br /><br /> *9* <= *BufferLength* <= comprimento do caractere<br /><br /> *BufferLength* < 9|Dados<br /><br /> Dados truncados [a]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Nenhum [b]|Dados|6 [d]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum [b]|Dados [c]|16 [d]|n/d|  
  
 [a] os segundos fracionários do tempo estão truncados.  
  
 [b] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [c] os campos de data da estrutura de carimbo de hora são definidos como a data atual e o campo de segundos fracionários da estrutura de carimbo de data/hora é definido como zero.  
  
 [d] Este é o tamanho do tipo de dados C correspondente.  
  
 Quando os dados SQL de tempo são convertidos em dados de caractere C, a cadeia de caracteres resultante está no formato "*hh*:*mm*:*SS*". Esse formato não é afetado pela configuração de país do Windows®.
