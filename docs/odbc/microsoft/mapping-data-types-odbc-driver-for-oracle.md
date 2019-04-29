---
title: Mapeando tipos de dados (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ecdd7d7d4b597c4cae218e18b40b0f78e27a6bd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026869"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Tipos de dados de mapeamento (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O servidor Oracle dá suporte a um conjunto de tipos de dados. O Driver ODBC para Oracle mapeia esses tipos de dados para seus tipos de dados SQL ODBC apropriados. A tabela a seguir lista os tipos de dados do Oracle Server 7.3 e seus tipos de dados ODBC SQL correspondentes.  
  
 O Driver ODBC para Oracle dá suporte ao Oracle 7.3 e alguns tipos de dados Oracle8. Para obter mais informações sobre tipos de dados Oracle8 com suporte, consulte [suporte para tipos de dados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo de dados do servidor Oracle|Tipo de dados SQL do ODBC|  
|-----------------------------|------------------------|  
|CHAR|SQL_CHAR|  
|DATE|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_DECIMAL|  
|LONG|SQL_LONGVARCHAR|  
|LONG RAW|SQL_LONGVARBINARY|  
|NUMBER|SQL_DECIMAL|  
|RAW|SQL_VARBINARY|  
|VARCHAR2|SQL_VARCHAR|  
  
> [!NOTE]  
>  Para obter mais informações sobre o tamanho permitido da coluna VARCHAR, consulte [tamanho da coluna VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
