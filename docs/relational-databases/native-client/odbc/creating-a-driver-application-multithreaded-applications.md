---
title: Aplicativos multithread | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d557b9195e14f4546d8b003f52bebdb7f0c2065b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419495"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>Criando um aplicativo de Driver – aplicativos multithread
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é um driver multi-threaded. Criar um aplicativo multi-threaded é uma alternativa ao uso de chamadas assíncronas para processar várias chamadas de ODBC. Um thread pode fazer uma chamada de ODBC síncrona e outros threads podem ser processados enquanto o primeiro thread está bloqueado esperando a resposta à sua chamada. Esse modelo é mais eficiente que fazer chamadas assíncronas, pois elimina sobrecarga, como tráfego de rede e a realização repetida de testes de chamadas a funções ODBC para SQL_STILL_EXECUTING.  
  
 O modo assíncrono ainda é um método eficaz de processamento. As melhorias de desempenho de um modelo multi-threaded não são suficientes para justificar a reformulação de aplicativos assíncronos. Se os usuários estiverem convertendo aplicativos DB-Library que usam o modelo assíncrono do DB-Library, será mais fácil convertê-los ao modelo assíncrono do ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de driver ODBC do SQL Server Native Client](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
