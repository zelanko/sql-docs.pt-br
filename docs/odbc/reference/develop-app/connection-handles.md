---
title: Alças de conexão | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299016"
---
# <a name="connection-handles"></a>Identificadores de conexão
Uma *conexão* consiste em um driver e uma fonte de dados. Uma alça de conexão identifica cada conexão. O cabo de conexão define não apenas qual driver usar, mas qual fonte de dados usar com esse driver. Dentro de um segmento de código que implementa o ODBC (o Driver Manager ou um driver), o cabo de conexão identifica uma estrutura que contém informações de conexão, como a seguinte:  
  
-   O estado da conexão  
  
-   Os diagnósticos atuais em nível de conexão  
  
-   As alças de declarações e descritores atualmente alocados na conexão  
  
-   As configurações atuais de cada atributo de conexão  
  
 O ODBC não impede múltiplas conexões simultâneas, se o driver as suportar. Portanto, em um ambiente Específico do ODBC, vários punhos de conexão podem apontar para uma variedade de drivers e fontes de dados, para o mesmo driver e uma variedade de fontes de dados, ou mesmo para múltiplas conexões com o mesmo driver e fonte de dados. Alguns drivers limitam o número de conexões ativas que suportam; a opção SQL_MAX_DRIVER_CONNECTIONS no **SQLGetInfo** especifica quantas conexões ativas um determinado driver suporta.  
  
 As alças de conexão são usadas principalmente quando se conectam à fonte de dados (**SQLConnect,** **SQLDriverConnect,** ou **SQLBrowseConnect),** desconectando-se da fonte de dados **(SQLDisconnect),** obtendo informações sobre o driver e a fonte de dados **(SQLGetInfo),** recuperando diagnósticos **(SQLGetDiagField** e **SQLGetDiagRec),** e realizando transações **(SQLEndTran).** Eles também são usados ao definir e obter atributos de conexão **(SQLSetConnectAttr** e **SQLGetConnectAttr)** e ao obter o formato nativo de uma declaração SQL **(SQLNativeSql).**  
  
 As alças de conexão são alocadas com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.
