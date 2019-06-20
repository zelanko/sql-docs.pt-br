---
title: Outros Assinantes não SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 135d317d74a720d51c966ed92f1c305f8c04b838
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63021946"
---
# <a name="other-non-sql-server-subscribers"></a>Outros assinantes não SQL Server
  Para uma lista de Assinantes não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , suportados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [Non-SQL Server Subscribers](non-sql-server-subscribers.md). Esse tópico inclui informações sobre exigências para drivers ODBC e provedores OLE DB.  
  
## <a name="odbc-driver-requirements"></a>Exigências do driver ODBC  
 O driver ODBC:  
  
-   Deve ser compatível com nível 1 do ODBC.  
  
-   Deve ser isento de threads e para a arquitetura do processador (Intel ou Alpha) e plataforma (32 bit ou 64 bit) na qual o Distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executado.  
  
-   Deve ser capaz em termos de transação.  
  
-   Deve oferecer suporte para linguagem de definição de dados (DLL).  
  
-   Não pode ser somente leitura.  
  
-   Deve oferecer suporte para nomes de tabela longos como **MSreplication_subscriptions**.  
  
## <a name="replicating-using-ole-db-interfaces"></a>Replicação com o uso de interfaces OLE DB  
 Provedores OLE DB devem oferecer suporte a esses objetos para replicação transacional:  
  
-   Objeto**DataSource**   
  
-   Objeto**Sessão**   
  
-   Objeto**Comando**   
  
-   Objeto**Conjunto de linhas**   
  
-   Objeto**Erro**   
  
### <a name="datasource-object-interfaces"></a>Interfaces de objeto DataSource  
 As interfaces a seguir são exigidas para a conexão com uma fonte de dados:  
  
-   `IDBInitialize`  
  
-   `IDBCreateSession`  
  
-   `IDBProperties`  
  
 Se o provedor oferece suporte para a interface **IDBInfo** , [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a interface para recuperar informações tais como o caractere identificador entre aspas, comprimento máximo da instrução SQL e número máximo de caracteres em nomes de tabelas e colunas.  
  
### <a name="session-object-interfaces"></a>Interfaces de objeto de sessão  
 As seguintes interfaces são exigidas:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Interfaces de objeto de comando  
 As seguintes interfaces são exigidas:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** é necessário criar acessadores de parâmetro. Se o provedor oferece suporte para **IColumnRowset**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa aquela interface para determinar se uma coluna é uma coluna de identidade.  
  
### <a name="rowset-object-interfaces"></a>Interfaces de objeto de conjunto de linhas  
 As seguintes interfaces são exigidas:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 Um aplicativo deve abrir um conjunto de linhas em uma tabela replicada que é criada no banco de dados de assinatura. **IColumnsInfo** e **IAccessor** são necessários para acessar dados no conjunto de linhas.  
  
### <a name="error-object-interfaces"></a>Interfaces de objeto de erro  
 Use as seguintes interfaces para gerenciar erros:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Use **ISQLErrorInfo** se for suportado pelo provedor OLE DB.  
  
 Para obter mais informações sobre o provedor OLE DB, consulte a documentação fornecida com seu provedor OLE DB.  
  
## <a name="see-also"></a>Consulte também  
 [Non-SQL Server Subscribers](non-sql-server-subscribers.md)  
  
  
