---
title: 'C a SQL: Binário | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818de0086ce3996cc1f6194311d2a2bb80c9f564
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292112"
---
# <a name="c-to-sql-binary"></a>C para SQL: binário
O identificador para o tipo binário de dados ODBC C é:  
  
 SQL_C_BINARY  
  
 A tabela a seguir mostra os tipos de dados SQL do ODBC para os quais os dados Binários C podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de byte de dados <= Comprimento do byte da coluna<br /><br /> Comprimento de byte de dados > comprimento de byte da coluna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento do caractere dos dados <= Comprimento do caractere da coluna<br /><br /> Comprimento do caractere dos dados > comprimento do caractere da Coluna|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|Comprimento de byte de dados = comprimento dos dados SQL<br /><br /> Comprimento de byte de dados <> comprimento de dados SQL|n/d<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|Comprimento dos dados <= comprimento da coluna<br /><br /> Comprimento do comprimento da coluna > de dados|n/d<br /><br /> 22001|
