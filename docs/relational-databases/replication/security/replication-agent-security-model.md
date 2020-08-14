---
title: Modelo de segurança do agente de replicação | Microsoft Docs
description: No SQL Server, o modelo de segurança do agente de replicação permite um controle refinado das contas nas quais os agentes de replicação executam e efetuam conexões.
ms.custom: ''
ms.date: 04/26/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 41d77ae1b9c0763fedf2e53610bb3a0be5cd185c
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823921"
---
# <a name="replication-agent-security-model"></a>Modelo de segurança do agente de replicação
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O modelo de segurança do agente de replicação permite um controle refinado das contas nas quais os agentes de replicação executam e efetuam conexões: Uma conta diferente pode ser especificada para cada agente. Para obter mais informações sobre como especificar contas, confira [Controle de acesso e identidade para replicação](../../../relational-databases/replication/security/identity-and-access-control-replication.md).  

O modelo de segurança do agente de replicação é um pouco diferente para a Instância Gerenciada de SQL do Azure, pois não há contas do Windows nas quais os agentes serão executados. Em vez disso, tudo deve ser feito por meio da autenticação do SQL Server. 
  
> [!IMPORTANT]  
>  Quando um membro da função fixa do servidor **sysadmin** configura a replicação, os agentes de replicação podem ser configurados para representar a conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Isso é realizado não especificando um logon nem uma senha para um agente de replicação, contudo, não recomendamos essa abordagem. Em vez disso, como a melhor prática de segurança, recomendamos especificar uma conta para cada agente que tenha as permissões mínimas descritas na seção "Permissões exigidas pelos agentes", mais adiante nesse tópico.  
  
 Os agentes de replicação, como todos os executáveis, são executados sob o contexto de uma conta do Windows. Os agentes fazem conexões de Segurança Integrada do Windows usando essa conta. A conta sob a qual o agente executa depende de como o agente é iniciado:  
  
