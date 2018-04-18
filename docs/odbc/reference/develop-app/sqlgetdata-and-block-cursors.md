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
ms.topic: article
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
ms.workload: Inactive
ms.openlocfilehash: 29b41623fe5f4681401e9726adbc1b0993ef98b4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursores em bloco
**SQLGetData** opera em uma única coluna de uma única linha e não é possível buscar uma matriz que contém dados de várias linhas. Isso ocorre porque o uso primário de **SQLGetData** é buscar dados longos em partes, e há pouco ou nenhum motivo para fazer isso para mais de uma linha por vez.  
  
 Para usar **SQLGetData** com um cursor em bloco, um aplicativo primeiro chama **SQLSetPos** para posicionar o cursor em uma única linha. Depois, ele chama **SQLGetData** para uma coluna na linha. No entanto, esse comportamento é opcional. Para determinar se um driver oferece suporte ao uso de **SQLGetData** com cursores em bloco, um aplicativo chama **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.
