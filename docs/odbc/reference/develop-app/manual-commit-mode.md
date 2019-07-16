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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036405"
---
# <a name="manual-commit-mode"></a>Modo de confirmação manual
*No modo de confirmação manual* aplicativos explicitamente devem concluir as transações chamando **SQLEndTran** para confirmá-las ou revertê-los. Este é o modo de transação normal para a maioria dos bancos de dados relacionais.  
  
 As transações em ODBC não têm explicitamente seja iniciada. Em vez disso, uma transação começa implicitamente sempre que o aplicativo é iniciado para operar no banco de dados. Se a fonte de dados requer a iniciação de transação explícita, o driver deve fornecer a ele sempre que o aplicativo executa uma instrução que exigem uma transação e não há nenhuma transação atual.
