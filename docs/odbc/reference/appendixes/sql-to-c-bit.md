---
title: 'SQL para C: Bit | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296746"
---
# <a name="sql-to-c-bit"></a>SQL para C: bit
O identificador para o bit ODBC SQL tipo de dados é:  
  
 SQL_BIT  
  
 A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL de bit podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*Comprimento de buffer* > 1<br /><br /> *Comprimento tampão* <= 1|Dados<br /><br /> Indefinido|1<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Nenhum[a]|Dados|Tamanho do tipo de dados C|n/d|  
|SQL_C_BIT|Nenhum[a]|Dados|1[b]|n/d|  
|SQL_C_BINARY|*Comprimento tampão* >= 1<br /><br /> *Comprimento de buffer* < 1|Dados<br /><br /> Indefinido|1<br /><br /> Indefinido|n/d<br /><br /> 22003|  
  
 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.  
  
 Quando os dados SQL de bit são convertidos em dados de caractere C, os valores possíveis são "0" e "1".
