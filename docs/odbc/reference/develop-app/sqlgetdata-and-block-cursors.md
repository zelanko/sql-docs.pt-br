---
title: SQLGetData e cursores em bloco | Microsoft Docs
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
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8642e5c228bb0e7976099d2151fe36f4db683f27
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursores em bloco
**SQLGetData** opera em uma única coluna de uma única linha e não é possível buscar uma matriz que contém dados de várias linhas. Isso ocorre porque o uso primário de **SQLGetData** é buscar dados longos em partes, e há pouco ou nenhum motivo para fazer isso para mais de uma linha por vez.  
  
 Para usar **SQLGetData** com um cursor em bloco, um aplicativo primeiro chama **SQLSetPos** para posicionar o cursor em uma única linha. Depois, ele chama **SQLGetData** para uma coluna na linha. No entanto, esse comportamento é opcional. Para determinar se um driver oferece suporte ao uso de **SQLGetData** com cursores em bloco, um aplicativo chama **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.
