---
title: Estabelecendo uma Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establishing a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establishing a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f71190a8a2ca1dd8af0d28adb5531540fb1b57e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298696"
---
# <a name="establishing-a-connection"></a>Estabelecer uma conexão
Depois de alocar o ambiente e as alças de conexão e definir quaisquer atributos de conexão, o aplicativo está pronto para se conectar à fonte de dados ou driver. Existem três funções diferentes que o aplicativo pode usar para fazer isso: **SQLConnect** (nível de conformidade da interface principal), **SQLDriverConnect** (Core) e **SQLBrowseConnect** (Nível 1). Cada um dos três foi projetado para ser usado em um cenário diferente. Antes de conectar, o aplicativo pode determinar qual dessas funções é suportada com a palavra-chave **ConnectFunctions** retornada por **SQLDrivers**.  
  
> [!NOTE]  
>  Alguns drivers limitam o número de conexões ativas que suportam. Um aplicativo chama **o SQLGetInfo** com a opção SQL_MAX_DRIVER_CONNECTIONS para determinar quantas conexões ativas um determinado driver suporta.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Fonte de dados padrão](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conectar-se com o SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Strings de conexão](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conectar-se com o SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectar-se com o SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
