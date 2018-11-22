---
title: Configurar um grupo de disponibilidade para transações distribuídas | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53c1a7c5ce6c7d529fb07f356d87e0adc5c02e31
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639114"
---
# <a name="configure-availability-group-for-distributed-transactions"></a>Configurar um grupo de disponibilidade para transações distribuídas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)] dá suporte a todas as transações distribuídas, incluindo bancos de dados em um grupo de disponibilidade. Este artigo explica como configurar um grupo de disponibilidade para transações distribuídas  

Para garantir as transações distribuídas, o grupo de disponibilidade deve ser configurado para registrar bancos de dados como gerenciadores de recursos de transação distribuída.  

>[!NOTE]
>O [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)] Service Pack 2 e posteriores dão suporte completo para transações distribuídas em grupos de disponibilidade. Nas versões do [!INCLUDE[SQL2016]](../../../includes/sssql15-md.md)] anteriores ao Service Pack 2, não há suporte para as transações distribuídas entre bancos de dados (ou seja, transação usando bancos de dados na mesma instância do SQL Server) que envolvem um banco de dados em um grupo de disponibilidade. O [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)] não tem essa limitação. 
>
>No [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)], as etapas de configuração são as mesmas do [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)].

Em uma transação distribuída, aplicativos cliente funcionam com o MS DTC (Coordenador de Transações Distribuídas da Microsoft) ou DTC para garantir a consistência transacional entre várias fontes de dados. O DTC é um serviço disponível em sistemas operacionais com suporte baseados no Windows Server. Para uma transação distribuída, o DTC é o *coordenador de transações*. Normalmente, uma instância do SQL Server é o *gerenciador de recursos*. Quando um banco de dados está em um grupo de disponibilidade, cada banco de dados precisa ser seu próprio gerenciador de recursos. 

O [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] não impede transações distribuídas para bancos de dados em um grupo de disponibilidade – mesmo quando o grupo de disponibilidade não está configurado para transações distribuídas. No entanto, quando um grupo de disponibilidade não está configurado para transações distribuídas, o failover pode não ser bem-sucedido em algumas situações. Especificamente, a instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] da nova réplica primária pode não conseguir obter o resultado da transação do DTC. Para permitir que a instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] obtenha o resultado de transações incertas do DTC após o failover, configure o grupo de disponibilidade para transações distribuídas. 

## <a name="prerequisites"></a>Prerequisites

Antes de configurar um grupo de disponibilidade para dar suporte a transações distribuídas, você deve atender aos seguintes pré-requisitos:

* Todas as instâncias do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] que fazem parte da transação distribuída devem ser o [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)] ou posterior.

* Os grupos de disponibilidade devem estar em execuçaõ no Windows Server 2016 ou Windows Server 2012 R2. Para o Windows Server 2012 R2, é necessário instalar a atualização na KB3090973 disponível em [https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973).  

## <a name="create-an-availability-group-for-distributed-transactions"></a>Criar um grupo de disponibilidade para transações distribuídas

Configure um grupo de disponibilidade para dar suporte a transações distribuídas. Defina o grupo de disponibilidade para permitir que cada banco de dados se registre como um gerenciador de recursos. Este artigo explica como configurar um grupo de disponibilidade, de modo que cada banco de dados possa ser um gerenciador de recursos no DTC.

É possível criar um grupo de disponibilidade para transações distribuídas no [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)] ou posterior. Para criar um grupo de disponibilidade para transações distribuídas, inclua `DTC_SUPPORT = PER_DB` na definição do grupo de disponibilidade. O script a seguir cria um grupo de disponibilidade para transações distribuídas. 

```sql
CREATE AVAILABILITY GROUP MyAG
   WITH (
      DTC_SUPPORT = PER_DB  
      )
   FOR DATABASE DB1, DB2
   REPLICA ON
      Server1 WITH (
         ENDPOINT_URL = 'TCP://SERVER1.corp.com:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         )
      Server2 WITH (
         ENDPOINT_URL = 'TCP://SERVER2.corp.com:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC  
         )
```

>[!NOTE]
>O script anterior é um exemplo simples de um grupo de disponibilidade e não foi projetado para nenhum ambiente de produção específico. 

## <a name="alter-an-availability-group-for-distributed-transactions"></a>Alterar um grupo de disponibilidade para transações distribuídas

É possível alterar um grupo de disponibilidade para transações distribuídas no [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)] ou posterior. Para alterar um grupo de disponibilidade para transações distribuídas, inclua `DTC_SUPPORT = PER_DB` no script de `ALTER AVAILABILITY GROUP`. O script de exemplo altera o grupo de disponibilidade para que ele dê suporte a transações distribuídas. 

