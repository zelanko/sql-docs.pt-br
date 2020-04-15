---
title: SQLGetData e Cursors de Bloco | Microsoft Docs
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
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299746"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData e cursores em bloco
**O SQLGetData** opera em uma única coluna de uma única linha e não pode buscar uma matriz contendo dados de várias linhas. Isso porque o uso principal do **SQLGetData** é buscar dados longos em partes, e há pouca ou nenhuma razão para fazer isso por mais de uma linha de cada vez.  
  
 Para usar **o SQLGetData** com um cursor de bloco, um aplicativo primeiro chama **SQLSetPos** para posicionar o cursor em uma única linha. Em seguida, ele chama **SQLGetData** para uma coluna nessa linha. No entanto, esse comportamento é opcional. Para determinar se um driver suporta o uso do **SQLGetData** com cursores de bloco, um aplicativo chama **SQLGetInfo** com a opção SQL_GETDATA_EXTENSIONS.
