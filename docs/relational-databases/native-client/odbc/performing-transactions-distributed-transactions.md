---
title: Criar transações distribuídas | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 537537ef2f3dd07a27ffcb4d092be2f8719f6ee1
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907382"
---
# <a name="create-a-distributed-transaction"></a>Criar uma transação distribuída

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

Uma transação distribuída pode ser criada para diferentes sistemas Microsoft SQL de diferentes maneiras.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>O driver ODBC chama o MSDTC para SQL Server local

O Microsoft Coordenador de Transações Distribuídas (MSDTC) permite que os aplicativos estendam ou _distribuam_ uma transação entre duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A transação distribuída funciona mesmo quando as duas instâncias são hospedadas em computadores separados.

O MSDTC é instalado para Microsoft SQL Server local, mas não está disponível para o serviço de nuvem do banco de dados SQL do Microsoft Azure.

O MSDTC é chamado pelo driver de SQL Server Native Client para ODBC (Open Database Connectivity), quando C++ o seu programa gerencia uma transação distribuída. O driver ODBC do Native Client tem um Gerenciador de transações que é compatível com o padrão XA do DTP (processamento de transações distribuídas) do grupo aberto. Essa conformidade é exigida pelo MSDTC. Normalmente, todos os comandos de gerenciamento de transações são enviados por meio desse driver ODBC do Native Client. A sequência é a seguinte:

1. Seu C++ aplicativo ODBC de cliente nativo inicia uma transação chamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), com o modo de confirmação automática desativado.

2. O aplicativo atualiza alguns dados no SQL Server X no computador A.

3. O aplicativo atualiza alguns dados no SQL Server Y no computador B.
    - Se uma atualização em SQL Server Y falhar, todas as atualizações não confirmadas em ambas as instâncias de SQL Server serão revertidas.

4. Por fim, o aplicativo encerra a transação chamando [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md), com a opção SQL_COMMIT ou SQL_ROLLBACK.

_(1)_ o MSDTC pode ser invocado sem ODBC. Nesse caso, o MSDTC torna-se o Gerenciador de transações e o aplicativo não usa mais **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Apenas uma transação distribuída

Suponha que seu C++ aplicativo ODBC de cliente nativo esteja inscrito em uma transação distribuída. Em seguida, o aplicativo se lista em uma segunda transação distribuída. Nesse caso, o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client deixa a transação distribuída original e as inlistas na nova transação distribuída.

Para obter mais informações, consulte [referência do programador do DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#alternativa para o banco de dados SQL na nuvem

O MSDTC não tem suporte para o banco de dados SQL do Azure nem para o Azure SQL Data Warehouse.

No entanto, uma transação distribuída pode ser criada para o banco C# de dados SQL fazendo com que seu programa use a classe .NET [System. Transactions. TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Outras linguagens de programação

As outras linguagens de programação a seguir podem não fornecer nenhum suporte para transações distribuídas com o serviço do banco de dados SQL:

- Nativo C++ que usam drivers ODBC
- Servidor vinculado usando Transact-SQL
- Drivers JDBC

## <a name="see-also"></a>Confira também

[Executando transações (ODBC)](performing-transactions-in-odbc.md)
