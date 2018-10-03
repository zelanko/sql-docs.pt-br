---
title: Identificadores de Conexão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77fdb63f346ada40346544a53c3ff69db0a8a9a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828934"
---
# <a name="connection-handles"></a>Identificadores de conexão
Um *conexão* consiste em um driver e uma fonte de dados. Um identificador de conexão identifica cada conexão. O identificador de conexão define não apenas qual driver a ser usado, mas qual fonte de dados para usar com esse driver. Dentro de um segmento de código que implementa o ODBC (o Gerenciador de Driver ou um driver), o identificador de conexão identifica uma estrutura que contém informações de conexão, como o seguinte:  
  
-   O estado da conexão  
  
-   O diagnóstico de nível de conexão atuais  
  
-   Os identificadores de instruções e descritores de alocado no momento em que a conexão  
  
-   As configurações atuais de cada atributo de conexão  
  
 ODBC não impede que várias conexões simultâneas, se o driver oferece suporte a eles. Portanto, em um ambiente ODBC específico, vários identificadores de conexão podem apontar para uma variedade de drivers e fontes de dados para o mesmo driver e uma variedade de fontes de dados, ou até mesmo várias conexões com o mesmo driver e a fonte de dados. Alguns drivers de limitam o número de conexões ativas, que dar suporte a eles; opção o SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** Especifica quantas conexões ativas que dá suporte a um driver específico.  
  
 Identificadores de Conexão são usados principalmente ao se conectar à fonte de dados (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**), desconectar-se de que os dados fonte (**SQLDisconnect**), obtendo informações sobre a fonte de dados e driver (**SQLGetInfo**), recuperando o diagnóstico (**SQLGetDiagField** e **SQLGetDiagRec**) e a execução de transações (**SQLEndTran**). Eles também são usados quando estiver definindo e Obtendo atributos de conexão (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e ao obter o formato nativo de uma instrução SQL (**SQLNativeSql** ).  
  
 Identificadores de Conexão são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
