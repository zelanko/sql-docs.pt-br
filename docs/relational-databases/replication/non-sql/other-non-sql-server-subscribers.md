---
title: "Outros assinantes n&#227;o SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Assinantes não SQL Server, outros tipos"
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Outros assinantes n&#227;o SQL Server
  Para obter uma lista de não -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suporte para os assinantes por [!INCLUDE[msCoName](../../../includes/msconame-md.md)], consulte [assinantes não-SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Esse tópico inclui informações sobre exigências para drivers ODBC e provedores OLE DB.  
  
## Exigências do driver ODBC  
 O driver ODBC:  
  
-   Deve ser compatível com nível 1 do ODBC.  
  
-   Deve ser um ambiente de distribuidor thread-safe.  
  
-   Deve ser capaz em termos de transação.  
  
-   Deve oferecer suporte para linguagem de definição de dados (DLL).  
  
-   Não pode ser somente leitura.  
  
-   Deve oferecer suporte a nomes de tabela longos como **MSreplication_subscriptions**.  
  
## Replicação com o uso de interfaces OLE DB  
 Provedores OLE DB devem oferecer suporte a esses objetos para replicação transacional:  
  
-   **Fonte de dados** objeto  
  
-   **Sessão** objeto  
  
-   **Comando** objeto  
  
-   **Conjunto de linhas** objeto  
  
-   **Erro** objeto  
  
### Interfaces de objeto DataSource   
 As interfaces a seguir são exigidas para a conexão com uma fonte de dados:  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 Se o provedor oferece suporte a **IDBInfo** interface, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a interface para recuperar informações como o caractere identificador entre aspas, o tamanho máximo da instrução SQL e o número máximo de caracteres nos nomes de tabela e coluna.  
  
### Interfaces de objeto de sessão  
 As seguintes interfaces são exigidas:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### Interfaces de objeto de comando  
 As seguintes interfaces são exigidas:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** é necessário criar acessadores de parâmetro. Se o provedor oferece suporte a **IColumnRowset**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa essa interface para determinar se uma coluna é uma coluna de identidade.  
  
### Interfaces de objeto de conjunto de linhas  
 As seguintes interfaces são exigidas:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 Um aplicativo deve abrir um conjunto de linhas em uma tabela replicada que é criada no banco de dados de assinatura. **IColumnsInfo** e **IAccessor** são necessários para acessar dados no conjunto de linhas.  
  
### Interfaces de objeto de erro  
 Use as seguintes interfaces para gerenciar erros:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Use **ISQLErrorInfo** se ele for suportado pelo provedor OLE DB.  
  
 Para obter mais informações sobre o provedor OLE DB, consulte a documentação fornecida com seu provedor OLE DB.  
  
## Consulte também  
 [Assinantes não SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  