---
description: SQLGetData e cursores em bloco
title: SQLGetData e cursores de bloco | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53358b2d4d8dfef1a5a820ed3943f07a584a595
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424488"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursores em bloco
**SQLGetData** opera em uma única coluna de uma única linha e não pode buscar uma matriz que contenha dados de várias linhas. Isso ocorre porque o uso principal de **SQLGetData** é buscar dados longos em partes, e há pouco ou nenhum motivo para fazer isso para mais de uma linha por vez.  
  
 Para usar **SQLGetData** com um cursor de bloco, um aplicativo primeiro chama **SQLSetPos** para posicionar o cursor em uma única linha. Em seguida, ele chama **SQLGetData** para uma coluna nessa linha. No entanto, esse comportamento é opcional. Para determinar se um driver dá suporte ao uso de **SQLGetData** com cursores de bloco, um aplicativo chama **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.