-   Iniciando o agente de um trabalho do Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o padrão: quando um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é usado para iniciar um agente de replicação, o agente executa sob o contexto de uma conta que é especificada quando a replicação é configurada. Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e replicação, consulte a seção "Segurança do Agente sob SQL Server Agent", mais adiante nesse tópico. Para obter informações sobre as permissões necessárias para a conta na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é executado, consulte [Configurar o SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Iniciando o agente de uma linha de comando do MS-DOS, seja diretamente ou por meio de um script: O agente é executado no contexto da conta do usuário que está executando o agente na linha de comando.  
  
-   Iniciando o agente de um aplicativo que usa objetos RMO ( Replication Management Objects) ou um controle ActiveX: O agente é executado no contexto do aplicativo que está chamando o RMO ou o controle ActiveX.  
  
    > [!NOTE]  
    >  Os controles ActiveX são preteridos.  
  
 Recomendamos que as conexões sejam feitas sob o contexto da Segurança Integrada do Windows. Para compatibilidade com versões anteriores, a Segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode ser usada também. Para obter mais informações sobre as práticas recomendadas, consulte [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Permissões exigidas pelos agentes  
 As contas sob as quais os agentes executam e fazem conexões requerem uma variedade de permissões. Essas permissões estão descritas na tabela a seguir. Recomendamos que cada agente execute sob uma conta do Windows diferente, e que a conta deve receber somente as permissões necessárias. Para obter informações sobre a PAL (lista de acesso à publicação), que são relevantes para vários agentes, consulte [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
> [!NOTE]  
>  O UAC (User Account Control) em alguns sistemas operacionais Windows pode impedir o acesso administrativo ao compartilhamento de instantâneos. Portanto, você deve conceder permissões de compartilhamento de instantâneos explicitamente às contas do Windows usadas pelo Agente de Instantâneo, pelo Agente de Distribuição, e pelo Agente de Mesclagem. Faça isso, mesmo se as contas do Windows forem membros do grupo de Administradores. Para obter mais informações, consulte [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
|Agente|Permissões|  
|-----------|-----------------|  
|Snapshot Agent|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve:<br /><br /> \- Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> \- Ter permissões de leitura, gravação e modificação no compartilhamento de instantâneo.<br /><br /> <br /><br /> Observe que a conta usada para *conexão* com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.|  
|Agente de Leitor de Log|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve ser no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de distribuição.<br /><br /> A conta usada para conexão com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.<br /><br /> Ao selecionar as opções de **sync_type** , *replication support only*, *initialize with backup*, ou *initialize from lsn*, o Agente de Leitor de Log deve ser executado após a execução de **sp_addsubscription**, para que os scripts configurados sejam gravados no banco de dados de distribuição. O Agente de Leitor de Log deve ser executado sob uma conta que seja membro da função de servidor fixa **sysadmin** . Quando a opção **sync_type** estiver definida como *Automatic*, nenhuma ação especial do Agente de Leitor de Log será necessária.|  
|Agente de Distribuição para uma assinatura push|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve:<br /><br /> \- Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> \- Ser um membro da PAL.<br /><br /> \- Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> \- Ter permissões de leitura no diretório de instalação do provedor OLE DB para o Assinante, se a assinatura for um Assinante não SQL Server.<br /><br /> \- Ao replicar dados LOB, o agente de distribuição deve ter permissões de gravação na pasta **C:\Arquivos de Programas\Microsoft SQL Server\XX\COM** de replicação, em que XX representa a ID da instância.<br /><br /> <br /><br /> Observe que a conta usada para *conexão* com o Assinante deverá ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura, ou ter permissões equivalentes, se a assinatura for um Assinante não SQL Server.<br /><br /> Observe também que, ao usar `-subscriptionstreams >= 2` no agente de distribuição, você deve também conceder a permissão **View Server State** nos assinantes para detectar deadlocks.|  
|Distribution Agent para uma assinatura pull|A conta do Windows sob a qual o agente executa é usada quando ele se conecta com o Assinante. Essa conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura. A conta usada para conectar-se ao Distribuidor deve:<br /><br /> \- Ser um membro da PAL.<br /><br /> \- Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> \- Ao replicar dados LOB, o agente de distribuição deve ter permissões de gravação na pasta **C:\Arquivos de Programas\Microsoft SQL Server\XX\COM** de replicação, em que XX representa a ID da instância.<br /><br /> <br /><br /> Observe que, ao usar `-subscriptionstreams >= 2` no agente de distribuição, você deve também conceder a permissão **View Server State** nos assinantes para detectar deadlocks.|  
|Merge Agent para uma assinatura push|A conta do Windows sob a qual o agente executa é usada quando ele se conecta ao Publicador e o Distribuidor. Essa conta deve:<br /><br /> \- Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> \- Ser um membro da PAL.<br /><br /> – Ser um logon associado a um usuário com permissões de leitura/gravação no banco de dados de publicação.<br /><br /> \- Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> <br /><br /> Observe que a conta usada para *conexão* ao Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** ,no banco de dados de assinatura.|  
|Merge Agent para uma assinatura pull|A conta do Windows sob a qual o agente executa é usada quando ele se conecta com o Assinante. Essa conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura. A conta usada para conectar-se ao Publicador e o Distribuidor deve:<br /><br /> \- Ser um membro da PAL.<br /><br /> – Ser um logon associado a um usuário com permissões de leitura/gravação no banco de dados de publicação.<br /><br /> \- Ser um logon associado a um usuário no banco de dados de distribuição. O usuário pode ser o usuário **Guest** .<br /><br /> \- Ter permissões de leitura no compartilhamento de instantâneos.|  
|Queue Reader Agent|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve ser no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de distribuição.<br /><br /> A conta usada para conexão com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.<br /><br /> A conta usada para se conectar ao Assinante deve ser no mínimo um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura.|  
  
## <a name="agent-security-under-sql-server-agent"></a>Segurança do agente sob o SQL Server Agent  
 Ao configurar a replicação usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], procedimentos [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO, um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é criado, por padrão, para cada agente. Os agentes executam sob o contexto de uma etapa de trabalho, independentemente de a execução ser contínua, por agendamento ou sob demanda. Esses trabalhos podem ser visualizados na pasta **Trabalhos** , no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. A tabela a seguir lista o nome dos trabalhos.  
  
|Agente|Nome do trabalho|  
|-----------|--------------|  
|Snapshot Agent|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<integer>**|  
|Snapshot Agent para uma partição de publicação de mesclagem|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|  
|Agente de Leitor de Log|**\<Publisher>-\<PublicationDatabase>-\<integer>**|  
|Merge Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<integer>**|  
|Merge Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Distribution Agent para assinaturas push|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Distribution Agent para assinaturas pull|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<SubscriptionDatabase>-\<GUID>**|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\<Publisher>-\<PublicationDatabase>-\<Publication>-\<Subscriber>-\<integer>**|  
|Queue Reader Agent|**[\<Distributor>].\<integer>**|  
  
 \*Para assinaturas push em publicações Oracle, o nome do trabalho é **\<Publisher>-\<Publisher**> em vez de **\<Publisher>-\<PublicationDatabase>** .  
  
 \*\*Para assinaturas pull em publicações Oracle, o nome do trabalho é **\<Publisher>-\<DistributionDatabase**> em vez de **\<Publisher>-\<PublicationDatabase>** .  
  
 Ao configurar a replicação, você especifica as contas sob as quais os agentes devem executar. Porém, todas as etapas do trabalho executam sob o contexto de segurança de um *proxy*; portanto, a replicação realiza internamente os seguintes mapeamentos para as contas de agentes que você especificar:  
  
-   A conta é mapeada primeiro para uma credencial usando a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](../../../t-sql/statements/create-credential-transact-sql.md). Os proxies do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent usam credenciais para armazenar informações sobre as contas de usuário do Windows.  
  
-   O procedimento armazenado [sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) é chamado e a credencial é usada para criar um proxy.  
  
> [!NOTE]  
>  Essas informações são fornecidas para auxiliar a entender o que está envolvido na execução de agentes com o contexto de segurança adequado. Você não deve interagir diretamente com as credenciais ou com os proxies que foram criados.  
  
## <a name="see-also"></a>Consulte Também  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Exibir e modificar configurações de segurança de replicação](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Proteger a pasta de instantâneos](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
