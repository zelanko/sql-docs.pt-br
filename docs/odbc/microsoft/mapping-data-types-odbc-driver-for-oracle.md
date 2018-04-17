---
title: Mapeando tipos de dados (ODBC Driver for Oracle) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- mapping data types [ODBC]
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: a5d9ce12-19da-4943-8493-e3d56fa08348
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a87220ab330cc7dab4337aa6592ee9f08443d431
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Mapeando tipos de dados (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O servidor Oracle oferece suporte a um conjunto de tipos de dados. O Driver ODBC do Oracle mapeia esses tipos de dados para seus tipos de dados SQL ODBC apropriados. A tabela a seguir lista os tipos de dados do Oracle Server 7.3 e seus tipos de dados ODBC SQL correspondentes.  
  
 O Driver ODBC do Oracle oferece suporte ao Oracle 7.3 e alguns tipos de dados do Oracle8. Para obter mais informações sobre tipos de dados Oracle8 com suporte, consulte [suporte para tipos de dados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo de dados do Oracle Server|Tipo de dados ODBC SQL|  
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
>  Para obter mais informações sobre o tamanho permitido da coluna de VARCHAR, consulte [tamanho da coluna de VARCHAR](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
