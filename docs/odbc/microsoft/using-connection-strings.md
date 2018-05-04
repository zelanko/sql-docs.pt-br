---
title: Usando cadeias de caracteres de Conexão | Microsoft Docs
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
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1e492423fec8f214890dfa7aa2f75c8a6ce19da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-strings"></a>Usando cadeias de caracteres de Conexão
Você pode usar uma cadeia de caracteres de conexão para se conectar a uma fonte de dados do Visual FoxPro.  
  
 Por exemplo, para se conectar à fonte de dados TasTrade e substituir que a configuração atual de exclusivo associada com a fonte de dados, você usaria a cadeia de caracteres:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Para obter uma lista das palavras-chave do atributo e valores que você pode incluir na cadeia de conexão, consulte [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Para obter uma explicação completa da sintaxe de cadeia de caracteres de conexão, consulte [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) no *referência do programador de ODBC*.
