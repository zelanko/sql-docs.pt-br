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
ms.openlocfilehash: 87a5bababd2129ffb7e0aad36a2ceb3362d4acd9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792351"
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* cada operação de banco de dados é uma transação é confirmada quando executada. Esse modo é adequado para muitas transações reais que consistem em uma única instrução SQL. Não é necessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo com suporte. Nesses bancos de dados, as instruções são confirmadas quando eles são executados e não é possível revertê-los; eles são, portanto, sempre no modo de confirmação automática.  
  
 Se o DBMS subjacente não oferece suporte a transações de modo de confirmação automática, o driver poderá emulá-los ao confirmar manualmente cada instrução SQL, conforme ele é executado.  
  
 Se um lote de instruções SQL for executado no modo de confirmação automática, ele é específico da fonte de dados quando as instruções no lote são confirmadas. Eles podem ser confirmados conforme elas são executadas ou como um todo após todo o lote foi executado. Algumas fontes de dados podem oferecer suporte a ambos os comportamentos e podem fornecer uma maneira de selecionar um ou os outros. Em particular, se ocorrer um erro no meio do lote, ele é específico da fonte de dados se as instruções já executadas são confirmadas ou revertidas. Assim, aplicativos interoperáveis que usam lotes e exigem que eles deve ser confirmada ou revertida como um todo devem executar lotes apenas no modo de confirmação manual.
