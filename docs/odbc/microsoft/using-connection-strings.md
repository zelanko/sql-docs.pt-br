---
title: Usando cadeias de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 496fe10fbf49f4d712127e2e4122c50fa20ba2be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044577"
---
# <a name="using-connection-strings"></a>Usar cadeias de conexão
Você pode usar uma cadeia de conexão para se conectar a uma fonte de dados do Visual FoxPro.  
  
 Por exemplo, para se conectar à fonte de dados TasTrade e substituir a configuração atual de exclusivo associada à fonte de dados, você usaria a cadeia de caracteres:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Para obter uma lista das palavras-chave e dos valores do atributo que você pode incluir na cadeia de conexão, consulte [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Para obter uma explicação completa da sintaxe da cadeia de conexão, consulte [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) na *referência do programador de ODBC*.
