---
title: Conectando-se com o SQLDriverConnect | Microsoft Docs
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
ms.openlocfilehash: 6cd95364d8a5316a50d9f55616236a8677bf99e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299066"
---
# <a name="connecting-with-sqldriverconnect"></a>Conectar-se com o SQLDriverConnect
**O SQLDriverConnect** é usado para se conectar a uma fonte de dados usando uma seqüência de conexões. **O SQLDriverConnect** é usado em vez do **SQLConnect** pelas seguintes razões:  
  
-   Para permitir que o aplicativo use informações de conexão específicas do driver.  
  
-   Para solicitar que o driver instrua o usuário a fornecer informações de conexão.  
  
-   Conectar sem especificar uma fonte de dados.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Informações de conexão específicas de driver](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [Solicitar o usuário para informações de conexão](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [Conectar-se usando fontes de dados de arquivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [Conectar-se diretamente a drivers](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
