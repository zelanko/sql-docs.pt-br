---
description: Conectar-se com o SQLDriverConnect
title: Conectando-se ao SQLDriverConnect | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 298461f5a1cb4758b3dc3d7bbddb1bb9f04ac577
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424808"
---
# <a name="connecting-with-sqldriverconnect"></a>Conectar-se com o SQLDriverConnect
**SQLDriverConnect** é usado para se conectar a uma fonte de dados usando uma cadeia de conexão. **SQLDriverConnect** é usado em vez de **SQLConnect** pelos seguintes motivos:  
  
-   Para permitir que o aplicativo use informações de conexão específicas do driver.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Para se conectar sem especificar uma fonte de dados.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Informações de conexão específicas de driver](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [Solicitar o usuário para informações de conexão](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [Conectar-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [Conectar-se diretamente a drivers](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
