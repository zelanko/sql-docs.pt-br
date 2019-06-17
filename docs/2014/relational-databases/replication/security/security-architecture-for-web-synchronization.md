---
title: Arquitetura de segurança para sincronização da Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Web synchronization, security architecture
ms.assetid: 74eee587-d5f5-4d1a-bbae-7f4e3f27e23b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc091885b01821aaf8d2d12b9a321c6949d1523c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62959742"
---
# <a name="security-architecture-for-web-synchronization"></a>Arquitetura de segurança para sincronização da Web
  O[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] habilita o controle refinado na configuração de segurança para sincronização da Web. Esse tópico fornece uma lista abrangente de todos os componentes que podem ser incluídos na configuração da sincronização da Web e as informações sobre as conexões que são efetuadas entre os componentes. [!INCLUDE[ssNoteWinAuthentication](../../../includes/ssnotewinauthentication-md.md)]  
  
 A ilustração a seguir mostra todas as possíveis conexões, embora algumas possam ser desnecessárias em uma topologia específica. Por exemplo, uma conexão para um servidor de FTP só será necessária se o instantâneo for entregue através de FTP.  
  
 ![Componentes e conexões na sincronização da Web](../media/websyncarchitecture.gif "Componentes e conexões na sincronização da Web")  
  
 As tabelas a seguir descrevem os componentes e as conexões ilustrados.  
  
## <a name="a-windows-user-under-which-the-merge-agent-runs"></a>A. Usuário do Windows sob o qual o Merge Agent é executado  
 Durante a sincronização, o Merge Agent (A) é iniciado no Assinante. O Merge Agent pode ser iniciado a partir de uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent ou de um aplicativo autônomo personalizado. Se o Merge Agent for iniciado de uma etapa de trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent, o Merge Agent executará sob o contexto de um usuário do Windows a ser especificado por você. Se não especificar um usuário do Windows, o Merge Agent executa sob o contexto da conta de serviços do Windows para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.  
  