```sql
ALTER AVAILABILITY GROUP MyaAG
   SET (
      DTC_SUPPORT = PER_DB  
      );
```

>[!NOTE]
>No [!INCLUDE[SQL2016](../../../includes/sssql15-md.md)], não é possível alterar um grupo de disponibilidade para transações distribuídas. Para alterar a remoção de configuração e recriar o grupo de disponibilidade com a configuração `DTC_SUPPORT = PER_DB`. 

## <a name="a-namedisttrandistributed-transactions---technical-concepts"></a><a name="distTran"/>Transações distribuídas – conceitos técnicos

Uma transação distribuída abrange dois ou mais bancos de dados. Assim como o gerenciador de transação, o DTC coordena as transações entre as instâncias do SQL Server e outras fontes de dados. Cada instância do mecanismo de banco de dados do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] pode funcionar como um gerenciador de recursos. Quando um grupo de disponibilidade é configurado com `DTC_SUPPORT = PER_DB`, os bancos de dados podem funcionar como gerenciadores de recursos. Para obter mais informações, consulte a documentação do MS DTC.

Uma transação com dois ou mais bancos de dados em uma única instância do mecanismo de banco de dados é, de fato, uma transação distribuída. A instância gerencia a transação distribuída internamente. Para o usuário, ela opera como uma transação local. O [!INCLUDE[SQL2017](../../../includes/sssqlv14-md.md)] promove todas as transações entre bancos de dados para o DTC quando os bancos de dados estão em um grupo de disponibilidade configurado com `DTC_SUPPORT = PER_DB` – mesmo em uma única instância do SQL Server. 

No aplicativo, uma transação distribuída é gerenciada da mesma forma como uma transação local. No final da transação, o aplicativo solicita que a transação seja confirmada ou revertida. Uma confirmação distribuída deve ser gerenciada de forma diferenciada pelo gerenciador de transações para minimizar o risco de que uma falha de rede possa resultar em alguns gerenciadores de recurso que confirmam com êxito enquanto outros revertem a transação. Isso é obtido pelo gerenciamento do processo de confirmação em duas fases (a fase de preparação e a fase de confirmação), o que é conhecido como protocolo 2PC.

- **Fase de preparação**
   
   Quando o gerenciador de transações recebe uma solicitação de confirmação, ele envia um comando de preparação a todos os gerenciadores de recursos envolvidos na transação. Cada gerenciador executa todas as ações necessárias para tornar a transação durável, e todos os buffers que mantêm imagens de log da transação são liberados no disco. À medida que cada gerenciador de recursos conclui a fase de preparação, ele retorna informações de êxito ou de falha ao gerenciador de transações.

- **Fase de confirmação**
   
   Se o gerenciador de transações receber preparos bem-sucedidos de todos os gerenciadores de recursos, ele enviará comandos de confirmação a cada gerenciador de recursos. Em seguida, os gerenciadores de recursos podem concluir a confirmação. Se todos os gerenciadores de recursos relatarem uma confirmação bem-sucedida, o gerenciador de transações enviará uma notificação de êxito ao aplicativo. Se um gerenciador de recursos informar uma falha na preparação, o gerenciador de transações enviará um comando de reversão a cada gerenciador de recursos e indicará a falha da confirmação ao aplicativo.

### <a name="detailed-steps"></a>Etapas detalhadas

A lista a seguir explica como o aplicativo funciona com o DTC para concluir as transações distribuídas.

1. A instância do SQL Server se inscreve na transação do DTC. Isso pode ocorrer quando há mais de um gerenciador de recursos na transação ou se o cliente solicita que uma transação seja promovida como uma transação do DTC.
2. O cliente realiza algumas tarefas na instância do SQL Server na transação do DTC.
3. O cliente emite uma confirmação ou anulação da transação do DTC.
    - Se o cliente emitir uma anulação, a transação será anulada imediatamente.
    - Se o cliente emitir uma confirmação, o DTC iniciará o protocolo de confirmação de duas fases solicitando que todos os gerenciadores de recursos na transação se preparem para a transação.
4. O DTC informa todos os gerenciadores de recursos para confirmar a transação depois que todos os gerenciadores de recursos reconhecerem a fase de preparação com êxito. Se algo impedir a confirmação bem-sucedida, o DTC anulará a transação. 

### <a name="effects-of-configuring-an-availability-group-for-distributed-transactions"></a>Efeitos da configuração de um grupo de disponibilidade para transações distribuídas

Cada entidade que faz parte de uma transação distribuída é chamada de gerenciador de recursos. Exemplos de gerenciadores de recursos incluem:

* Uma instância [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)]. 
* Um banco de dados em um grupo de disponibilidade que foi configurado para transações distribuídas.
* Serviço DTC – também pode ser um gerenciador de transação.
* Outras fontes de dados. 

