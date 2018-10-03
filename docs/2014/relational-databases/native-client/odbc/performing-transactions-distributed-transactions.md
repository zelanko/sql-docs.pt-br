---
title: Executando transações distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e59fe6624c84c9918e659063d4d46ca0d7337b4f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135906"
---
# <a name="performing-distributed-transactions"></a>Executando transações distribuídas
  O Coordenador de Transações Distribuídas da Microsoft (MS DTC) permite que os aplicativos estendam transações por duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Permite também que os aplicativos participem de transações gerenciadas por gerenciadores de transações compatíveis com o padrão XA/DTP do Open Group.  
  
 Normalmente, todos os comandos de gerenciamento de transações são enviados ao servidor pelo driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. O aplicativo inicia uma transação chamando [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) com o modo de confirmação automática desativado. O aplicativo, em seguida, executa as atualizações que compõem a transação e chama [SQLEndTran](../../native-client-odbc-api/sqlendtran.md) com a opção SQL_COMMIT ou SQL_ROLLBACK.  
  
 Ao usar o MS DTC, no entanto, o MS DTC se torna o Gerenciador de transações e o aplicativo não usa mais **SQLEndTran**.  
  
 Quando inscrita em uma transação distribuída, e em seguida se inscreve em uma segunda transação distribuída, o Driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sai da transação distribuída original e se inscreve na nova transação. Para obter mais informações, consulte [referência do programador de DTC](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
