---
title: Aplicativos multithread | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35768c262c3a2c0512a23049d6988eadfcb978d8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426855"
---
# <a name="multithreaded-applications"></a>Aplicativos multi-threaded
  O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é um driver multi-threaded. Criar um aplicativo multi-threaded é uma alternativa ao uso de chamadas assíncronas para processar várias chamadas de ODBC. Um thread pode fazer uma chamada de ODBC síncrona e outros threads podem ser processados enquanto o primeiro thread está bloqueado esperando a resposta à sua chamada. Esse modelo é mais eficiente que fazer chamadas assíncronas, pois elimina sobrecarga, como tráfego de rede e a realização repetida de testes de chamadas a funções ODBC para SQL_STILL_EXECUTING.  
  
 O modo assíncrono ainda é um método eficaz de processamento. As melhorias de desempenho de um modelo multi-threaded não são suficientes para justificar a reformulação de aplicativos assíncronos. Se os usuários estiverem convertendo aplicativos DB-Library que usam o modelo assíncrono do DB-Library, será mais fácil convertê-los ao modelo assíncrono do ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de driver ODBC do SQL Server Native Client](creating-a-driver-application.md)  
  
  