Para fazer parte de transações distribuídas, uma instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] se inscreve com um DTC. Normalmente, a instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] se inscreve com o DTC no servidor local. Cada instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] cria um gerenciador de recursos com um RMID (identificador de gerenciador de recursos) exclusivo e registra-o no DTC. Na configuração padrão, todos os bancos de dados de uma instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] usam o mesmo RMID. 

Quando um banco de dados está em um grupo de disponibilidade, a cópia de leitura/gravação do banco de dados – ou da réplica primária – pode ser movida para outra instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)]. Para dar suporte a transações distribuídas durante essa movimentação, cada banco de dados deve agir como um gerenciador de recursos separado e ter um RMID exclusivo. Quando um grupo de disponibilidade tem `DTC_SUPPORT = PER_DB`, o [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] cria um gerenciador de recursos para cada banco de dados e registra-o no DTC usando um RMID exclusivo. Nessa configuração, o banco de dados é um gerenciador de recursos das transações do DTC.

Para obter mais detalhes sobre transações distribuídas no [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)], consulte [Transações distribuídas](#distTran)

## <a name="manage-unresolved-transactions"></a>Gerenciar transações não resolvidas

O resultado das transações ativas que existem durante a alteração do RMID não pode ser recuperado após um failover. Isso ocorre porque o RMID que o SQL Server usou para inscrição e o RMID que o SQL Server usou para recuperação são diferentes. A alteração do RMID pode ocorrer nos seguintes casos:

* Altere `DTC_SUPPORT` para um grupo de disponibilidade. 
* Adicione ou remova um banco de dados de um grupo de disponibilidade. 
* Remova um grupo de disponibilidade.

Nos casos anteriores, se a réplica primária fizer failover para uma nova instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)], a instância tentará contatar o DTC para identificar o resultado da transação. O DTC não pode retornar o resultado porque o RMID usado pelo banco de dados para obter o resultado de transações incertas durante a recuperação não foi inscrito antes. Portanto, o banco de dados entra no estado SUSPECT.

O novo log de erros do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] tem uma entrada semelhante ao seguinte exemplo:

```
Microsoft Distributed Transaction Coordinator (MS DTC) 
failed to reenlist citing that the database RMID does 
not match the RMID [xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx] 
associated with the transaction.  Please manually resolve
the transaction.
    
SQL Server detected a DTC/KTM in-doubt transaction with UOW 
{yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy}.Please resolve it 
following the guideline for Troubleshooting DTC Transactions.
```

O exemplo anterior mostra que o DTC não pôde inscrever novamente o banco de dados da nova réplica primária na transação criada após o failover. A instância do [!INCLUDE[SQLServer](../../../includes/ssnoversion-md.md)] não pode determinar o resultado da transação distribuída e, portanto, marca o banco de dados como suspeito. A transação é marcada como uma UOW (unidade de trabalho) e referenciada por um GUID. Para recuperar o banco de dados, confirme ou reverta a transação manualmente. 

>[!WARNING]
>Ao confirmar ou reverter uma transação manualmente, isso poderá afetar um aplicativo. Verifique se a ação de confirmação ou reversão é consistente com seus requisitos de aplicativo. 

Execute apenas um dos seguintes scripts:

   * Para confirmar a transação, atualize e execute o seguinte script – substitua `yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy` pela UOW da transação incerta da mensagem de erro anterior e execute:

   ```sql
   KILL 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy' WITH COMMIT
   ```

   * Para reverter a transação, atualize e execute o seguinte script – substitua `yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy` pela UOW da transação incerta da mensagem de erro anterior e execute:

   ```sql
   KILL 'yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy' WITH ROLLBACK
   ```

Depois de confirmar ou reverter a transação, use `ALTER DATABASE` para definir o banco de dados online. Atualize e execute o seguinte script – defina o nome do banco de dados com o nome do banco de dados suspeito:

   ```sql
   ALTER DATABASE [DB1] SET ONLINE
   ```

Para obter mais informações sobre como resolver transações incertas, consulte [Resolver transações manualmente](https://technet.microsoft.com/library/cc754134.aspx).

## <a name="next-steps"></a>Next Steps  

[Transações distribuídas](https://docs.microsoft.com/dotnet/framework/data/adonet/distributed-transactions)

[Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
[Transações – grupos de disponibilidade Always On e Espelhamento de Banco de Dados](transactions-always-on-availability-and-database-mirroring.md)  

[Dando suporte a transações XA](https://technet.microsoft.com/library/cc753563(v=ws.10).aspx)

[Como funciona: Sessão/SPID (–2) para transações do DTC](https://blogs.msdn.microsoft.com/bobsql/2016/08/04/how-it-works-sessionspid-2-for-dtc-transactions/)
