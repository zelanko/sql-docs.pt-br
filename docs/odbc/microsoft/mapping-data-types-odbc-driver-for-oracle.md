---
description: Tipos de dados de mapeamento (Driver ODBC para Oracle)
title: Mapeando tipos de dados (driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ea39a8277508422028d5794ccbcb7a62dacdb08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483508"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Tipos de dados de mapeamento (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O servidor Oracle dá suporte a um conjunto de tipos de dados. O ODBC driver for Oracle mapeia esses tipos de dados para seus tipos de dados SQL ODBC apropriados. A tabela a seguir lista os tipos de dados do servidor Oracle 7,3 e seus tipos de dados SQL ODBC correspondentes.  
  
 O ODBC driver for Oracle dá suporte ao Oracle 7,3 e a alguns tipos de dados Oracle8. Para obter mais informações sobre tipos de dados Oracle8 com suporte, consulte [tipos de dados com suporte](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
|Tipo de dados do servidor Oracle|Tipo de dados SQL ODBC|  
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
>  Para obter mais informações sobre o tamanho permitido da coluna VARCHAR, consulte [varchar Column size](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
