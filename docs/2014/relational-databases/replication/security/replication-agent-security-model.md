---
title: Modelo de segurança do agente de replicação | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 4b919289d49901f64b26db0aa2d4b71eeb0e132a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62960808"
---
# <a name="replication-agent-security-model"></a>Modelo de segurança do agente de replicação
  O modelo de segurança do agente de replicação proporciona um controle refinado nas contas sob as quais os agentes de replicação executam e fazem conexões: uma conta diferente pode ser especificada para cada agente. Para obter mais informações sobre como especificar contas, consulte [Gerenciar logons e senhas na replicação](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
> [!IMPORTANT]  
>  Quando um membro da função fixa do servidor **sysadmin** configura a replicação, os agentes de replicação podem ser configurados para representar a conta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent Isso é realizado não especificando um logon nem uma senha para um agente de replicação, contudo, não recomendamos essa abordagem. Em vez disso, como a melhor prática de segurança, recomendamos especificar uma conta para cada agente que tenha as permissões mínimas descritas na seção "Permissões exigidas pelos agentes", mais adiante nesse tópico.  
  
 Os agentes de replicação, como todos os executáveis, são executados sob o contexto de uma conta do Windows. Os agentes fazem conexões de Segurança Integrada do Windows usando essa conta. A conta sob a qual o agente executa depende de como o agente é iniciado:  
  
-   Iniciando o agente de um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, o padrão: quando um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é usado para iniciar um agente de replicação, o agente executa sob o contexto de uma conta que é especificada quando a replicação é configurada. Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent e replicação, consulte a seção "Segurança do Agente sob SQL Server Agent", mais adiante nesse tópico. Para obter informações sobre as permissões necessárias para a conta na qual o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é executado, consulte [Configurar o SQL Server Agent](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Iniciando o agente de uma linha de comando MS-DOS, diretamente ou através de um script: o agente executa sob o contexto da conta do usuário que estiver executando o agente na linha de comando.  
  
-   Iniciando o agente de um aplicativo que usa o RMO (Replication Management Objects) ou um controle ActiveX: o agente executa sob o contexto do aplicativo que estiver chamando o RMO ou o controle ActiveX.  
  
    > [!NOTE]  
    >  Os controles ActiveX são preteridos.  
  
 Recomendamos que as conexões sejam feitas sob o contexto da Segurança Integrada do Windows. Para compatibilidade com versões anteriores, a Segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode ser usada também. Para obter mais informações sobre as práticas recomendadas, consulte [Replication Security Best Practices](replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Permissões exigidas pelos agentes  
 As contas sob as quais os agentes executam e fazem conexões requerem uma variedade de permissões. Essas permissões estão descritas na tabela a seguir. Recomendamos que cada agente execute sob uma conta do Windows diferente, e que a conta deve receber somente as permissões necessárias. Para obter informações sobre a PAL (lista de acesso à publicação), que são relevantes para vários agentes, consulte [Proteger o Publicador](secure-the-publisher.md).  
  
> [!NOTE]  
>  O UAC (User Account Control) em alguns sistemas operacionais Windows pode impedir o acesso administrativo ao compartilhamento de instantâneos. Portanto, você deve conceder permissões de compartilhamento de instantâneos explicitamente às contas do Windows usadas pelo Agente de Instantâneo, pelo Agente de Distribuição, e pelo Agente de Mesclagem. Faça isso, mesmo se as contas do Windows forem membros do grupo de Administradores. Para obter mais informações, consulte [proteger a pasta de instantâneo](secure-the-snapshot-folder.md).  
  
|Agente|Permissões|  
|-----------|-----------------|  
|Snapshot Agent|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve:<br /><br /> -No mínimo, seja um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> - Ter permissões de leitura, gravação e modificação no compartilhamento de instantâneo.<br /><br /> <br /><br /> A conta usada para conexão com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.|  
|Agente de Leitor de Log|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve ser no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de distribuição.<br /><br /> A conta usada para conexão com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.<br /><br /> Ao selecionar as `sync_type` opções *somente suporte de replicação*, *inicializar com backup*ou *inicializar do LSN*, o agente de leitor de log deve ser `sp_addsubscription`executado após a execução, para que os scripts de configuração sejam gravados no banco de dados de distribuição. O Agente de Leitor de Log deve ser executado sob uma conta que seja membro da função de servidor fixa **sysadmin** . Quando a `sync_type` opção é definida como *automática*, nenhuma ação especial do agente de leitor de log é necessária.|  
|Agente de Distribuição para uma assinatura push|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve:<br /><br /> - Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> - Ser um membro da PAL.<br /><br /> - Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> - Ter permissões de leitura no diretório de instalação do provedor OLE DB para o Assinante, se a assinatura for um Assinante não SQL Server.<br /><br /> - Ao replicar dados LOB, o agente de distribuição deve ter permissões de gravação na pasta **C:\Arquivos de Programas\Microsoft SQL Server\XX\COM** de replicação, em que XX representa a ID da instância.<br /><br /> <br /><br /> A conta usada para conectar-se com o Assinante deverá ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura, ou ter permissões equivalentes, se a assinatura for um Assinante não SQL Server.<br /><br /> Observação: ao usar `-subscriptionstreams >= 2` o no agente de distribuição, você também deve `View Server State` conceder a permissão nos assinantes para detectar deadlocks.|  
|Distribution Agent para uma assinatura pull|A conta do Windows sob a qual o agente executa é usada quando ele se conecta com o Assinante. Essa conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura. A conta usada para conectar-se ao Distribuidor deve:<br /><br /> - Ser um membro da PAL.<br /><br /> - Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> - Ao replicar dados LOB, o agente de distribuição deve ter permissões de gravação na pasta **C:\Arquivos de Programas\Microsoft SQL Server\XX\COM** de replicação, em que XX representa a ID da instância.<br /><br /> <br /><br /> Observação: ao usar `-subscriptionstreams >= 2` o no agente de distribuição, você também deve `View Server State` conceder a permissão nos assinantes para detectar deadlocks.|  
|Merge Agent para uma assinatura push|A conta do Windows sob a qual o agente executa é usada quando ele se conecta ao Publicador e o Distribuidor. Essa conta deve:<br /><br /> - Ser, no mínimo, um membro da função de banco de dados fixa **db_owner** no banco de dados de distribuição.<br /><br /> - Ser um membro da PAL.<br /><br /> - Ser um logon associado a um usuário no banco de dados de publicação.<br /><br /> - Ter permissões de leitura no compartilhamento de instantâneos.<br /><br /> <br /><br /> A conta usada para conectar-se ao Assinante deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** ,no banco de dados de assinatura.|  
|Merge Agent para uma assinatura pull|A conta do Windows sob a qual o agente executa é usada quando ele se conecta com o Assinante. Essa conta deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura. A conta usada para conectar-se ao Publicador e o Distribuidor deve:<br /><br /> - Ser um membro da PAL.<br /><br /> - Ser um logon associado a um usuário no banco de dados de publicação.<br /><br /> - Ser um logon associado a um usuário no banco de dados de distribuição. O usuário pode ser o usuário `Guest`.<br /><br /> - Ter permissões de leitura no compartilhamento de instantâneos.|  
|Queue Reader Agent|A conta do Windows sob a qual o agente executa é usada quando fizer conexões ao Distribuidor. Essa conta deve ser no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de distribuição.<br /><br /> A conta usada para conexão com o Publicador deve ser, no mínimo, um membro da função de banco de dados fixa **db_owner** , no banco de dados de publicação.<br /><br /> A conta usada para se conectar ao Assinante deve ser no mínimo um membro da função de banco de dados fixa **db_owner** , no banco de dados de assinatura.|  
  
## <a name="agent-security-under-sql-server-agent"></a>Segurança do agente sob o SQL Server Agent  
 Ao configurar a replicação usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], procedimentos [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou RMO, um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent é criado, por padrão, para cada agente. Os agentes executam sob o contexto de uma etapa de trabalho, independentemente de a execução ser contínua, por agendamento ou sob demanda. Esses trabalhos podem ser visualizados na pasta **Trabalhos** , no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. A tabela a seguir lista o nome dos trabalhos.  
  
|Agente|Nome do trabalho|  
|-----------|--------------|  
|Snapshot Agent|**\<Publicador>\<-PublicationDatabase>\<-publicação>\<-Integer>**|  
|Snapshot Agent para uma partição de publicação de mesclagem|**Dyn_\<Publisher>-\<PublicationDatabase>-\<Publication>-\<GUID>**|  
|Agente de Leitor de Log|**\<Publicador>\<-PublicationDatabase>\<-inteiro>**|  
|Merge Agent para assinaturas pull|**\<Publicador>\<-PublicationDatabase>\<-publicação>\<-Subscriber>\<-SubscriptionDatabase>\<-inteiro>**|  
|Merge Agent para assinaturas push|**\<Publicador>\<-PublicationDatabase>\<-publicação>\<-Subscriber>\<-inteiro>**|  
|Distribution Agent para assinaturas push|**\<\<\<Publicador>-PublicationDatabase>-publicação>-Subscriber>\<-inteiro>1 \<** <sup>1</sup>|  
|Distribution Agent para assinaturas pull|**\<\<\<\<Publicador>-PublicationDatabase>-publicação>-Subscriber>-SubscriptionDatabase>\<-GUID>2 \<** <sup>2</sup>|  
|Distribution Agent para assinaturas push para Assinantes não SQL Server|**\<Publicador>\<-PublicationDatabase>\<-publicação>\<-Subscriber>\<-inteiro>**|  
|Queue Reader Agent|**[\<> do distribuidor]. \<>inteiro**|  
  
 <sup>1</sup> para assinaturas push para publicações Oracle, o nome do trabalho é ** \<Publisher>-\<Publisher**> em vez de ** \<Publisher>-\<PublicationDatabase>**.  
  
 <sup>2</sup> para assinaturas pull para publicações Oracle, o nome do trabalho é ** \<Publisher>-\<DistributionDatabase**> em vez de ** \<Publisher>-\<PublicationDatabase>**.  
  
 Ao configurar a replicação, você especifica as contas sob as quais os agentes devem executar. Porém, todas as etapas do trabalho executam sob o contexto de segurança de um *proxy*; portanto, a replicação realiza internamente os seguintes mapeamentos para as contas de agentes que você especificar:  
  
-   A conta é mapeada primeiro para uma credencial usando a instrução [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql). Os proxies do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent usam credenciais para armazenar informações sobre as contas de usuário do Windows.  
  
-   O procedimento armazenado [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) é chamado e a credencial é usada para criar um proxy.  
  
> [!NOTE]  
>  Essas informações são fornecidas para auxiliar a entender o que está envolvido na execução de agentes com o contexto de segurança adequado. Você não deve interagir diretamente com as credenciais ou com os proxies que foram criados.  
  
## <a name="see-also"></a>Consulte Também  
 [Práticas recomendadas de segurança de replicação](replication-security-best-practices.md)   
 [Segurança de Replicação do SQL Server](view-and-modify-replication-security-settings.md)   
 [Proteger a pasta de instantâneos](secure-the-snapshot-folder.md)  
  
  
