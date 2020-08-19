---
description: 'SQL para C: carimbo de data/hora'
title: 'SQL para C: carimbo de data/hora | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a2904f01b5ecadbfc224d052366197e41163cd9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429538"
---
# <a name="sql-to-c-timestamp"></a>SQL para C: carimbo de data/hora

O identificador para o tipo de dados SQL ODBC de carimbo de data/hora é o seguinte:

- SQL_TYPE_TIMESTAMP  

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de carimbo de data/hora podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento de byte de caractere<br /><br /> 20 <= *BufferLength* <= comprimento de byte de caractere<br /><br /> *BufferLength* < 20|Dados<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caractere<br /><br /> 20 <= *BufferLength* <= comprimento do caractere<br /><br /> *BufferLength* < 20|Dados<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|A parte de tempo do carimbo de data/hora é zero [a]<br /><br /> A parte de tempo do carimbo de data/hora é diferente de zero|Dados<br /><br /> Dados truncados [c]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|A parte de segundos fracionários do carimbo de data/hora é zero [a]<br /><br /> A parte de segundos fracionários do carimbo de data/hora é diferente de um]|Dados [d]<br /><br /> Dados truncados [d], [e]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|A parte de segundos fracionários do carimbo de data/hora não está truncada [a]<br /><br /> A parte de segundos fracionários do carimbo de data/hora é truncada [a]|Dados [e]<br /><br /> Dados truncados [e]|16 [f]<br /><br /> 16 [f]|n/d<br /><br /> 01S07|  

 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] os segundos fracionários do carimbo de data/hora estão truncados.  
  
 [c] a parte de tempo do carimbo de data/hora está truncada.  
  
 [d] a parte de data do carimbo de hora é ignorada.  
  
 [e] a parte de segundos fracionários do carimbo de data/hora está truncada.  
  
 [f] Este é o tamanho do tipo de dados C correspondente.  

Quando os dados SQL de carimbo de data/hora são convertidos em dados de caracteres C, a cadeia de caracteres resultante está no "*aaaa* - *mm* - *DD* *hh*:*mm*:*SS*[.* f...*] " formato, onde até nove dígitos podem ser usados para segundos fracionários. Esse formato não é afetado pela configuração de país do Windows®. (Exceto para o ponto decimal e os segundos fracionários, o formato inteiro deve ser usado, independentemente da precisão do tipo de dados timestamp SQL.)
