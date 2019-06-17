---
title: Criar um transações distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ea6c4886a3c5397777b7a65afe96ab7e1b422bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65620547"
---
# <a name="create-a-distributed-transaction"></a>Criar uma transação distribuída

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

Uma transação distribuída pode ser criada para diferentes sistemas do Microsoft SQL de maneiras diferentes.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Driver ODBC chama o MSDTC para o SQL Server no local

O Microsoft Distributed Transaction coordenador (MSDTC) permite que os aplicativos estender ou _distribuir_ uma transação entre dois ou mais instâncias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A transação distribuída funciona mesmo quando as duas instâncias são hospedadas em computadores separados.

MSDTC está instalado para o Microsoft SQL Server no local, mas não está disponível para o serviço de nuvem do banco de dados SQL da Microsoft.

MSDTC é chamado pelo driver do SQL Server Native Client para Open Database Connectivity (ODBC), quando o C++ programa gerencia uma transação distribuída. O driver ODBC do Native Client tem um Gerenciador de transação que está em conformidade com a abrir grupo Distributed transação de processamento (DTP) padrão XA. Essa conformidade é exigida pelo MSDTC. Normalmente, todos os comandos de gerenciamento de transação são enviados por esse driver ODBC do Native Client. A sequência é da seguinte maneira:

1. O C++ aplicativo de ODBC do Native Client inicia uma transação chamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), com o modo de confirmação automática desativado.

2. O aplicativo atualiza alguns dados no SQL Server X no computador A.

3. O aplicativo atualiza alguns dados no SQL Server Y no computador B.
    - Se uma atualização do SQL Server Y falhar, todas as atualizações não confirmadas em ambas as instâncias do SQL Server são revertidas.

4. Por fim, o aplicativo termina a transação chamando [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md), com a opção SQL_COMMIT ou SQL_ROLLBACK.

_(1)_  MSDTC pode ser invocado sem ODBC. Nesse caso, o MSDTC se torna o Gerenciador de transações e o aplicativo não usa mais **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Somente uma transação distribuída

Suponha que seu C++ aplicativo de ODBC do Native Client está inscrita em uma transação distribuída. Em seguida, o aplicativo se inscreve em uma segunda transação distribuída. Nesse caso, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client deixa a transação distribuída original e se inscreve na nova transação distribuída.

Para obter mais informações, consulte [referência do programador de DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#alternativa para o banco de dados SQL na nuvem

MSDTC não é suportado para o banco de dados SQL ou SQL Data Warehouse do Azure.

No entanto, uma transação distribuída pode ser criada para banco de dados SQL fazendo com que seu C# programa de usar a classe do .NET [Transactions](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Outras linguagens de programação

A seguir outras linguagens de programação podem não fornecer nenhum suporte para transações distribuídas com o serviço de banco de dados SQL:

- Nativo C++ que usam drivers ODBC
- Servidor vinculado usando o Transact-SQL
- Drivers JDBC

## <a name="see-also"></a>Confira também

[Executando transações (ODBC)](performing-transactions-in-odbc.md)
