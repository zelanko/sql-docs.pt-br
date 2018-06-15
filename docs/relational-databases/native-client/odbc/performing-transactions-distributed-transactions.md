---
title: Executando transações distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2e75f8506a1bb7d58dd9e9669b241031d118ea4b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32949971"
---
# <a name="performing-transactions---distributed-transactions"></a>Executando transações - transações distribuídas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O Coordenador de Transações Distribuídas da Microsoft (MS DTC) permite que os aplicativos estendam transações por duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Permite também que os aplicativos participem de transações gerenciadas por gerenciadores de transações compatíveis com o padrão XA/DTP do Open Group.  
  
 Normalmente, todos os comandos de gerenciamento de transações são enviados ao servidor pelo driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. O aplicativo inicia uma transação chamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com o modo de confirmação automática desativado. O aplicativo executa as atualizações que incluem a transação e chama [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) com a opção SQL_COMMIT ou SQL_ROLLBACK.  
  
 Ao usar o MS DTC, no entanto, o MS DTC se torna o Gerenciador de transações e o aplicativo não usa mais **SQLEndTran**.  
  
 Quando inscrita em uma transação distribuída, e em seguida se inscreve em uma segunda transação distribuída, o Driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client sai da transação distribuída original e se inscreve na nova transação. Para obter mais informações, consulte [referência do programador de DTC](http://msdn.microsoft.com/library/ms686108\(VS.85\).aspx).  
  
## <a name="see-also"></a>Consulte também  
 [Executando transações & #40; ODBC & #41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
