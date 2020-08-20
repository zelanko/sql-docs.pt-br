---
description: 'SQL para C: binário'
title: 'SQL para C: Binary | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 229611308c2dba83a8d793810eb5a5443cbd7062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456549"
---
# <a name="sql-to-c-binary"></a>SQL para C: binário
Os identificadores para os tipos de dados SQL ODBC binários são:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL binários podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Comprimento de bytes de dados) \* 2 < *BufferLength*<br /><br /> (Comprimento de bytes de dados) \* 2 >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Comprimento de caracteres de dados) \* 2 < *BufferLength*<br /><br /> (Comprimento de caracteres de dados) \* 2 >= *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Comprimento de bytes de dados <= *BufferLength*<br /><br /> Comprimento de bytes de dados > *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
  
 Quando dados SQL binários são convertidos em dados de caracteres C, cada byte (8 bits) de dados de origem é representado como dois caracteres ASCII. Esses caracteres são a representação de caractere ASCII do número em sua forma hexadecimal. Por exemplo, um 00000001 binário é convertido em "01" e um binário 11111111 é convertido em "FF".  
  
 O driver sempre converte bytes individuais em pares de dígitos hexadecimais e encerra a cadeia de caracteres com um byte nulo. Por isso, se *BufferLength* for par e for menor que o comprimento dos dados convertidos, o último byte do * buffer de **TargetValuePtr* não será usado. (Os dados convertidos exigem um número par de bytes, o byte do próximo a último é um byte nulo e o último byte não pode ser usado.)  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desencorajados de associar dados SQL binários a um tipo de dados de caractere C. Normalmente, essa conversão é ineficiente e lenta.
