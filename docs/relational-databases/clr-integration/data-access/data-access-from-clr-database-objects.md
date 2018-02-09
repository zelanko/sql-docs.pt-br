---
title: Acesso a dados de objetos de banco de dados CLR | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a1132744c7d58581c1d5d60b5fca1cbd5e9fc66
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="data-access-from-clr-database-objects"></a>Acesso aos dados dos objetos de banco de dados CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Uma rotina do common language runtime (CLR) pode acessar facilmente os dados armazenados na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no qual ele é executado, bem como os dados armazenados em instâncias remotas. Os dados específicos que a rotina pode acessar são determinados pelo contexto de usuário no qual o código está sendo executado. Acessar dados de um objeto de banco de dados CLR usando o .NET Framework Data Provider para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], também conhecidos como **SqlClient**. Este é o mesmo provedor usado por desenvolvedores que acessam dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de aplicativos cliente gerenciados e de camada intermediária. Por isso, você pode aproveitar seu conhecimento do ADO.NET e **SqlClient** em aplicativos cliente e de camada intermediária.  
  
> [!NOTE]  
>  Os métodos de tipos definidos pelo usuário e as funções definidas pelo usuário não são permitidos para executar o acesso a dados por padrão. Você deve definir o **DataAccess** propriedade **SqlMethodAttribute** ou **SqlFunctionAttribute** para **DataAccessKind. Read** para habilitar acesso a dados somente leitura de métodos de tipo definido pelo usuário (UDT) ou funções definidas pelo usuário. As operações de modificação de dados não são permitidas de UDTs ou de funções definidas pelo usuário e lançam exceções em tempo de execução, se houver alguma tentativa.  
  
 Esta seção aborda apenas as diferenças funcionais e comportamentais específicas ao acessar dados de um objeto de banco de dados de CLR. Para obter mais informações sobre os recursos e a funcionalidade do ADO.NET, consulte a documentação do ADO.NET incluída no SDK do .NET Framework.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Conexão de contexto](../../../relational-databases/clr-integration/data-access/context-connection.md)  
 Descreve a conexão de contexto com o SQL Server.  
  
 [Representação e credenciais para conexões](../../../relational-databases/clr-integration/data-access/impersonation-and-credentials-for-connections.md)  
 Descreve as conexões de representação e as credenciais de conexão.  
  
 [Extensões específicas em processo do SQL Server para o ADO.NET](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 Discute a específica no processo **SqlPipe**, **SqlContext**, **SqlTriggerContext**, e **SqlDataRecord** objetos.  
  
 [Integração CLR e transações](../../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
 Descreve como a nova estrutura de transação fornecida no namespace System.Transactions se integra ao ADO.NET e a integração CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Serialização de XML de objetos de banco de dados CLR](http://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344)  
 Explica como habilitar cenários de serialização XML de objetos de banco de dados de CLR dentro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
