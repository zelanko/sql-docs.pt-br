---
title: "Configurar contas e permissões do serviço Windows | Microsoft Docs"
ms.custom: 
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- startup service states [SQL Server]
- Setup [SQL Server], user accounts
- Windows permissions [SQL Server]
- modifying user accounts
- default accounts
- domains [SQL Server], user accounts
- startup accounts [SQL Server]
- system accounts [SQL Server]
- services [SQL Server], permissions
- ACL (access control list)
- local system accounts [SQL Server]
- instance-aware services [SQL Server]
- permissions [SQL Server], services
- SQL Server Agent service, user accounts
- Windows NT permissions [SQL Server]
- user accounts [SQL Server]
- identifying instance-unaware services [SQL Server]
- installing SQL Server, user accounts
- disabled startup state [SQL Server]
- user accounts [SQL Server], users
- Local Service account [SQL Server]
- SQL Server Installation Wizard
- instance-unaware services [SQL Server]
- services [SQL Server], configuring at installation
- Windows accounts [SQL Server]
- SQL Server services, user accounts
- user accounts [SQL Server], services
- MSSQLServer
- identifying instance-aware services [SQL Server]
- services [SQL Server], accounts
- access control lists
- optional accounts [SQL Server]
- service accounts [SQL Server]
- accounts [SQL Server], services
- built-in system accounts [SQL Server]
- automatic startup state
- domains [SQL Server]
- manual startup state [SQL Server]
- accounts [SQL Server], user
ms.assetid: 309b9dac-0b3a-4617-85ef-c4519ce9d014
caps.latest.revision: 
author: MikeRayMSFT
ms.author: MikeRayMSFT
manager: craigg
ms.workload: Active
ms.openlocfilehash: 85893d6f71a6caf270a56910418fe8217906ed76
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-windows-service-accounts-and-permissions"></a>Configurar contas de serviço e permissões do Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > Para obter o conteúdo relacionado a versões anteriores do SQL Server, consulte [Configurar contas e permissões do serviço Windows](https://msdn.microsoft.com/en-US/library/ms143504(SQL.120).aspx).


  Cada serviço no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representa um processo ou um conjunto de processos para gerenciar a autenticação das operações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o Windows. Este tópico descreve a configuração padrão de serviços nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e as opções de configuração de serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode definir durante e após a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este tópico ajuda usuários avançados a entender os detalhes das contas de serviço.  
  
 A maioria dos serviços e suas propriedades podem ser configurados usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Aqui estão os caminhos para as últimas quatro versões Windows instaladas na unidade C.  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  

##  <a name="Service_Details"></a> Serviços instalados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Dependendo dos componentes que você decidir instalar, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalará os seguintes serviços:  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database Services** : o serviço para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacional do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O arquivo executável é \<MSSQLPATH>\MSSQL\Binn\sqlservr.exe.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent** : executa trabalhos, monitora o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dispara alertas e habilita a automação de algumas tarefas administrativas. O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está presente, mas desabilitado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. O arquivo executável é \<MSSQLPATH>\MSSQL\Binn\sqlagent.exe.  
  
-   **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]**  : fornece funcionalidade de mineração de dados e OLAP (processamento analítico online) para aplicativos de business intelligence. O arquivo executável é \<MSSQLPATH>\OLAP\Bin\msmdsrv.exe.  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**  : gerencia, executa, cria, agenda e entrega relatórios. O arquivo executável é \<MSSQLPATH>\Reporting Services\ReportServer\Bin\ReportingServicesService.exe.  
  
-   **[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]**  : fornece suporte de gerenciamento para o armazenamento e a execução de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O caminho do executável é \<MSSQLPATH>\130\DTS\Binn\MsDtsSrvr.exe  
  
