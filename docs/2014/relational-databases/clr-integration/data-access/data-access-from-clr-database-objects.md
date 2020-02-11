---
title: Acesso a dados de objetos de banco de dados CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4561c7b8979a919ea144bab6d9b42f722b089e48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874076"
---
# <a name="data-access-from-clr-database-objects"></a>Acesso aos dados dos objetos de banco de dados CLR
  Uma rotina Common Language Runtime (CLR) pode acessar facilmente os dados armazenados na instância do [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] na qual ele é executado, bem como os dados armazenados em instâncias remotas. Os dados específicos que a rotina pode acessar são determinados pelo contexto de usuário no qual o código está sendo executado. Acesse dados de dentro de um objeto CLR Database usando o .NET Framework Provedor de Dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para dados de aplicativos de cliente gerenciado e de camada intermediária. Por causa disto, você pode aproveitar seu conhecimento do ADO.NET e do `SqlClient` em aplicativos cliente e de camada intermediária.  
  
> [!NOTE]  
>  Os métodos de tipos definidos pelo usuário e as funções definidas pelo usuário não são permitidos para executar o acesso a dados por padrão. Você deve definir a propriedade `DataAccess` de `SqlMethodAttribute` ou de `SqlFunctionAttribute` como `DataAccessKind.Read` para habilitar o acesso a dados somente leitura de métodos de UDT (Tipo Definido pelo Usuário) ou de funções definidas pelo usuário. As operações de modificação de dados não são permitidas de UDTs ou de funções definidas pelo usuário e lançam exceções em tempo de execução, se houver alguma tentativa.  
  
 Esta seção aborda apenas as diferenças funcionais e comportamentais específicas ao acessar dados de um objeto de banco de dados de CLR. Para obter mais informações sobre os recursos e a funcionalidade do ADO.NET, consulte a documentação do ADO.NET incluída no SDK do .NET Framework.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Conexão de contexto](context-connection.md)  
 Descreve a conexão de contexto com o SQL Server.  
  
 [Representação e credenciais para conexões](impersonation-and-credentials-for-connections.md)  
 Descreve as conexões de representação e as credenciais de conexão.  
  
 [Extensões específicas em processo do SQL Server para o ADO.NET](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 Aborda os processos `SqlPipe`, `SqlContext`, `SqlTriggerContext` e `SqlDataRecord` específicos em andamento.  
  
 [Integração CLR e transações](../../native-client-ole-db-transactions/transactions.md)  
 Descreve como a nova estrutura de transação fornecida no namespace System.Transactions se integra ao ADO.NET e a integração CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Serialização XML de objetos de banco de dados CLR](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 Explica como habilitar cenários de serialização XML de objetos de banco de dados de CLR dentro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
