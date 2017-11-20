---
title: Conectar-se com o SQLDriverConnect | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7bdfbf03fb4e67fcd0bc88ecf9212e3bb9cd7773
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