-   **Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: o serviço de resolução de nomes que especifica informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para computadores cliente. O caminho do executável é c:\Arquivos de Programas (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe  
  
-   **Pesquisa de texto completo** : cria rapidamente índices de texto completo sobre conteúdo e propriedades de dados estruturados e semiestruturados para fornecer filtragem de documentos e separação de palavras para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Gravador do SQL** : permite que aplicativos de backup e restauração operem na estrutura do VSS (Serviço de Cópias de Sombra de Volume).
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller** : fornece orquestração de reprodução de rastreamento em vários computadores cliente Distributed Replay Client.  
  
-   **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client** : um ou mais computadores cliente do Distributed Replay Client que funcionam junto com um Distributed Replay Controller para simular cargas de trabalho simultâneas em relação a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**  : um serviço confiável que hospeda executáveis externos fornecidos pela Microsoft, como o tempo de execução de R instalado como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Processos de satélite podem ser iniciados pelo processo do Launchpad, mas serão controlados por recursos, com base na configuração da instância individual. O serviço Launchpad será executado em sua própria conta de usuário e cada processo de satélite para um tempo de execução registrado específico herdará a conta de usuário do Launchpad. Processos de satélite são criados e destruídos sob demanda durante o tempo de execução.

    O Launchpad não é capaz de criar as contas que ele utiliza se você instala o SQL Server em um computador que também é usado como um controlador de domínio. Portanto, a instalação dos R Services (no banco de dados) ou Serviços de Machine Learning (No Banco de Dados) falha em um controlador de domínio.

  
 - **Mecanismo PolyBase do SQL Server** – fornece funcionalidades de consulta distribuída para fontes de dados externas.
 
 - **Serviço de Movimentação de Dados PolyBase do SQL Server** – permite a movimentação de dados entre o SQL Server e Fontes de Dados Externas e entre nós do SQL em Grupos de Expansão PolyBase.
  
##  <a name="Serv_Prop"></a> Propriedades e configuração do serviço

As contas de inicialização usadas para iniciar e executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser [contas de usuário de domínio](#Domain_User), [contas de usuário locais](#Local_User), [contas de serviço gerenciado](#MSA), [contas virtuais](#VA_Desc)ou [contas de sistema internas](#Local_Service). Para ser iniciado e executado, cada serviço no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter uma conta de inicialização configurada durante a instalação.
  
 Esta seção descreve as contas que podem ser configuradas para iniciar os serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , os valores padrão usados pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o conceito de SIDs por serviço, as opções de inicialização e a configuração de firewall.  
  
-   [Contas de serviço padrão](#Default_Accts)  
  
-   [Inicialização automática](#Auto_Start)  
  
-   [Configurando o tipo de inicialização do serviço](#Configure_services)  
  
-   [Porta do firewall](#Firewall)  
  
###  <a name="Default_Accts"></a> Contas de serviço padrão

A tabela a seguir lista as contas de serviço padrão usadas pela instalação ao instalar todos os componentes. As contas padrão listadas são as contas recomendadas, exceto como observado.
  
 **Servidor autônomo ou controlador de domínio**
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|Windows 7 e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 e posterior|  
|---------------|------------------------------------|----------------------------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssRS](../../includes/ssrs-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)*|  
|Iniciador FD (Pesquisa de texto completo)|[SERVIÇO LOCAL](#Local_Service)|[Conta Virtual](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|[SERVIÇO LOCAL](#Local_Service)|[SERVIÇO LOCAL](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gravador VSS|[SISTEMA LOCAL](#Local_System)|[SISTEMA LOCAL](#Local_System)|  
|[!INCLUDE[rsql_extensions](../../includes/rsql-extensions-md.md)]|NTSERVICE\MSSQLLaunchpad|NTSERVICE\MSSQLLaunchpad|  
|Mecanismo PolyBase  |[SERVIÇO DE REDE](#Network_Service) |[SERVIÇO DE REDE](#Network_Service)  |
|Serviço de Movimentação de Dados PolyBase |[SERVIÇO DE REDE](#Network_Service) |[SERVIÇO DE REDE](#Network_Service)  |
  
 *Quando recursos externos ao computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são necessários, a [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomenda usar uma MSA (Conta de Serviço Gerenciado), configurada com os privilégios mínimos necessários.  
  
 **Instância de cluster de failover do SQL Server**
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2|  
|---------------|------------------------------------|---------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|Nenhum. Forneça uma conta de [usuário de domínio](#Domain_User) .|Forneça uma conta de [usuário de domínio](#Domain_User) .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|Nenhum. Forneça uma conta de [usuário de domínio](#Domain_User) .|Forneça uma conta de [usuário de domínio](#Domain_User) .|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|Nenhum. Forneça uma conta de [usuário de domínio](#Domain_User) .|Forneça uma conta de [usuário de domínio](#Domain_User) .|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)|  
|[!INCLUDE[ssRS](../../includes/ssrs-md.md)]|[SERVIÇO DE REDE](#Network_Service)|[Conta Virtual](#VA_Desc)|  
|Iniciador FD (Pesquisa de texto completo)|[SERVIÇO LOCAL](#Local_Service)|[Conta Virtual](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|[SERVIÇO LOCAL](#Local_Service)|[SERVIÇO LOCAL](#Local_Service)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gravador VSS|[SISTEMA LOCAL](#Local_System)|[SISTEMA LOCAL](#Local_System)|  

####  <a name="Changing_Accounts"></a> Alterando as propriedades da conta
  
> [!IMPORTANT]  
>  -   Sempre use as ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, para alterar a conta usada pelos serviços [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ou para alterar a senha da conta. Além de alterar o nome da conta, o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa configurações adicionais, como a atualização do repositório de segurança local do Windows, que protege a chave mestra do serviço para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Outras ferramentas, como o Gerenciador de Controle de Serviços do Windows, podem alterar o nome da conta, mas não alteram todas as configurações necessárias.  
> -   Para instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implantadas em um farm do SharePoint, use sempre a Administração Central do SharePoint para alterar as contas de servidor dos aplicativos [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] e [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. As configurações e permissões associadas serão atualizadas para usar as novas informações da conta quando você usar a Administração Central.  
> -   Para alterar as opções do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , use a Ferramenta de Configuração do Reporting Services.  
  
###  <a name="New_Accounts"></a> Contas de serviço gerenciado, contas de serviço gerenciado de grupo e contas virtuais  
  
As contas de serviço gerenciado, as contas de serviço gerenciado de grupo e as contas virtuais são criadas para fornecer aplicativos cruciais, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o isolamento das próprias contas, eliminando a necessidade de um administrador gerenciar manualmente o SPN (Nome da Entidade de Serviço) e as credenciais dessas contas. Isso facilita bastante o gerenciamento de usuários de contas de serviço, senhas e SPNs a longo prazo.  
  
-   <a name="MSA"></a> **Managed Service Accounts**  
  
     Uma MSA é um tipo de conta de domínio criada e gerenciada pelo controlador de domínio. Ela é atribuída a um único computador membro para a execução de um serviço. A senha é gerenciada automaticamente pelo controlador de domínio. Não é possível usar uma MSA para fazer logon em um computador, mas um computador pode usar uma MSA para iniciar um serviço do Windows. Uma MSA tem a capacidade de registrar SPN com o Active Directory. Uma MSA é nomeada com um sufixo **$** , por exemplo, **DOMAIN\ACCOUNTNAME$**. Ao especificar uma MSA, deixe a senha em branco. Como um MSA é atribuído a um único computador, não pode ser usado em diferentes nós de um cluster do windows.  
  
    > [!NOTE]  
    >  A MSA deve ser criada no Active Directory pelo administrador de domínio antes que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa usá-la para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-  <a name="GMSA"></a> **Contas de serviço gerenciado de grupo**  
  
     Uma conta de serviço gerenciado de grupo é uma MSA para vários servidores. O Windows gerencia uma conta de serviço para os serviços executados em um grupo de servidores. O Active Directory atualiza automaticamente a senha da conta de serviço gerenciado de grupo sem reiniciar os serviços. Você pode configurar os serviços do SQL Server para usar uma entidade da conta de serviço gerenciado de grupo. A partir do SQL Server 2014, o SQL Server dá suporte a contas de serviço gerenciado de grupo no Windows Server 2012 R2 e posterior para instâncias autônomas, instâncias de cluster de failover e grupos de disponibilidade.  
  
    Para usar uma conta de serviço gerenciado de grupo para o SQL Server 2014 ou posterior, o sistema operacional precisa ser o Windows Server 2012 R2 ou posterior. Servidores com o Windows Server 2012 R2 requerem que o [KB 2998082](http://support.microsoft.com/kb/2998082) seja aplicado de forma que os serviços possam fazer logon sem interrupção imediatamente após uma alteração de senha.  
  
    Para obter mais informações, consulte [Contas de Serviço Gerenciado de grupo](http://technet.microsoft.com/library/hh831782.aspx)  
      
    > [!NOTE]  
    >  A conta de serviço gerenciado de grupo deve ser criada no Active Directory pelo administrador de domínio antes que a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa usá-la para serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   <a name="VA_Desc"></a>**Virtual Accounts**  
  
    As contas virtuais (começando com o Windows Server 2008 R2 e no Windows 7) são *contas locais gerenciadas* que fornecem os recursos a seguir para simplificar a administração do serviço. A conta virtual é autogerenciada e pode acessar a rede em um ambiente de domínio. Se o valor padrão for usado para as contas de serviço durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], será usada uma conta virtual que usa o nome da instância como o nome do serviço, no formato **NT SERVICE\\***\<SERVICENAME>*. Os serviços executados como contas virtuais acessam recursos de rede usando as credenciais da conta do computador no formato *<domain_name>***\\***<computer_name>***$**.  Ao especificar uma conta virtual para iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deixe a senha em branco. Se a conta virtual não registra o SPN (Nome da Entidade de Serviço), registre-o manualmente. Para obter mais informações sobre como registrar um SPN manualmente, confira [Registro manual de SPN](https://msdn.microsoft.com/library/ms191153.aspx).  
  
    > [!NOTE]  
    >  As contas virtuais não podem ser usadas para a Instância de Cluster de Failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque a conta virtual não teria o mesmo SID em cada nó do cluster.  
  
     A tabela a seguir lista exemplos de nomes de contas virtuais.  
  
    |Serviço|Nome da conta virtual|  
    |-------------|--------------------------|  
    |A instância padrão do serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)]|**NT SERVICE\MSSQLSERVER**|  
    |A instância nomeada de um serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] nomeado **PAYROLL**|**NT SERVICE\MSSQL$PAYROLL**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent na instância padrão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|**NT SERVICE\SQLSERVERAGENT**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chamada **PAYROLL**|**NT SERVICE\SQLAGENT$PAYROLL**|  
  
 Para obter mais informações sobre Contas de Serviço Gerenciado e Contas Virtuais, consulte a seção **Managed service account and virtual account concepts** (Conceitos de conta de serviço gerenciado e conta virtual) do [Service Accounts Step-by-Step Guide](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx) (Guia passo a passo de contas de serviço) e [Managed Service Accounts Frequently Asked Questions (FAQ)](http://technet.microsoft.com/library/ff641729\(WS.10\).aspx)(Perguntas frequentes sobre contas de serviço gerenciado).  
  
 **Observação de segurança:** [!INCLUDE[ssNoteLowRights](../../includes/ssnotelowrights-md.md)] Use um [MSA](#MSA) ou [virtual account](#VA_Desc) quando possível. Quando a MSA e as contas virtuais não forem possíveis, use uma conta de usuário específica de baixo privilégio ou uma conta de domínio em vez de uma conta compartilhada para os serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use contas separadas para serviços diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não conceda permissões adicionais à conta de serviço ou a grupos de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As permissões serão concedidas por meio da associação de grupo ou diretamente a um SID de serviço, onde um SID de serviço tiver suporte.  
  
###  <a name="Auto_Start"></a> Inicialização automática

Além de ter contas de usuário, todo serviço tem três possíveis estados de inicialização que os usuários podem controlar:
  
-   **Desabilitado** O serviço está instalado, mas não está em execução atualmente.  
  
-   **Manual** O serviço está instalado, mas será iniciado somente quando outro serviço ou aplicativo precisar de sua funcionalidade.  
  
-   **Automático** O serviço é iniciado automaticamente pelo sistema operacional.  
  
 O estado de inicialização é selecionado durante a instalação. Ao instalar uma instância nomeada, o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser definido para iniciar automaticamente.  
  
###  <a name="Configure_services"></a> Configurando serviços durante a instalação autônoma

A tabela a seguir mostra os serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem ser configurados durante a instalação. Para instalações autônomas, você pode usar as opções em um arquivo de configuração ou em um prompt de comando.  
  
|Nome do serviço SQL Server|Opções para instalações autônomas*|  
|-----------------------------|---------------------------------------------|  
|MSSQLSERVER|SQLSVCACCOUNT, SQLSVCPASSWORD, SQLSVCSTARTUPTYPE|  
|SQLServerAgent**|AGTSVCACCOUNT, AGTSVCPASSWORD, AGTSVCSTARTUPTYPE|  
|MSSQLServerOLAPService|ASSVCACCOUNT, ASSVCPASSWORD, ASSVCSTARTUPTYPE|  
|ReportServer|RSSVCACCOUNT, RSSVCPASSWORD, RSSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|ISSVCACCOUNT, ISSVCPASSWORD, ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay|DRU_CTLR, CTLRSVCACCOUNT, CTLRSVCPASSWORD, CTLRSTARTUPTYPE, CTLRUSERS|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay|DRU_CLT, CLTSVCACCOUNT, CLTSVCPASSWORD, CLTSTARTUPTYPE, CLTCTLRNAME, CLTWORKINGDIR, CLTRESULTDIR|  
|[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]|EXTSVCACCOUNT, EXTSVCPASSWORD, ADVANCEDANALYTICS***|
|Mecanismo PolyBase| PBENGSVCACCOUNT, PBENGSVCPASSWORD, PBENGSVCSTARTUPTYPE, PBDMSSVCACCOUNT,PBDMSSVCPASSWORD, PBDMSSVCSTARTUPTYPE, PBSCALEOUT, PBPORTRANGE
  
 *Para obter mais informações e a sintaxe de exemplo para instalações autônomas, consulte [Instalar o SQL Server 2016 do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
 **O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é desabilitado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] com Advanced Services.

 ***Não há suporte atualmente para configurar a conta para a barra inicial apenas por meio de comutadores. Para alterar a conta e outras configurações de serviço, use o SQL Server Configuration Manager.

###  <a name="Firewall"></a> Porta do firewall

Na maioria dos casos, quando inicialmente instalado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode ser conectado por ferramentas como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , instalado no mesmo computador que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não abre portas no firewall do Windows. Talvez não sejam possíveis conexões de outros computadores até que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] seja configurado para ouvir em uma porta TCP e a porta apropriada seja aberta para conexões no firewall do Windows. Para obter mais informações sobre como fazer isso, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="Serv_Perm"></a> Permissões de serviço

Esta seção descreve as permissões que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura para os SIDs por serviço dos serviços [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Configuração de serviço e controle de acesso](#Serv_SID)  
  
-   [Privilégios e direitos do Windows](#Windows)  
  
-   [Permissões do sistema de arquivos concedidas a SIDs por serviço do SQL Server ou a grupos locais do Windows do SQL Server](#Reviewing_ACLs)  
  
-   [Permissões do sistema de arquivos concedidas a outros grupos ou contas de usuário do Windows](#File_System_Other)  
  
-   [Permissões do sistema de arquivos relacionadas a locais de disco incomuns](#Unusual_Locations)  
  
-   [Revisando considerações adicionais](#Review_additional_considerations)  
  
-   [Permissões de Registro](#Registry)  
  
-   [WMI](#WMI)  
  
-   [Pipes nomeados](#Pipes)  
  
###  <a name="Serv_SID"></a> Configuração de serviço e controle de acesso

O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] habilita o SID por serviço para cada um de seus serviços para fornecer isolamento do serviço e defesa em profundidade. O SID por serviço é derivado do nome do serviço e é exclusivo ao serviço. Por exemplo, um nome de SID de serviço para o serviço [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser **NT Service\MSSQL$***\<InstanceName>*. O isolamento de serviço permite acessar objetos específicos sem a necessidade de executar uma conta de privilégios mais altos nem de limitar a proteção de segurança do objeto. Ao usar uma entrada de controle de acesso que contenha um SID de serviço, um serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode restringir o acesso a seus recursos.
  
> [!NOTE]  
>  No Windows 7 e no [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 (e posterior), o SID por serviço pode ser a conta virtual usada pelo serviço.
  
 Para a maioria dos componentes, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura a ACL para a conta por serviço diretamente. Dessa forma, a alteração da conta de serviço pode ser efetuada sem a necessidade de repetir o processo da ACL de recurso.
  
 Ao instalar o [!INCLUDE[ssAS](../../includes/ssas-md.md)], será criado um SID por serviço para o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Um grupo local do Windows é criado, nomeado no formato **SQLServerMSASUser$***computer_name***$***instance_name*. O SID **NT SERVICE\MSSQLServerOLAPService** por serviço recebe permissão de associação no grupo local do Windows, e o grupo local do Windows recebe as permissões apropriadas na ACL. Se a conta usada para iniciar o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] for alterada, o Gerenciador de Configurações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá alterar algumas permissões do Windows (como o direito de fazer logon como um serviço), mas as permissões atribuídas ao grupo local do Windows ainda estarão disponíveis sem qualquer atualização, pois o SID por serviço não foi alterado. Esse método permite que o serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seja renomeado durante atualizações.
  
 Durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria grupos locais do Windows para o serviço [!INCLUDE[ssAS](../../includes/ssas-md.md)] e o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para esses serviços, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura a ACL para os grupos locais do Windows.  
  
 Dependendo da configuração do serviço, a conta de serviço para um serviço ou SID de serviço é adicionada como um membro do grupo de serviços durante a instalação ou atualização.
  
###  <a name="Windows"></a> Privilégios e direitos do Windows  
 A conta atribuída para iniciar um serviço precisa da **permissão Iniciar, parar e pausar** para o serviço. O programa de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui automaticamente essa permissão.  Primeiro instale as Ferramentas de Administração de Servidor Remoto. Consulte o artigo sobre as [Ferramentas de Administração de Servidor Remoto para Windows 7](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=7d2f6ad7-656b-4313-a005-4e344e43997d).
  
 A tabela a seguir mostra as permissões que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita para os SIDs por serviço ou para os grupos locais do Windows usados pelos componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
|Serviço do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Permissões concedidas pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|
|---------------------------------------|------------------------------------------------------------|
|**[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:**<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão: **NT SERVICE\MSSQLSERVER**. Instância nomeada: **NT SERVICE\MSSQL$**InstanceName.)|**Fazer logon como um serviço** (SeServiceLogonRight)<br /><br /> **Substituir um token no nível de processo** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Ignorar a verificação completa** (SeChangeNotifyPrivilege)<br /><br /> **Ajustar quotas de memória para um processo** (SeIncreaseQuotaPrivilege)<br /><br /> Permissão para iniciar o Gravador do SQL<br /><br /> Permissão para ler o serviço Log de Eventos<br /><br /> Permissão para ler o serviço Chamada de Procedimento Remoto|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:** \*<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão: **NT Service\SQLSERVERAGENT**. Instância nomeada: **NT Service\SQLAGENT$***InstanceName*).|**Fazer logon como um serviço** (SeServiceLogonRight)<br /><br /> **Substituir um token no nível de processo** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Ignorar a verificação completa** (SeChangeNotifyPrivilege)<br /><br /> **Ajustar quotas de memória para um processo** (SeIncreaseQuotaPrivilege)|  
|**[!INCLUDE[ssAS](../../includes/ssas-md.md)]:**<br /><br /> (Todos os direitos são concedidos a um grupo local do Windows. Instância padrão: **SQLServerMSASUser$***ComputerName***$MSSQLSERVER**. Instância nomeada: **SQLServerMSASUser$***ComputerName***$***InstanceName*. Instância [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]: **SQLServerMSASUser$***ComputerName***$***PowerPivot*).|**Fazer logon como um serviço** (SeServiceLogonRight)<br /><br /> Somente tabular:<br /><br /> **Aumentar conjunto de trabalho de processo** (SeIncreaseWorkingSetPrivilege)<br /><br /> **Ajustar cotas de memória para um processo** (SeIncreaseQuotaSizePrivilege)<br /><br /> **Bloquear páginas na memória** (SeLockMemoryPrivilege): isso é necessário somente quando a paginação está totalmente desativada.<br /><br /> Somente para instalações de cluster de failover:<br /><br /> **Aumentar a prioridade de planejamento** (SeIncreaseBasePriorityPrivilege)|  
|**[!INCLUDE[ssRS](../../includes/ssrs-md.md)]:**<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão: **NT SERVICE\ReportServer**. Instância nomeada: **NT SERVICE\\ReportServer$***InstanceName*).|**Fazer logon como um serviço** (SeServiceLogonRight)|  
|**[!INCLUDE[ssIS](../../includes/ssis-md.md)]:**<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão e instância nomeada: **NT SERVICE\MsDtsServer130**. O[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não tem um processo separado para uma instância nomeada).|**Fazer logon como um serviço** (SeServiceLogonRight)<br /><br /> Permissão para gravar no log de eventos do aplicativo.<br /><br /> **Ignorar a verificação completa** (SeChangeNotifyPrivilege)<br /><br /> **Representar um cliente após autenticação** (SeImpersonatePrivilege)|  
|**Pesquisa de texto completo:**<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão: **NT Service\MSSQLFDLauncher**. Instância nomeada: **NT Service\ MSSQLFDLauncher$***InstanceName*).|**Fazer logon como um serviço** (SeServiceLogonRight)<br /><br /> **Ajustar quotas de memória para um processo** (SeIncreaseQuotaPrivilege)<br /><br /> **Ignorar a verificação completa** (SeChangeNotifyPrivilege)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador:**<br /><br /> (Todos os direitos são concedidos a um grupo local do Windows. Instância padrão ou nomeada: **SQLServer2005SQLBrowserUser***$ComputerName*. O Navegador do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem um processo separado para uma instância nomeada.)|**Fazer logon como um serviço** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gravador VSS:**<br /><br /> (Todos os direitos são concedidos ao SID por serviço. Instância padrão ou nomeada: **NT Service\SQLWriter**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Gravador VSS não tem um processo separado para uma instância nomeada).|O SQLWriter é executado sob a conta LOCAL SYSTEM que tem todas as permissões exigidas. A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não verifica nem concede permissões para este serviço.| 
  |**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay:**|**Fazer logon como um serviço** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay:**|**Fazer logon como um serviço** (SeServiceLogonRight)|  
|**Mecanismo PolyBase e DMS**| **Fazer logon como um serviço** (SeServiceLogonRight)  |   
|**Launchpad:**|**Fazer logon como um serviço** (SeServiceLogonRight) <br /><br /> **Substituir um token no nível de processo** (SeAssignPrimaryTokenPrivilege)<br /><br />**Ignorar a verificação completa** (SeChangeNotifyPrivilege)<br /><br />**Ajustar quotas de memória para um processo** (SeIncreaseQuotaPrivilege)|     
|**Serviços do R:** **SQLRUserGroup**  |**Permitir logon local** |   

 *O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está desabilitado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
###  <a name="Reviewing_ACLs"></a> Permissões do sistema de arquivos concedidas a SIDs por serviço do SQL Server ou a grupos locais do Windows  
 As contas de serviço do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ter acesso aos recursos. As listas de controle de acesso são definidas para o SID por serviço ou para o grupo local do Windows.  
  
> [!IMPORTANT]  
>  Para instalações de cluster de failover, os recursos em discos compartilhados devem ser definidos como uma ACL para uma conta local.  
  
 A tabela a seguir mostra as ACLs que são definidas pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
|Conta de serviço para|Arquivos e pastas|Acesso|  
|-------------------------|-----------------------|------------|  
|MSSQLServer|Instid\MSSQL\backup|Controle total|  
||Instid\MSSQL\binn|Leitura, Execução|  
||Instid\MSSQL\data|Controle total|  
||Instid\MSSQL\FTData|Controle total|  
||Instid\MSSQL\Install|Leitura, Execução|  
||Instid\MSSQL\Log|Controle total|  
||Instid\MSSQL\Repldata|Controle total|  
||130\shared|Leitura, Execução|  
||Instid\MSSQL\Template Data (somente[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] )|Leitura|  
|SQLServerAgent*|Instid\MSSQL\binn|Controle total|  
||Instid\MSSQL\binn|Controle total|  
||Instid\MSSQL\Log|Leitura, Gravação, Exclusão, Execução|  
||130\com|Leitura, Execução|  
||130\shared|Leitura, Execução|  
||130\shared\Errordumps|Leitura, Gravação|  
||ServerName\EventLog|Controle total|  
|FTS|Instid\MSSQL\FTData|Controle total|  
||Instid\MSSQL\FTRef|Leitura, Execução|  
||130\shared|Leitura, Execução|  
||130\shared\Errordumps|Leitura, Gravação|  
||Instid\MSSQL\Install|Leitura, Execução|  
||Instid\MSSQL\jobs|Leitura, Gravação|  
|MSSQLServerOLAPService|130\shared\ASConfig|Controle total|  
||Instid\OLAP|Leitura, Execução|  
||Instid\Olap\Data|Controle total|  
||Instid\Olap\Log|Leitura, Gravação|  
||Instid\OLAP\Backup|Leitura, Gravação|  
||Instid\OLAP\Temp|Leitura, Gravação|  
||130\shared\Errordumps|Leitura, Gravação|  
|SQLServerReportServerUser|Instid\Reporting Services\Log Files|Leitura, Gravação, Exclusão|  
||Instid\Reporting Services\ReportServer|Leitura, Execução|  
||Instid\Reportingservices\Reportserver\global.asax|Controle total|  
||Instid\Reportingservices\Reportserver\Reportserver.config|leitura|  
||Instid\Reporting Services\reportManager|Leitura, Execução|  
||Instid\Reporting Services\RSTempfiles|Leitura, Gravação, Execução, Exclusão|  
||130\shared|Leitura, Execução|  
||130\shared\Errordumps|Leitura, Gravação|  
|MSDTSServer100|130\dts\binn\MsDtsSrvr.ini.xml|leitura|  
||130\dts\binn|Leitura, Execução|  
||130\shared|Leitura, Execução|  
||130\shared\Errordumps|Leitura, Gravação|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador|130\shared\ASConfig|leitura|  
||130\shared|Leitura, Execução|  
||130\shared\Errordumps|Leitura, Gravação|  
|SQLWriter|N/A (Executado como sistema local)||  
|Usuário|Instid\MSSQL\binn|Leitura, Execução|  
||Instid\Reporting Services\ReportServer|Leitura, Execução, Listar Conteúdo de Pastas|  
||Instid\Reportingservices\Reportserver\global.asax|leitura|  
||Instid\Reporting Services\reportManager|Leitura, Execução|  
||Instid\Reporting Services\ReportManager\pages|leitura|  
||Instid\Reporting Services\ReportManager\Styles|leitura|  
||130\dts|Leitura, Execução|  
||130\tools|Leitura, Execução|  
||100\tools|Leitura, Execução|  
||90\tools|Leitura, Execução|  
||80\tools|Leitura, Execução|  
||130\sdk|leitura|  
||Microsoft SQL Server\130\Setup Bootstrap|Leitura, Execução|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador Distributed Replay|\<ToolsDir>\DReplayController\Log\ (diretório vazio)|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\DReplayController.exe|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\resources\| Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\\{todas as dlls}|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\DReplayController.config|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\IRTemplate.tdf|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayController\IRDefinition.xml|Leitura, Execução, Listar Conteúdo de Pastas|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cliente Distributed Replay|\<ToolsDir>\DReplayClient\Log\| Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\DReplayClient.exe|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\resources\| Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\ (todas as dlls)|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\DReplayClient.config|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\IRTemplate.tdf|Leitura, Execução, Listar Conteúdo de Pastas|  
||\<ToolsDir>\DReplayClient\IRDefinition.xml|Leitura, Execução, Listar Conteúdo de Pastas|  
|Launchpad|%binn|Leitura, Execução|
||ExtensiblilityData|Controle total|
||Log\ExtensibiltityLog|Controle total|
  
 *O serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é desabilitado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] com Advanced Services.  
  
 Quando os arquivos de banco de dados são armazenados em um local definido pelo usuário, você deve conceder acesso ao SID por serviço para esse local. Para obter mais informações sobre como conceder permissões para um SID por serviço, consulte [Configurar permissões do sistema de arquivos para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md).  
  
###  <a name="File_System_Other"></a> Permissões do sistema de arquivos concedidas a outros grupos ou contas de usuário do Windows  

Poderá ser necessário conceder algumas permissões de controle de acesso a contas internas ou a outras contas do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A tabela a seguir lista ACLs adicionais que são definidas pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Componente solicitante|Conta|Recurso|Permissões|  
|--------------------------|-------------|--------------|-----------------|  
|MSSQLServer|Usuários do Log de Desempenho|Instid\MSSQL\binn|Listar conteúdo da pasta|  
||Usuários do Monitor de Desempenho|Instid\MSSQL\binn|Listar conteúdo da pasta|  
||Usuários do Log de Desempenho, Usuários do Monitor de Desempenho|\WINNT\system32\sqlctr130.dll|Leitura, Execução|  
||Somente Administrador|\\\\.\root\Microsoft\SqlServer\ServerEvents\\<nome_da_instância_sql>*|Controle total|  
||Administradores, Sistema|\tools\binn\schemas\sqlserver\2004\07\showplan|Controle total|  
||Usuários|\tools\binn\schemas\sqlserver\2004\07\showplan|Leitura, Execução|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|\<Report Server Web Service Account>|*\<install>*\Reporting Services\LogFiles|Delete (excluir)<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Identidade do pool de aplicativos do Gerenciador de Relatórios, conta do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , Todos|*\<install>*\Reporting Services\ReportManager, *\<install>*\Reporting Services\ReportManager\Pages\\\*.\*, *\<install>*\Reporting Services\ReportManager\Styles\\\*.\*, *\<install>*\Reporting Services\ReportManager\webctrl_client\1_0\\*.\*|leitura|  
||Identidade do pool de aplicativos do Gerenciador de Relatórios|*\<install>*\Reporting Services\ReportManager\Pages\\*.\*|leitura|  
||\<Report Server Web Service Account>|*\<install>*\Reporting Services\ReportServer|leitura|  
||\<Report Server Web Service Account>|*\<install>*\Reporting Services\ReportServer\global.asax|Completo|  
||Todos|*\<install>*\Reporting Services\ReportServer\global.asax|READ_CONTROL<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_READ_ATTRIBUTES|  
||SERVIÇO DE REDE|*\<install>*\Reporting Services\ReportServer\ReportService.asmx|Completo|  
||Todos|*\<install>*\Reporting Services\ReportServer\ReportService.asmx|READ_CONTROL<br /><br /> SYNCHRONIZE FILE_GENERIC_READ<br /><br /> FILE_GENERIC_EXECUTE<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_EXECUTE<br /><br /> FILE_READ_ATTRIBUTES|  
||Conta de Serviços do Windows do ReportServer|*\<install>*\Reporting Services\ReportServer\RSReportServer.config|Delete (excluir)<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Todos|Chaves do Servidor de Relatório (ramificação Instid)|Consultar Valor<br /><br /> Enumerar Subchaves<br /><br /> Notificar<br /><br /> Controle de Leitura|  
||Usuários dos Serviços de Terminal|Chaves do Servidor de Relatório (ramificação Instid)|Consultar Valor<br /><br /> Definir Valor<br /><br /> Criar Subchave<br /><br /> Enumerar Subchave<br /><br /> Notificar<br /><br /> DELETE<br /><br /> Controle de Leitura|  
||Usuários Avançados|Chaves do Servidor de Relatório (ramificação Instid)|Consultar Valor<br /><br /> Definir Valor<br /><br /> Criar Subchave<br /><br /> Enumerar Subchaves<br /><br /> Notificar<br /><br /> DELETE<br /><br /> Controle de Leitura|  
  
 *Este é o namespace do provedor WMI.  
  
###  <a name="Unusual_Locations"></a> Permissões do sistema de arquivos relacionadas a locais de disco incomuns  

A unidade padrão de locais para instalação é **systemdrive**, normalmente a unidade C. Esta seção descreve considerações adicionais quando tempdb ou bancos de dados de usuários são instalados em locais não usuais.  
  
 **Unidade não padrão**  
  
 Quando instalado em uma unidade local que não seja a unidade padrão, o SID por serviço deve ter acesso ao local do arquivo. A instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provisionará o acesso necessário.  
  
 **Compartilhamento de rede**  
  
 Quando bancos de dados são instalados em um compartilhamento de rede, a conta de serviço deve ter acesso ao local do arquivo do usuário e aos bancos de dados tempdb. A Instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode provisionar o acesso a um compartilhamento de rede. O usuário deve provisionar o acesso a um local de tempdb para a conta de serviço antes de executar a instalação. O usuário deve provisionar o acesso ao local do banco de dados de usuário antes de criar o banco de dados.  
  
> [!NOTE]  
>  Contas virtuais não podem ser autenticadas em um local remoto. Todas as contas virtuais usam a permissão da conta de máquina. Provisione a conta do computador no formato *<domain_name>***\\***<computer_name>***$**.  
  
###  <a name="Review_additional_considerations"></a> Revisando considerações adicionais  

A tabela a seguir mostra as permissões necessárias para que os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forneçam funcionalidade adicional.  
  
|Serviço/Aplicativo|Funcionalidade|Permissão necessária|  
|--------------------------|-------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|Gravar em um slot de email usando xp_sendmail.|Permissões de gravação de rede.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)|Executar xp_cmdshell para um usuário que não seja um administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Atuar como parte do sistema operacional e substituir um token de nível de processo.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (MSSQLSERVER)|Usar o recurso de reinicialização automática.|Deve ser um membro do grupo local Administradores.|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Orientador de Otimização|Ajusta bancos de dados para desempenho ideal de consulta.|No primeiro uso, um usuário que tenha credenciais administrativas do sistema deve inicializar o aplicativo. Após a inicialização, os usuários do dbo podem usar o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para ajustar somente as tabelas que eles possuem. Para obter mais informações, consulte "Inicializando o Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no primeiro uso" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
> [!IMPORTANT]  
>  Antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite a Autenticação do Windows para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verifique a configuração padrão exigida: se a conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é membro do grupo sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="Registry"></a> Permissões de Registro  
 O hive do registro é criado em **HKLM\Software\Microsoft\Microsoft SQL Server\\***<Instance_ID>* para componentes com reconhecimento de instância. Por exemplo  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL13.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSASSQL13.MyInstance**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL.130**  
  
 O registro também mantém um mapeamento do ID da instância para o nome da instância. O mapeamento do ID da instância para o nome da instância é mantido como segue:  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\SQL] "InstanceName"="MSSQL13"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\OLAP] "InstanceName"="MSASSQL13"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\RS] "InstanceName"="MSRSSQL13"**  
  
###  <a name="WMI"></a> WMI  

O WMI (Instrumentação de Gerenciamento do Windows) deve poder se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para dar suporte a isso, o SID por serviço do provedor WMI do Windows (**NT SERVICE\winmgmt**) é provisionado no [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 O provedor WMI do SQL requer as seguintes permissões:  
  
-   Associação nas funções de banco de dados fixas **db_ddladmin** ou **db_owner** no banco de dados msdb.  
  
-   Permissão**CREATE DDL EVENT NOTIFICATION** no servidor.  
  
-   Permissão**CREATE TRACE EVENT NOTIFICATION** no [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Permissão**VIEW ANY DATABASE** no nível do servidor.  
  
     A instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um namespace do WMI do SQL e concede permissão de leitura ao SID do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
###  <a name="Pipes"></a> Pipes nomeados  

Em toda a instalação, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece acesso ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] via protocolo de memória compartilhada, que é um pipe nomeado local.  
  
##  <a name="Provisioning"></a> Provisionamento  
 Esta seção descreve como as contas são provisionadas em vários componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Provisionamento do Mecanismo de Banco de Dados](#DE_Prov)  
  
    -   [Entidades de segurança do Windows](#Win_Principals)  
  
    -   [Conta sa](#sa)  
  
    -   [Logon e privilégios de SID por serviço do SQL Server](#Logins)  
  
    -   [Logon e privilégios do SQL Server Agent](#Agent)  
  
    -   [HADRON, privilégios e instância de cluster de failover do SQL](#Hadron)  
  
    -   [Gravador e privilégios do SQL](#Writer)  
  
    -   [WMI e privilégios do SQL](#SQLWMI)  
  
-   [Provisionamento SSAS](#SSAS)  
  
-   [Provisionamento SSRS](#SSRS)  
  
###  <a name="DE_Prov"></a> Provisionamento do Mecanismo de Banco de Dados  
 As contas a seguir são adicionadas como logons ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Win_Principals"></a> Entidades de segurança do Windows  
 Durante a instalação, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer que pelo menos uma conta de usuário seja nomeada como membro da função de servidor fixa **sysadmin** .  
  
####  <a name="sa"></a> Conta sa  
 A conta **sa** está sempre presente como um logon do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e é membro da função de servidor fixa **sysadmin** . Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] é instalado usando somente a Autenticação do Windows (ou seja, quando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está habilitada), o logon de **sa** ainda está presente, mas desabilitado. Para obter informações sobre como habilitar a conta **sa** , consulte [Alterar modo de autenticação do servidor](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
####  <a name="Logins"></a> Logon e privilégios de SID por serviço do SQL Server  
 O SID por serviço do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é provisionado como um logon do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O logon do SID por serviço é membro da função de servidor fixa **sysadmin** .  
  
####  <a name="Agent"></a> Logon e privilégios do SQL Server Agent  
 O SID por serviço do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é provisionado como um logon do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O logon do SID por serviço é membro da função de servidor fixa **sysadmin** .  
  
####  <a name="Hadron"></a> [!INCLUDE[ssHADRc](../../includes/sshadrc-md.md)] e privilégios e instância de cluster de failover do SQL  
 Ao instalar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] como um [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] ou SQL FCI (Instância de Cluster de Failover do SQL), **LOCAL SYSTEM** é provisionado no [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O logon de **LOCAL SYSTEM** recebe a permissão **ALTER ANY AVAILABILITY GROUP** (para o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]) e a permissão **VIEW SERVER STATE** (para o SQL FCI).  
  
####  <a name="Writer"></a> Gravador e privilégios do SQL  
 O SID por serviço do serviço Gravador VSS do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é provisionado como um logon do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O logon do SID por serviço é membro da função de servidor fixa **sysadmin** .  
  
####  <a name="SQLWMI"></a> WMI e privilégios do SQL  
 A instalação do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provisiona a conta **NT SERVICE\Winmgmt** como um [!INCLUDE[ssDE](../../includes/ssde-md.md)] logon e a adiciona à função de servidor fixa **sysadmin** .  
  
#### <a name="ssrs-provisioning"></a>Provisionamento SSRS  
 A conta especificada durante a instalação é provisionada como membro da função de banco de dados **RSExecRole** . Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
###  <a name="SSAS"></a> Provisionamento SSAS  
 Os requisitos da conta do serviço[!INCLUDE[ssAS](../../includes/ssas-md.md)] variam, dependendo de como o servidor está implantado. Se você estiver instalando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer a configuração do serviço [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para a execução em uma conta de domínio. Contas de domínio são necessárias para dar suporte ao recurso de conta gerenciada criada no SharePoint. Por essa razão, a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece uma conta de serviço padrão, como uma conta virtual, para uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obter mais informações sobre o provisionamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, consulte [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md).  
  
 Para todas as outras instalações autônomas do [!INCLUDE[ssAS](../../includes/ssas-md.md)] , você pode provisionar o serviço para ser executado em uma conta de domínio, conta de sistema interna, conta gerenciada ou conta virtual. Para obter mais informações sobre o provisionamento de conta, consulte [Configurar contas de serviço &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
 Para instalações clusterizadas, especifique uma conta de domínio ou uma conta de sistema interna. Não há suporte para contas gerenciadas nem contas virtuais em clusters de failover do [!INCLUDE[ssAS](../../includes/ssas-md.md)] .  
  
 Todas as instalações do [!INCLUDE[ssAS](../../includes/ssas-md.md)] requerem que você especifique um administrador do sistema da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . São provisionados privilégios de administrador na função **Servidor** do Analysis Services.  
  
###  <a name="SSRS"></a> Provisionamento SSRS  
 A conta especificada durante a instalação é provisionada no [!INCLUDE[ssDE](../../includes/ssde-md.md)] como membro da função de banco de dados **RSExecRole** . Para obter mais informações, veja [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
##  <a name="Upgrade"></a> Atualização de versões anteriores  
 Esta seção descreve as alterações feitas durante a atualização de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requer o [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 SP1, o Windows Server 2012, o Windows 8.0, o Windows Server 2012 R2 ou o Windows 8.1. Qualquer versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada em uma versão inferior do sistema operacional deve ter o sistema operacional atualizado antes de atualizar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Durante a atualização do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do modo a seguir.  
  
    -   O [!INCLUDE[ssDE](../../includes/ssde-md.md)] é executado com o contexto de segurança do SID por serviço. O SID por serviço recebe acesso às pastas de arquivos da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como DATA) e às chaves do Registro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   O SID por serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é provisionado no [!INCLUDE[ssDE](../../includes/ssde-md.md)] como membro da função de servidor fixa **sysadmin** .  
  
    -   Os SIDs por serviço são adicionados aos grupos locais do Windows do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja uma Instância de Cluster de Failover.  
  
    -   Os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecem provisionados nos grupos locais do Windows do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   O grupo Windows local para serviços é renomeado de **SQLServer2005MSSQLUser$***<computer_name>***$***<instance_name>* para **SQLServerMSSQLUser$***<computer_name>***$***<instance_name>*. Os locais de arquivos de bancos de dados migrados terão ACEs (Entradas de Controle de Acesso) para os grupos locais do Windows. Os locais de arquivos dos novos bancos de dados terão ACEs para o SID por serviço.  
  
-   Durante a atualização do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preserva as ACEs para o SID por serviço do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .  
  
-   Para uma Instância de Cluster de Failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a ACE da conta de domínio configurada para o serviço será retida.  
  
##  <a name="Appendix"></a> Apêndice  
 Esta seção contém informações adicionais sobre os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Descrição de contas de serviço](#Serv_Accts)  
  
-   [Identificando serviços com e sem reconhecimento de instância](#Identify_instance_aware_and_unaware)  
  
-   [Nomes de serviços localizados](#Localized_service_names)  
  
###  <a name="Serv_Accts"></a> Descrição de contas de serviço  
 A conta de serviço é a conta usada para iniciar um serviço do Windows, como o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Any_OS"></a> Contas disponíveis com qualquer sistema operacional  
 Além da nova [MSA](#MSA) e das [contas virtuais](#VA_Desc) descritas anteriormente, as contas a seguir podem ser usadas.  
  
 <a name="Domain_User"></a> **Conta de usuário de domínio**  
  
 Se o serviço precisar interagir com os serviços de rede, acessar recursos de domínio, como os compartilhamentos de arquivos, ou usar conexões de servidor vinculado com outros computadores que estejam executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá usar uma conta de domínio com privilégios mínimos. Muitas atividades de servidor a servidor podem ser executadas somente com uma conta de usuário do domínio. Essa conta deve ser pré-criada pela administração do domínio do ambiente.  
  
> [!NOTE]  
>  Se você configurar o aplicativo para usar uma conta de domínio, poderá isolar os privilégios para o aplicativo, mas deverá gerenciar senhas manualmente ou criar uma solução personalizada para gerenciar essas senhas. Muitos aplicativos para servidores usam essa estratégia para aprimorar a segurança, mas essa estratégia requer administração adicional e complexidade. Nessas implantações, os administradores de serviço gastam um tempo considerável em tarefas de manutenção, como o gerenciamento de senhas de serviço e SPNs, que são necessários para a autenticação Kerberos. Além disso, essas tarefas de manutenção podem interromper serviço.  
  
 <a name="Local_User"></a> **Local User Accounts**  
  
 Se o computador não fizer parte de um domínio, é recomendável usar uma conta de usuário local sem permissões de administrador do Windows.  
  
 <a name="Local_Service"></a> **Conta de serviço local**  
  
 A conta Serviço Local é uma conta interna que tem o mesmo nível de acesso a recursos e objetos que os membros do grupo Usuários. Esse acesso limitado ajuda a salvaguardar o sistema se serviços ou processos individuais forem comprometidos. Os serviços que são executados como a conta Serviço Local acessam os recursos de rede em uma sessão nula, sem credenciais. Lembre-se de que a conta de Serviço Local não tem suporte no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O Serviço Local não tem suporte como a conta que executa esses serviços porque é um serviço compartilhado e qualquer outro serviço que é executado sob o serviço local teria acesso de administrador do sistema ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome real da conta é **NT AUTHORITY\LOCAL SERVICE**.  
  
 <a name="Network_Service"></a> **Conta de serviço de rede**  
  
 A conta de Serviço de Rede é uma conta interna que tem mais acesso a recursos e objetos do que os membros do grupo Usuários. Os serviços executados como a conta de Serviço de Rede acessam recursos de rede usando as credenciais da conta do computador no formato *<domain_name>***\\***<computer_name>***$**. O nome real da conta é **NT AUTHORITY\NETWORK SERVICE**.  
  
<a name="Local_System"></a> **Conta de sistema local**  
  
 A conta Sistema Local é uma conta interna com privilégios altos. Ela tem privilégios extensos no sistema local e funciona como o computador na rede. O nome real da conta é **NT AUTHORITY\SYSTEM**.  
  
###  <a name="Identify_instance_aware_and_unaware"></a> Identificando serviços com e sem reconhecimento de instância  
 Os serviços com reconhecimento de instância são associados a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e têm suas próprias ramificações de registro. Você pode instalar várias cópias de serviços com reconhecimento de instância, executando a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada componente ou serviço. Os serviços sem reconhecimento de instância são compartilhados entre todas as instâncias instaladas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Eles não são associados a uma instância específica, são instalados uma só vez e não podem ser instalados lado a lado.  
  
 Os serviços com reconhecimento de instância no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluem o seguinte:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
     Esteja ciente de que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é desabilitado em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] com Advanced Services.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]*  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Pesquisa de texto completo  
  
 Os serviços sem reconhecimento de instância no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluem o seguinte:  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Navegador  
  
-   Gravador do SQL  
  
 *O Analysis Services no modo integrado do SharePoint é executado como '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]' como uma instância única, nomeada. O nome da instância é fixo. Não é possível especificar um nome diferente. Você pode instalar apenas uma instância do Analysis Services executada como '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]' em cada servidor físico.  
  
###  <a name="Localized_service_names"></a> Nomes de serviços localizados  
 A tabela a seguir mostra nomes de serviços que são exibidos por versões localizadas do Windows.  
  
|Linguagem|Nome do serviço local|Nome do serviço de rede|Nome do sistema local|Nome do grupo Admin.|  
|--------------|----------------------------|------------------------------|---------------------------|--------------------------|  
|Inglês<br /><br /> Chinês simplificado<br /><br /> Chinês tradicional<br /><br /> Coreano<br /><br /> Japonês|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|Alemão|NT-AUTORITÄT\LOKALER DIENST|NT-AUTORITÄT\NETZWERKDIENST|NT-AUTORITÄT\SYSTEM|VORDEFINIERT\Administratoren|  
|Francês|AUTORITE NT\SERVICE LOCAL|AUTORITE NT\SERVICE RÉSEAU|AUTORITE NT\SYSTEM|BUILTIN\Administradores|  
|Italiano|NT AUTHORITY\SERVIZIO LOCALE|NT AUTHORITY\SERVIZIO DI RETE|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|Espanhol|NT AUTHORITY\SERVICIO LOC|NT AUTHORITY\SERVICIO DE RED|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|Russo|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Администраторы|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
 [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
