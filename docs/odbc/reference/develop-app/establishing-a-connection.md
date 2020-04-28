---
title: Estabelecendo uma conexão | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298696"
---
# <a name="establishing-a-connection"></a>Estabelecer uma conexão
Depois de alocar identificadores de ambiente e conexão e definir qualquer atributo de conexão, o aplicativo estará pronto para se conectar à fonte de dados ou ao driver. Há três funções diferentes que o aplicativo pode usar para fazer isso: **SQLConnect** (nível de conformidade da interface principal), **SQLDriverConnect** (núcleo) e **SQLBrowseConnect** (nível 1). Cada um dos três é projetado para ser usado em um cenário diferente. Antes de se conectar, o aplicativo pode determinar quais dessas funções têm suporte com a palavra-chave **ConnectFunctions** retornada por **SQLDrivers**.  
  
> [!NOTE]  
>  Alguns drivers limitam o número de conexões ativas para as quais dão suporte. Um aplicativo chama **SQLGetInfo** com a opção SQL_MAX_DRIVER_CONNECTIONS para determinar a quantas conexões ativas um driver específico dá suporte.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Fonte de dados padrão](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conectar-se com o SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Cadeias de conexão](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conectar-se com o SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectar-se com o SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
