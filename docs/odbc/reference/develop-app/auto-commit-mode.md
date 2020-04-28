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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285106"
---
# <a name="auto-commit-mode"></a>Modo de confirmação automática
*No modo de confirmação automática,* cada operação de banco de dados é uma transação que é confirmada quando executada. Esse modo é adequado para muitas transações do mundo real que consistem em uma única instrução SQL. Não é necessário delimitar ou especificar a conclusão dessas transações. Em bancos de dados sem suporte a transações, o modo de confirmação automática é o único modo com suporte. Nesses bancos de dados, as instruções são confirmadas quando são executadas e não há nenhuma maneira de revertida-las; Portanto, eles estão sempre no modo de confirmação automática.  
  
 Se o DBMS subjacente não oferecer suporte a transações do modo de confirmação automática, o driver poderá emular esses itens confirmando manualmente cada instrução SQL conforme ela for executada.  
  
 Se um lote de instruções SQL for executado no modo de confirmação automática, ele será específico da fonte de dados quando as instruções no lote forem confirmadas. Eles podem ser confirmados à medida que são executados ou como um todo após a execução do lote inteiro. Algumas fontes de dados podem dar suporte a esses dois comportamentos e podem fornecer uma maneira de selecionar um ou outros. Em particular, se ocorrer um erro no meio do lote, ele será específico da fonte de dados se as instruções já executadas forem confirmadas ou revertidas. Assim, aplicativos interoperáveis que usam lotes e exigem que eles sejam confirmados ou revertidos como um todo devem executar lotes somente no modo de confirmação manual.
