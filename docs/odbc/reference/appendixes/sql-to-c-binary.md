---
title: 'SQL a C: Binário | Microsoft Docs'
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
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298815"
---
# <a name="sql-to-c-binary"></a>SQL para C: binário
Os identificadores para os tipos binários de dados ODBC SQL são:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL binários podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Comprimento de byte de dados) \* 2 *< bufferLength*<br /><br /> (Comprimento de byte de dados) \* 2 >= *Comprimento do Buffer*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Comprimento do caractere dos dados) \* 2 *< bufferLength*<br /><br /> (Comprimento do caractere dos dados) \* 2 >= *Comprimento do Buffer*|Dados<br /><br /> Dados truncados|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Dados truncados|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes|n/d<br /><br /> 01004|  
  
 Quando os dados SQL binários são convertidos em dados de caractere C, cada byte (8 bits) dos dados de origem é representado como dois caracteres ASCII. Esses caracteres são a representação do caractere ASCII do número em sua forma hexadecimal. Por exemplo, um binário 0000001 é convertido em "01" e um binário 11111111 é convertido em "FF".  
  
 O driver sempre converte bytes individuais em pares de dígitos hexadecimais e termina a seqüência de caracteres com um byte nulo. Por causa disso, se *BufferLength* estiver uniforme e for menor do que o comprimento dos dados convertidos, o último byte do buffer ** TargetValuePtr* não será usado. (Os dados convertidos exigem um número uniforme de bytes, o penúltimo byte é um byte nulo e o último byte não pode ser usado.)  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são desencorajados de vincular dados SQL binários a um tipo de dados c de caractere. Esta conversão é geralmente ineficiente e lenta.
