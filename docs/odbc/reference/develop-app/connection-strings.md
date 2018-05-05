---
title: Cadeias de caracteres de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5b88b1056d8b645614a7f17fd6edf81eb804f16
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connection-strings"></a>Cadeias de Conexão
Uma cadeia de caracteres de conexão contém informações usadas para estabelecer uma conexão. Uma cadeia de caracteres de conexão completa contém todas as informações necessárias para estabelecer uma conexão. A cadeia de caracteres de conexão é uma série de pares de palavra-chave/valor separados por ponto e vírgula. (Para obter a sintaxe completa de uma cadeia de caracteres de conexão, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.) A cadeia de caracteres de conexão é usada pelo:  
  
-   **SQLDriverConnect**, que conclui a cadeia de caracteres de conexão, a interação com o usuário.  
  
-   **SQLBrowseConnect**, que conclui a cadeia de caracteres de conexão iterativamente com a fonte de dados.  
  
 **SQLConnect** não usa uma cadeia de caracteres de conexão; usando **SQLConnect** é análogo ao se conectar usando uma cadeia de caracteres de conexão com exatamente três pares de palavra-chave/valor (para o nome da fonte de dados e, opcionalmente, o usuário ID e senha) .