|Tipo de conta|Onde a conta é especificada|  
|---------------------|------------------------------------|  
|Usuário do Windows|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: os parâmetros **@job_login** e **@job_password** do [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO (Replication Management Objects): as propriedades <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> e <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> para <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>.|  
|Conta de serviço do Windows para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent|Gerenciador de Configurações do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|Aplicativo autônomo|O Merge Agent executa sob o contexto do usuário do Windows que estiver executando o aplicativo.|  
  
## <a name="b-connection-to-the-subscriber"></a>B. Conexão com o Assinante  
 O Merge Agent conecta-se com Assinante usando a Autenticação do Windows ou a ou Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O usuário do Windows ou o logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você especificar deve ser associado a um usuário de banco de dados que seja membro da função de banco de dados fixa **dbowner** , no banco de dados de assinatura.  
  
> [!NOTE]  
>  A Autenticação do Windows é sempre usada quando o Merge Agent é iniciado de um trabalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. A Autenticação do Windows é também usada quando o Merge Agent é iniciado de forma programada, a menos que a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esteja especificada explicitamente.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|Autenticação do Windows.|O Merge Agent efetua conexões sob o contexto do usuário do Windows que estiver especificado para o Merge Agent (A).|  
|A Autenticação do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só será usada se o seguinte estiver especificado:<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **0** para **SubscriberSecurityMode**.|RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberLogin%2A> e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriberPassword%2A>.<br /><br /> Linha de comando do Merge Agent: **-SubscriberLogin** e **-SubscriberLogin**.|  
  
## <a name="c-connection-to-an-outgoing-proxy-server"></a>C. Conexão com um servidor proxy de saída  
 Especifique um usuário Windows para esta conexão somente se houver um servidor proxy de saída que restrinja o acesso a uma rede interna do Assinante.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|Autenticação do Windows|RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyLogin%2A> e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyPassword%2A> com <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetProxyServer%2A>.<br /><br /> A linha de comando do Merge Agent: **-InternetProxyLogin** e **-InternetProxyPassword** com **- InternetProxyServer**.|  
  
## <a name="d-connection-to-iis"></a>D. Conexão com o IIS  
 Após conectar-se ao Assinante e extrair as alterações do banco de dados de assinatura, o Merge Agent emite uma solicitação HTTPS ao [!INCLUDE[msCoName](../../../includes/msconame-md.md)] IIS (Serviços de Informações da Internet) e carrega as alterações de dados como uma mensagem XML. O Merge Agent deve ter permissões de logon para o IIS.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|A Autenticação Básica será usada se um dos itens a seguir for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **0** para o **@internet_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **0** para **- InternetSecurityMode**.|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: os parâmetros **@internet_login** e **@internet_password** do [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetLogin%2A> e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetPassword%2A>.<br /><br /> Linha de comando do Merge Agent: **-InternetLogin** e **-InternetPassword**.|  
|Autenticação integrada\* será usado se um dos seguintes for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **1** para o **@internet_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.InternetSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **1** para **- InternetSecurityMode**.|O Merge Agent efetua conexões sob o contexto do usuário do Windows que estiver especificado para o Merge Agent (A).|  
  
 \* Autenticação integrada pode ser usada somente se todos os computadores estiverem no mesmo domínio ou em vários domínios que tenham relações de confiança entre si.  
  
> [!NOTE]  
>  A delegação é necessária quando se usa a Autenticação integrada. Recomendamos usar a Autenticação Básica e o SSL para conexões do Assinante com o IIS.  
  
## <a name="e-connection-to-the-publisher"></a>E. Conexão com o Publicador  
 Os componentes do Replication Listener e do Reconciliador de Replicação de Mesclagem do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estão hospedados no computador que está executando o IIS. Esses componentes executam as seguintes ações:  
  
-   Retiram a solicitação HTTPS descrita na seção "D. Conexão com o IIS."  
  
-   Efetuam uma conexão SQL com o banco de dados de publicação e aplicam as alterações carregadas no banco de dados de publicação.  
  
-   Extraem as alterações baixadas e retornam uma resposta em HTTPS ao Merge Agent.  
  
 O Reconciliador de Replicação de Mesclagem se conecta ao Publicador usando a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O usuário do Windows ou o login do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você especificar deve ser compatível com o seguinte:  
  
-   Estar na lista de acesso à publicação (PAL). Para obter mais informações, consulte [Secure the Publisher](secure-the-publisher.md) (Proteger o publicador).  
  
-   Estar associado a um usuário no banco de dados de publicação.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|A Autenticação do Windows será usada se um dos seguintes for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **1** para o **@publisher_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **1** para **- PublisherSecurityMode**.|O Merge Agent efetua conexões com o Publicador no contexto do usuário do Windows que estiver especificado para a conexão com o ISS (D). Se o Publicador e o ISS estiverem em computadores diferentes e a Autenticação Integrada for usada para a conexão (D), será preciso habilitar a delegação Kerberos no computador executando o IIS. Para obter mais informações, consulte a documentação do Windows.|  
|A Autenticação do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será usada se um dos seguintes for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **0** para o **@publisher_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **0** para **- PublisherSecurityMode**.|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: os parâmetros **@publisher_login** e **@publisher_password** do [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A> e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A>.<br /><br /> Linha de comando do Merge Agent: **-PublisherLogin** e **-PublisherPassword**.|  
  
## <a name="f-connection-to-the-distributor"></a>F. Conexão com o Distribuidor  
 O Replication Listener e o Reconciliador de Replicação de Mesclagem que estão hospedados no computador que está executando o IIS, também efetuam conexões com o Distribuidor. O Reconciliador de Replicação de Mesclagem conecta-se com o Distribuidor usando a Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O usuário do Windows ou o login do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você especificar deve ser compatível com o seguinte:  
  
-   Estar na lista de acesso à publicação (PAL). Para obter mais informações, consulte [Secure the Publisher](secure-the-publisher.md) (Proteger o publicador).  
  
-   Estar associado a um usuário de banco de dados no banco de dados de distribuição. O usuário pode ser o usuário `Guest`.  
  
 Geralmente, o compartilhamento de instantâneos está no Distribuidor. Para obter mais informações sobre os compartilhamentos de instantâneos, consulte a seção "H. Acesso ao compartilhamento de instantâneos", mais adiante nesse tópico.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|A Autenticação do Windows será usada se um dos seguintes for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **1** para o **@distributor_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **1** para **- DistributorSecurityMode**.|O Merge Agent efetua conexões ao Distribuidor sob o contexto do usuário do Windows especificado para a conexão com o IIS (D). Se o Distribuidor e o ISS estiverem em computadores diferentes e a Autenticação Integrada for usada para a conexão (D), será preciso habilitar a delegação Kerberos no computador executando o IIS. Para obter mais informações, consulte a documentação do Windows.|  
|A Autenticação do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será usada se um dos seguintes for especificado:<br /><br /> [!INCLUDE[tsql](../../../includes/tsql-md.md)]: um valor de **0** para o **@distributor_security_mode** parâmetro [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: um valor de <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> para <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>.<br /><br /> Linha de comando do agente de mesclagem: um valor de **0** para **- DistributorSecurityMode**.|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: os parâmetros **@distributor_login** e **@distributor_password** do [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql).<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A> e <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A><br /><br /> Linha de comando do Merge Agent: **-DistributorLogin** e **-DistributorPassword**.|  
  
## <a name="g-connection-to-an-ftp-server"></a>G. Conexão com um servidor de FTP  
 Especifique um usuário do Windows para esta conexão somente se pretende baixar arquivos de instantâneos de um servidor de FTP, em vez de um local UNC, para o computador executando o IIS, antes de aplicar o instantâneo ao Assinante. Para obter mais informações, consulte [Transferir instantâneos pelo FTP](../transfer-snapshots-through-ftp.md).  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|Autenticação do Windows|[!INCLUDE[tsql](../../../includes/tsql-md.md)]: os parâmetros **@ftp_login** e **@ftp_password** do [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql).<br /><br /> RMO: <xref:Microsoft.SqlServer.Replication.Publication.FtpLogin%2A> e <xref:Microsoft.SqlServer.Replication.Publication.FtpPassword%2A>.|  
  
## <a name="h-access-to-the-snapshot-share"></a>H. Acesso a um compartilhamento de instantâneos  
 O compartilhamento de instantâneos é acessado pelo Reconciliador de Replicação de Mesclagem hospedado no computador que está executando IIS.  
  
|Tipo de autenticação|Onde a autenticação é especificada|  
|----------------------------|-------------------------------------------|  
|Autenticação do Windows|O Merge Agent acessa o compartilhamento de instantâneos sob o contexto do usuário do Windows especificado para a conexão ao IIS (D). Se o compartilhamento de instantâneos e o ISS estiverem em computadores diferentes e a Autenticação Integrada for usada para a conexão (D), será preciso habilitar a delegação Kerberos no computador executando o IIS. Para obter mais informações, consulte a documentação do Windows.|  
  
## <a name="i-application-pool-account-for-iis"></a>I. Conta do pool de aplicativos para o IIS  
 Essa conta é usada para iniciar o processo W3wp.exe no computador executando o IIS para [!INCLUDE[winxpsvr](../../../includes/winxpsvr-md.md)] ou o processo Dllhost.exe no [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)]. Esses processos hospedam aplicativos no computador executando o IIS, como o Replication Listener e o Reconciliador de Replicação de Mesclagem do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Essa conta deve ter permissões de leitura e de execução nos seguintes DLLs de replicação no computador executando o IIS:  
  
-   Replisapi  
  
-   Replrec  
  
-   Replprov  
  
-   Msgprox  
  
-   Xmlsub  
  
 A conta deve fazer também parte do grupo IIS_WPG. Para obter mais informações, consulte a seção “Configurando permissões para o Ouvinte de replicação de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]“ em [Configurar IIS para sincronização da Web](../configure-iis-for-web-synchronization.md).  
  
|Tipo de conta|Onde a conta é especificada|  
|---------------------|------------------------------------|  
|Qualquer usuário do Windows que tenha as permissões exigidas.|Gerenciador dos Serviços de Informações da Internet (IIS).|  
  
## <a name="see-also"></a>Consulte também  
 [Configure Web Synchronization](../configure-web-synchronization.md)   
 [Replication Merge Agent](../agents/replication-merge-agent.md)  
  
  
