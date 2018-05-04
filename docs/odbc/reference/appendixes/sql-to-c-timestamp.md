---
title: 'SQL para c: Timestamp | Microsoft Docs'
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
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f3ace8f40ecafc857c63dca58ec072247d3b475
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-timestamp"></a>SQL para c: Timestamp
O identificador para o tipo de dados SQL ODBC timestamp é:  
  
 SQL_TYPE_TIMESTAMP  
  
 A tabela a seguir mostra o ODBC C para o qual o carimbo de hora de dados do SQL podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> 20 < = *BufferLength* < = comprimento de bytes de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> 20 < = *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Parte de hora de carimbo de hora for zero [a]<br /><br /> Parte de hora do carimbo de hora é diferente de zero [a]|data<br /><br /> Dados truncados [c]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|A parte fracionária de segundos de carimbo de hora for zero [a]<br /><br /> A parte fracionária de segundos de carimbo de hora é diferente de zero [a]|Dados [d]<br /><br /> Dados truncados [d], [e]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|A parte fracionária de segundos de carimbo de hora não será truncado [a]<br /><br /> A parte fracionária de segundos de carimbo de hora é truncado [a]|Dados [e]<br /><br /> Dados truncados [e]|16 [f]<br /><br /> 16 [f]|n/d<br /><br /> 01S07|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] as frações de segundo o carimbo de hora são truncadas.  
  
 [c] a parte de hora do carimbo de hora é truncada.  
  
 [d] a parte de data do carimbo de hora será ignorada.  
  
 [e] parte fracionária de segundos do carimbo de hora é truncado.  
  
 [f] este é o tamanho do tipo de dados C correspondente.  
  
 Quando dados SQL de carimbo de hora são convertidos em dados de caractere C, a cadeia de caracteres resultante é a "*aaaa*-*mm*-*dd* *hh* :*mm*:*ss*[.*f...*] "formato, onde pode ser usado até nove dígitos para segundos fracionários. Esse formato não é afetado pela configuração de país Windows®. (Com exceção do ponto decimal e frações de segundo, o formato inteiro deve ser usado, independentemente da precisão do tipo de dados timestamp SQL.)
