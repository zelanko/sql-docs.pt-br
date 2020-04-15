---
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
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287870"
---
# <a name="manual-commit-mode"></a>Modo de confirmação manual
*No modo de confirmação manual,* os aplicativos devem concluir explicitamente as transações ligando para **o SQLEndTran** para comprometê-las ou revertê-las. Este é o modo normal de transação para a maioria dos bancos de dados relacionais.  
  
 As transações na ODBC não devem ser explicitamente iniciadas. Em vez disso, uma transação começa implicitamente sempre que o aplicativo começa a operar no banco de dados. Se a fonte de dados exigir início explícito da transação, o motorista deve fornecê-lo sempre que o aplicativo executar uma declaração exigindo uma transação e não houver transação atual.
