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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 491fb8db9e37cfb3bfa07881958fe7828e6bb911
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63048420"
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* cada operação de banco de dados é uma transação é confirmada quando executada. Esse modo é adequado para muitas transações reais que consistem em uma única instrução SQL. Não é necessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo com suporte. Nesses bancos de dados, as instruções são confirmadas quando eles são executados e não é possível revertê-los; eles são, portanto, sempre no modo de confirmação automática.  
  
 Se o DBMS subjacente não oferece suporte a transações de modo de confirmação automática, o driver poderá emulá-los ao confirmar manualmente cada instrução SQL, conforme ele é executado.  
  
 Se um lote de instruções SQL for executado no modo de confirmação automática, ele é específico da fonte de dados quando as instruções no lote são confirmadas. Eles podem ser confirmados conforme elas são executadas ou como um todo após todo o lote foi executado. Algumas fontes de dados podem oferecer suporte a ambos os comportamentos e podem fornecer uma maneira de selecionar um ou os outros. Em particular, se ocorrer um erro no meio do lote, ele é específico da fonte de dados se as instruções já executadas são confirmadas ou revertidas. Assim, aplicativos interoperáveis que usam lotes e exigem que eles deve ser confirmada ou revertida como um todo devem executar lotes apenas no modo de confirmação manual.
