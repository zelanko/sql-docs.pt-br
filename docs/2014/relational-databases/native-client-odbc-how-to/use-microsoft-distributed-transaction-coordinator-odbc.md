---
title: Usar o Microsoft Coordenador de Transações Distribuídas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 425f9fc0b7637aab1869130a2830c2f3c134fe7d
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688698"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Usar o Microsoft Coordenador de Transações Distribuídas (ODBC)
    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Para atualizar dois ou mais SQL Servers usando o MS DTC  
  
1.  Conecte-se ao MS DTC usando a função OLE DtcGetTransactionManager do MS DTC. Para obter informações sobre o MS DTC, consulte Microsoft Coordenador de Transações Distribuídas.  
  
2.  Chame o SQL DriverConnect uma vez para cada conexão de Microsoft SQL Server que você deseja estabelecer.  
  
3.  Chame a função OLE ITransactionDispenser:: BeginTransaction do MS DTC para iniciar uma transação do MS DTC e obter um objeto de transação que representa a transação.  
  
4.  Chame [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) uma ou mais vezes para cada conexão ODBC que você deseja inscrever na transação do MS DTC. O segundo parâmetro [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) deve ser SQL_ATTR_ENLIST_IN_DTC e o terceiro parâmetro deve ser o objeto Transaction (obtido na etapa 3).  
  
5.  Chame [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) uma vez para cada SQL Server que você deseja atualizar.  
  
6.  Chame a função OLE ITransaction:: Commit do MS DTC para confirmar a transação do MS DTC. O objeto de transação não é mais válido.  
  
 Para executar uma série de transações do MS DTC, repita as etapas 3 a 6.  
  
 Para liberar a referência ao objeto de transação, chame a função MS DTC OLE ITransaction:: Return.  
  
 Para usar uma conexão ODBC com uma transação do MS DTC e, em seguida, usar a mesma conexão com uma transação de SQL Server local, chame [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) com SQL_DTC_DONE.  
  
> [!NOTE]  
>  Você também pode chamar [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) e [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) por vez para cada SQL Server em vez de chamá-los como sugerido anteriormente nas etapas 4 e 5.  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações &#40;ODBC&#41;](../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
