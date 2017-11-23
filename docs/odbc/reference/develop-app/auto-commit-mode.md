---
title: "Modo de confirmação automática | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e2127d5b33c5ea4bf2a0c96c5e020322aec39db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* cada operação de banco de dados é uma transação que é confirmada quando executada. Esse modo é adequado para muitas transações reais que consistem em uma única instrução SQL. Não é necessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo com suporte. Nesses bancos de dados, instruções são confirmadas quando eles são executados e não é possível revertê-los; eles são, portanto, sempre em modo de confirmação automática.  
  
 Se o DBMS subjacente não oferece suporte a transações de modo de confirmação automática, o driver pode emulá-los ao confirmar manualmente cada instrução SQL, conforme ele é executado.  
  
 Se um lote de instruções SQL é executado em modo de confirmação automática, é específico da fonte de dados quando as instruções no lote são confirmadas. Elas podem ser confirmadas à medida que eles são executados, ou como um todo depois que todo o lote foi executado. Algumas fontes de dados podem oferecer suporte a ambos os comportamentos e podem fornecer uma maneira de selecionar um ou os outros. Em particular, se ocorrer um erro no meio do lote, ele é específico da fonte de dados se as instruções executadas já estão confirmadas ou revertidas. Dessa forma, aplicativos interoperáveis que usam lotes e exigem a ser confirmada ou revertida como um todo devem executar lotes apenas no modo de confirmação manual.
