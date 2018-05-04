---
title: Estabelecer uma Conexão | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21b410afda6e5420b723360cdde03cb76f8b7293
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="establishing-a-connection"></a>Estabelecer uma Conexão
Depois de alocar identificadores de ambiente e conexão e definir quaisquer atributos de conexão, o aplicativo está pronto para se conectar à fonte de dados ou driver. Há três funções diferentes, o aplicativo pode usar para fazer isso: **SQLConnect** (nível de conformidade de interface de núcleo), **SQLDriverConnect** (Core), e **SQLBrowseConnect**(Nível 1). Cada um dos três foi projetada para ser usado em um cenário diferente. Antes de se conectar, o aplicativo pode determinar qual dessas funções é compatível com o **ConnectFunctions** palavra-chave retornada por **SQLDrivers**.  
  
> [!NOTE]  
>  Alguns drivers de limitam o número de conexões ativas, que eles oferecem suporte. Um aplicativo chama **SQLGetInfo** com a opção SQL_MAX_DRIVER_CONNECTIONS para determinar quantas conexões ativas oferece suporte a um driver específico.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Fonte de dados padrão](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conectando com SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Cadeias de conexão](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conectando-se com o SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectando com SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
