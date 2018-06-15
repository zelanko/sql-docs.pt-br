---
title: Modo de confirmação automática | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- auto-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: c8de5b60-d147-492d-b601-2eeae8511d00
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 679bbb3486c947ef3ebbd7d285f74f3cb510172f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908601"
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* cada operação de banco de dados é uma transação que é confirmada quando executada. Esse modo é adequado para muitas transações reais que consistem em uma única instrução SQL. Não é necessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo com suporte. Nesses bancos de dados, instruções são confirmadas quando eles são executados e não é possível revertê-los; eles são, portanto, sempre em modo de confirmação automática.  
  
 Se o DBMS subjacente não oferece suporte a transações de modo de confirmação automática, o driver pode emulá-los ao confirmar manualmente cada instrução SQL, conforme ele é executado.  
  
 Se um lote de instruções SQL é executado em modo de confirmação automática, é específico da fonte de dados quando as instruções no lote são confirmadas. Elas podem ser confirmadas à medida que eles são executados, ou como um todo depois que todo o lote foi executado. Algumas fontes de dados podem oferecer suporte a ambos os comportamentos e podem fornecer uma maneira de selecionar um ou os outros. Em particular, se ocorrer um erro no meio do lote, ele é específico da fonte de dados se as instruções executadas já estão confirmadas ou revertidas. Dessa forma, aplicativos interoperáveis que usam lotes e exigem a ser confirmada ou revertida como um todo devem executar lotes apenas no modo de confirmação manual.
