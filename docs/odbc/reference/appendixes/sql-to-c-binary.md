---
title: "SQL em c: binário | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cf5191b9fa41af5c0e180f9ad605f9563cbcf8bc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sql-to-c-binary"></a>SQL em c: binário
Os identificadores para os tipos de dados SQL ODBC binários são:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 A tabela a seguir mostra o ODBC C para o qual os dados binários do SQL podem ser convertidos de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Comprimento em bytes de dados) \* 2 < *BufferLength*<br /><br /> (Comprimento em bytes de dados) \* 2 > = *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Caractere de comprimento de dados) \* 2 < *BufferLength*<br /><br /> (Caractere de comprimento de dados) \* 2 > = *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Comprimento em bytes de dados < = *BufferLength*<br /><br /> Comprimento em bytes de dados > *BufferLength*|data<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
  
 Quando dados binários do SQL são convertidos em dados de caractere C, cada byte (8 bits) de fonte de dados é representado como dois caracteres ASCII. Esses caracteres são a representação de caracteres ASCII de número em formato hexadecimal. Por exemplo, um 00000001 binário é convertido em "01" e um 11111111 binário é convertido em "FF".  
  
 O driver sempre converte bytes individuais em pares de dígitos hexadecimais e encerra a cadeia de caracteres com um byte nulo. Por isso, se *BufferLength* é mesmo e é menor que o comprimento dos dados convertidos, o último byte do **TargetValuePtr* buffer não é usado. (Os dados convertidos requerem um número par de bytes, o próximo ao último byte é um byte nulo e o último byte não pode ser usado.)  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desaconselhável de dados SQL binários de associação para um tipo de dados caractere C. Normalmente, essa conversão é ineficiente e lento.
