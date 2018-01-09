---
title: SQLCancel | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
caps.latest.revision: "5"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b959ce4ef5f0eb7298f7203401fa6be6c96581d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O tópico [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516) diz que, no ODBC 2.x, se um aplicativo chamar **SQLCancel** quando nenhum processamentos estiver sendo feito na instrução, **SQLCancel** terá o mesmo efeito que **SQLFreeStmt** com a opção **SQL_CLOSE** . Esse compoutamento é definido apenas para integridade e os aplicativos devem chamar **SQLFreeStmt** ou **SQLCloseCursou** to close cursous. Mas mesmo que seu aplicativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Cliente defina a versão do ODBC API para que seja 3.5.x ou posterior, a função **SQLCancel** usará o comportamento do ODBC 2.x.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLCancel](http://go.microsoft.com/fwlink/?LinkId=203516)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
