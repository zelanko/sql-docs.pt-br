---
title: Modo de confirmação automática | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f19053eec7a48eba7a51425b01744f3acd10015
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285106"
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* toda operação de banco de dados é uma transação que é cometida quando realizada. Este modo é adequado para muitas transações do mundo real que consistem em uma única declaração SQL. É desnecessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo suportado. Nesses bancos de dados, as declarações são cometidas quando são executadas e não há como reverlá-las; portanto, eles estão sempre no modo de confirmação automática.  
  
 Se o DBMS subjacente não suportar transações de modo de confirmação automática, o driver poderá emulá-las cometendo manualmente cada declaração SQL à medida que for executada.  
  
 Se um lote de instruções SQL for executado no modo de confirmação automática, será específico da fonte de dados quando as declarações no lote forem comprometidas. Eles podem ser cometidos à medida que são executados ou como um todo depois que todo o lote foi executado. Algumas fontes de dados podem apoiar esses dois comportamentos e podem fornecer uma maneira de selecionar um ou outros. Em particular, se ocorrer um erro no meio do lote, é específico da fonte de dados se as declarações já executadas são cometidas ou revertidas. Assim, os aplicativos interoperáveis que usam lotes e exigem que eles sejam comprometidos ou revertidos como um todo devem executar lotes apenas no modo de confirmação manual.
