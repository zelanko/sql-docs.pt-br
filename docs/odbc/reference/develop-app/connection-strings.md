---
title: Cadeias de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f68a87db729df2f4a27e2766a9de60e8c75a71a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036418"
---
# <a name="connection-strings"></a>Cadeias de Conexão
Uma cadeia de conexão contém informações usadas para estabelecer uma conexão. Uma cadeia de conexão completa contém todas as informações necessárias para estabelecer uma conexão. A cadeia de conexão é uma série de pares de palavras-chave/valor separados por ponto e vírgula. (Para obter a sintaxe completa de uma cadeia de conexão, consulte a descrição da função [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .) A cadeia de conexão é usada por:  
  
-   **SQLDriverConnect**, que conclui a cadeia de conexão por interação com o usuário.  
  
-   **SQLBrowseConnect**, que conclui a cadeia de conexão iterativamente com a fonte de dados.  
  
 O **SQLConnect** não usa uma cadeia de conexão; o uso de **SQLConnect** é análogo à conexão usando uma cadeia de conexão com exatamente três pares de palavras-chave/valor (para o nome da fonte de dados e, opcionalmente, a ID de usuário e a senha).
