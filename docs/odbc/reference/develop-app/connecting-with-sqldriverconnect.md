---
title: Conectar-se com o SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b8285ca9fddf0e1b77ca171414e4c00b0029d110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036498"
---
# <a name="connecting-with-sqldriverconnect"></a>Conectar-se com o SQLDriverConnect
**SQLDriverConnect** é usado para se conectar a uma fonte de dados usando uma cadeia de caracteres de conexão. **SQLDriverConnect** é usado em vez de **SQLConnect** pelos seguintes motivos:  
  
-   Para permitir que o aplicativo use as informações de conexão específicas do driver.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Para se conectar sem especificar uma fonte de dados.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Informações de conexão específicas de driver](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [Solicitando o usuário para informações de conexão](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [Conectando-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [Conectando-se diretamente a drivers](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
