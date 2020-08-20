---
description: Modo de confirmação manual
title: Modo de confirmação manual | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb576166242078707846e005b958143812fd5901
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499830"
---
# <a name="manual-commit-mode"></a>Modo de confirmação manual
*No modo de confirmação manual,* os aplicativos devem concluir explicitamente as transações chamando **SQLEndTran** para confirmá-las ou redistribuí-las de volta. Esse é o modo de transação normal para a maioria dos bancos de dados relacionais.  
  
 As transações em ODBC não precisam ser iniciadas explicitamente. Em vez disso, uma transação começa implicitamente sempre que o aplicativo começa a operar no banco de dados. Se a fonte de dados exigir um início de transação explícito, o driver deverá fornecê-lo sempre que o aplicativo executar uma instrução que requer uma transação e não houver nenhuma transação atual.
