---
title: Identificadores de conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299016"
---
# <a name="connection-handles"></a>Identificadores de conexão
Uma *conexão* consiste em um driver e uma fonte de dados. Um identificador de conexão identifica cada conexão. O identificador de conexão define não apenas o driver a ser usado, mas qual fonte de dados usar com esse driver. Dentro de um segmento de código que implementa o ODBC (o Gerenciador de driver ou um driver), o identificador de conexão identifica uma estrutura que contém informações de conexão, como as seguintes:  
  
-   O estado da conexão  
  
-   O diagnóstico no nível de conexão atual  
  
-   Os identificadores de instruções e descritores atualmente alocados na conexão  
  
-   As configurações atuais de cada atributo de conexão  
  
 O ODBC não impede várias conexões simultâneas, se o driver oferecer suporte a elas. Portanto, em um ambiente ODBC específico, vários identificadores de conexão podem apontar para uma variedade de drivers e fontes de dados, para o mesmo driver e uma variedade de fontes de dados, ou até mesmo para várias conexões com o mesmo driver e fonte de dados. Alguns drivers limitam o número de conexões ativas para as quais dão suporte; a opção SQL_MAX_DRIVER_CONNECTIONS em **SQLGetInfo** especifica a quantas conexões ativas um driver específico dá suporte.  
  
 Os identificadores de conexão são usados principalmente ao se conectar à fonte de dados (**SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**), desconectar-se da fonte de dados (**SQLDisconnect**), obter informações sobre o driver e a fonte de dados (**SQLGetInfo**), recuperar diagnósticos (**SQLGetDiagField** e **SQLGetDiagRec**) e executar transações (**SQLEndTran**). Eles também são usados ao definir e obter atributos de conexão (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e ao obter o formato nativo de uma instrução SQL (**SQLNativeSql**).  
  
 Os identificadores de conexão são alocados com **SQLAllocHandle** e liberados com **SQLFreeHandle**.
