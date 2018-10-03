---
title: 'SQL to c: carimbo de hora | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47a0fa22e2d5810faae10ca4ae620bb2a57bb856
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724414"
---
# <a name="sql-to-c-timestamp"></a>SQL para C: carimbo de data/hora
O identificador para o tipo de dados SQL ODBC de carimbo de hora é:  
  
 SQL_TYPE_TIMESTAMP  
  
 A tabela a seguir mostra os tipos de dados ao qual o carimbo de hora de dados do SQL podem ser convertidos de ODBC C. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > bytes de comprimento de caracteres<br /><br /> 20 < = *BufferLength* < = comprimento de byte do caractere<br /><br /> *BufferLength* < 20|data<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > comprimento de caracteres<br /><br /> 20 < = *BufferLength* < = comprimento de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Dados truncados [b]<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de bytes de dados < = *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|data<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Parte de hora do carimbo de hora é zero [a]<br /><br /> Parte de hora do carimbo de hora é diferente de zero [a]|data<br /><br /> Dados truncados [c]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|A parte fracionária de segundos de carimbo de hora é zero [a]<br /><br /> A parte fracionária de segundos de carimbo de hora é diferente de zero [a]|Dados [d]<br /><br /> Dados truncados [d], [e]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|A parte fracionária de segundos de carimbo de hora não será truncado [a]<br /><br /> A parte fracionária de segundos de carimbo de hora é truncado [a]|Dados [e]<br /><br /> Dados truncados [e]|16 [f]<br /><br /> 16 [f]|n/d<br /><br /> 01S07|  
  
 [a] o valor de *BufferLength* é ignorado para essa conversão. O driver pressupõe que o tamanho de **TargetValuePtr* é o tamanho do tipo de dados C.  
  
 [b] os segundos fracionários do que o carimbo de hora são truncados.  
  
 [c] a parte de hora do carimbo de hora será truncada.  
  
 [d] a parte de data do carimbo de hora será ignorada.  
  
 [e] parte fracionária de segundos do carimbo de hora será truncado.  
  
 [f] esse é o tamanho do tipo de dados C correspondente.  
  
 Quando dados SQL de carimbo de hora são convertidos em dados de caractere C, a cadeia de caracteres resultante está no "*aaaa*-*mm*-*dd* *hh* :*mm*:*ss*[.*f...*] "formato, onde pode ser usada até nove dígitos para segundos fracionários. Esse formato não é afetado pela configuração de país Windows®. (Exceto para o ponto decimal e frações de segundos, o formato inteiro deve ser usado, independentemente da precisão do tipo de dados SQL timestamp.)
