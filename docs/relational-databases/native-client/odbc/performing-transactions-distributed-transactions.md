---
title: Criar uma transações distribuídas | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303672"
---
# <a name="create-a-distributed-transaction"></a>Criar uma transação distribuída

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


Uma transação distribuída pode ser criada para diferentes sistemas Microsoft SQL de diferentes maneiras.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Driver ODBC chama o MSDTC para SQL Server no local

O Microsoft Distributed Transaction Coordinator (MSDTC) permite que os aplicativos ampliem ou _distribuam_ uma transação em duas ou mais instâncias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A transação distribuída funciona mesmo quando as duas instâncias estão hospedadas em computadores separados.

O MSDTC está instalado no local do Microsoft SQL Server, mas não está disponível para o serviço de nuvem Azure SQL Database da Microsoft.

O MSDTC é chamado pelo Driver Cliente Nativo do Servidor SQL para Conectividade de Banco de Dados Aberto (ODBC), quando seu programa C++ gerencia uma transação distribuída. O driver Nativo Cliente ODBC possui um gerenciador de transações compatível com o padrão DTP (Open Group Distributed Transaction Processing, processamento de transações distribuídas de grupo aberto). Essa conformidade é exigida pelo MSDTC. Normalmente, todos os comandos de gerenciamento de transações são enviados através deste driver ODBC cliente nativo. Esta é a sequência:

1. O aplicativo C++ Native Client ODBC inicia uma transação chamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), com o modo de confirmação automática desligado.

2. O aplicativo atualiza alguns dados no SQL Server X no computador A.

3. O aplicativo atualiza alguns dados no SQL Server Y no computador B.
    - Se uma atualização no SQL Server Y falhar, todas as atualizações não comprometidas em ambas as instâncias do SQL Server serão revertidas.

4. Finalmente, o aplicativo encerra a transação ligando para [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), com a opção SQL_COMMIT ou SQL_ROLLBACK.

_(1)_ O MSDTC pode ser invocado sem o ODBC. Nesse caso, o MSDTC torna-se o gerenciador de transações, e o aplicativo não usa mais **o SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Apenas uma transação distribuída

Suponha que seu aplicativo C++ Cliente Nativo ODBC seja alistado em uma transação distribuída. Em seguida, o aplicativo se alista em uma segunda transação distribuída. Neste caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o driver ODBC do Cliente Nativo deixa a transação distribuída original e se alista na nova transação distribuída.

Para obter mais informações, consulte [A Referência do Programador DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C# alternativa para Banco de Dados SQL na nuvem

O MSDTC não é suportado nem para o Azure SQL Database ou para o Azure SQL Data Warehouse.

No entanto, uma transação distribuída pode ser criada para o Banco de Dados SQL fazendo com que seu programa C# use o Sistema de classe [.NET.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Outras linguagens de programação

As seguintes outras linguagens de programação podem não fornecer qualquer suporte para transações distribuídas com o serviço SQL Database:

- C++ nativo que usam drivers ODBC
- Servidor vinculado usando Transact-SQL
- Drivers JDBC

## <a name="see-also"></a>Confira também

[Executando transações (ODBC)](performing-transactions-in-odbc.md)
