---
title: Mapeamento de tipos de dados (Driver ODBC para Oracle) | Microsoft Docs
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
ms.openlocfilehash: 432c21b70efcdd63ef36bfe3d26f8488ddb11d1d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302667"
---
# <a name="mapping-data-types-odbc-driver-for-oracle"></a>Tipos de dados de mapeamento (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Oracle Server suporta um conjunto de tipos de dados. O Driver ODBC para Oracle mapeia esses tipos de dados para seus tipos de dados ODBC SQL apropriados. A tabela a seguir lista os tipos de dados do Oracle 7.3 Server e seus tipos de dados ODBC SQL correspondentes.  
  
 O Driver ODBC para Oracle suporta oracle 7.3 e alguns tipos de dados Oracle8. Para obter mais informações sobre os tipos de dados Oracle8 suportados, consulte [Tipos de dados suportados](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md).  
  
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
>  Para obter mais informações sobre o tamanho permitido da coluna VARCHAR, consulte [varchar tamanho da coluna](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
