---
title: 'SQL a C: Data | Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296526"
---
# <a name="sql-to-c-date"></a>SQL para C: data
O identificador para a data em que o tipo de dados SQL o DSBC é:  
  
 SQL_TYPE_DATE  
  
 A tabela a seguir mostra os tipos de dados ODBC C para a qual os dados SQL de data podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > comprimento do byte do caractere<br /><br /> 11 <= *TampãoComprimento* <= Comprimento do byte do caractere<br /><br /> *Comprimento do tampão* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*Comprimento do > comprimento* do caractere do buffer<br /><br /> 11 <= *TampãoComprimento* <= Comprimento do caractere<br /><br /> *Comprimento do tampão* < 11|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|10<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Nenhum[a]|Dados|6[c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Nenhum[a]|Dados[b]|16[c]|n/d|  
  
 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Os campos de tempo da estrutura do carimbo de tempo são definidos como zero.  
  
 [c] Este é o tamanho do tipo de dados C correspondente.  
  
 Quando os dados SQL de data são convertidos em dados do caractere C, a seqüência resultante está no formato "*yyyy*-*mm*-*dd*". Este formato não é afetado pela configuração de país ® Windows.
