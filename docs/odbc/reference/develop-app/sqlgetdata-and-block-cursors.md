---
title: SQLGetData e cursores em bloco | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4841d8d923ff73d187569df3d7f9e29daf0f4e48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107405"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursores em bloco
**SQLGetData** opera em uma única coluna de uma única linha e não é possível buscar uma matriz que contém dados de várias linhas. Isso ocorre porque o uso primário dos **SQLGetData** é buscar dados longos em partes, e há pouco ou nenhum motivo para fazer isso para mais de uma linha por vez.  
  
 Para usar **SQLGetData** com um cursor em bloco, um aplicativo primeiro chama **SQLSetPos** para posicionar o cursor em uma única linha. Em seguida, ele chama **SQLGetData** para uma coluna nessa linha. No entanto, esse comportamento é opcional. Para determinar se um driver suporta o uso de **SQLGetData** com cursores em bloco, um aplicativo chama **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.
