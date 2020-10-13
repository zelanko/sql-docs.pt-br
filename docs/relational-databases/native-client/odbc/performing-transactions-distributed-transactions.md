---
title: Criar transações distribuídas | Microsoft Docs
description: Os aplicativos podem usar o MSDTC para estender ou distribuir uma transação em várias instâncias do SQL Server. Uma classe .NET também pode distribuir uma transação.
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
ms.openlocfilehash: e5ace381694dcc3afdbed36e35e48af147067b32
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005964"
---
# <a name="create-a-distributed-transaction"></a>Criar uma transação distribuída

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


Uma transação distribuída pode ser criada para diferentes sistemas Microsoft SQL de diferentes maneiras.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>O driver ODBC chama o MSDTC para SQL Server local

O Microsoft Coordenador de Transações Distribuídas (MSDTC) permite que os aplicativos estendam ou _distribuam_ uma transação entre duas ou mais instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A transação distribuída funciona mesmo quando as duas instâncias são hospedadas em computadores separados.

O MSDTC é instalado para Microsoft SQL Server local, mas não está disponível para o serviço de nuvem do banco de dados SQL do Microsoft Azure.

O MSDTC é chamado pelo driver de SQL Server Native Client para ODBC (Open Database Connectivity), quando o programa C++ gerencia uma transação distribuída. O driver ODBC do Native Client tem um Gerenciador de transações que é compatível com o padrão XA do DTP (processamento de transações distribuídas) do grupo aberto. Essa conformidade é exigida pelo MSDTC. Normalmente, todos os comandos de gerenciamento de transações são enviados por meio desse driver ODBC do Native Client. Esta é a sequência:

1. Seu aplicativo ODBC do C++ nativo Client inicia uma transação chamando [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), com o modo de confirmação automática desativado.

2. O aplicativo atualiza alguns dados no SQL Server X no computador A.

3. O aplicativo atualiza alguns dados no SQL Server Y no computador B.
    - Se uma atualização em SQL Server Y falhar, todas as atualizações não confirmadas em ambas as instâncias de SQL Server serão revertidas.

4. Por fim, o aplicativo encerra a transação chamando [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), com a opção SQL_COMMIT ou SQL_ROLLBACK.

_(1)_ o MSDTC pode ser invocado sem ODBC. Nesse caso, o MSDTC torna-se o Gerenciador de transações e o aplicativo não usa mais **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Apenas uma transação distribuída

Suponha que seu aplicativo ODBC nativo do cliente do C++ seja inscrito em uma transação distribuída. Em seguida, o aplicativo se lista em uma segunda transação distribuída. Nesse caso, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client deixa a transação distribuída original e as inlistas na nova transação distribuída.

Para obter mais informações, consulte [referência do programador do DTC](/previous-versions/windows/desktop/ms686108(v=vs.85)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>Alternativa C# para banco de dados SQL na nuvem

O MSDTC não tem suporte para o banco de dados SQL do Azure nem para o Azure Synapse Analytics.

No entanto, uma transação distribuída pode ser criada para o banco de dados SQL fazendo com que seu programa C# use a classe do .NET [System. Transactions. TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Outras linguagens de programação

As outras linguagens de programação a seguir podem não fornecer nenhum suporte para transações distribuídas com o serviço do banco de dados SQL:

- C++ nativo que usa drivers ODBC
- Servidor vinculado usando Transact-SQL
- Drivers JDBC

## <a name="see-also"></a>Veja também

[Executando transações (ODBC)](performing-transactions-in-odbc.md)