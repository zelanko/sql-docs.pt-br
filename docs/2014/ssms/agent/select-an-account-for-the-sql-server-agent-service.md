---
title: Selecionar uma conta para o Serviço do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b2fd7a22c202b1210b17f86903fce32ec8d4b5b
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68811085"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>Selecionar uma conta para o Serviço do SQL Server Agent
  A conta de inicialização do serviço define a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado, bem como suas permissões de rede. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado como uma conta de usuário especificada. Selecione uma conta para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no qual estão disponíveis as seguintes opções:  
  
-   **Conta interna**. Em uma lista, você pode escolher uma das seguintes contas de serviço Windows internas:  
  
    -   Conta**Sistema Local** . O nome desta conta é NT AUTHORITY\System. É uma conta poderosa, com acesso irrestrito a todos os recursos do sistema local. Ela é membro do grupo **Administradores** do Windows no computador local e, portanto, é membro da função de servidor fixa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin**  
  
        > [!IMPORTANT]  
        >  A opção **conta Sistema Local** é fornecida apenas por questão de compatibilidade retroativa. A conta Sistema Local tem permissões de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não necessita. Evite executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent como a conta Sistema Local. Para maior segurança, use uma conta de domínio do Windows com as permissões listadas na seção "Permissões de contas de domínio do Windows", a seguir.  
  
-   **Esta conta**. Permite-lhe especificar a conta de domínio do Windows na qual deve ser executado o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Recomendamos escolher uma conta de usuário do Windows que não seja membro do grupo **Administradores** do Windows. Porém, há limitações ao uso de administração multisservidor quando a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não é membro do grupo **Administradores** local. Para obter mais informações, consulte 'Tipos de conta de serviço com suporte' a seguir neste tópico.  
  
## <a name="windows-domain-account-permissions"></a>Permissões de contas de domínio do Windows  
 Para maior segurança, selecione **Esta conta**, que especifica uma conta de domínio do Windows. A conta de domínio do Windows que você especificar deve ter as seguintes permissões:  
  
-   Em todas as versões do Windows, permissão para efetuar logon como um serviço (SeServiceLogonRight)  
  
> [!NOTE]  
>  A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve fazer parte do grupo Acesso Compatível Pré-Windows 2000 no controlador de domínio; caso contrário, os trabalhos de propriedade de usuários do domínio que não sejam membros do grupo Administradores do Windows falharão.  
  
-   Em servidores Windows, a conta em que o Serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado requer as permissões a seguir para poder dar suporte a proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
    -   Permissão para ignorar verificação completa (SeChangeNotifyPrivilege)  
  
    -   Permissão para substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
    -   Permissão para ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
    -   Permissão para efetuar logon usando o tipo de logon em lote (SeBatchLogonRight)  
  
> [!NOTE]  
>  Se a conta não tiver as permissões necessárias para dar suporte a proxies, apenas membros da função de servidor fixa **sysadmin** poderão criar trabalhos.  
  
> [!NOTE]  
>  Para receber notificação de alertas do WMI, a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve deter permissão para o namespace que contém os eventos do WMI e ALTER ANY EVENT NOTIFICATION.  
  
## <a name="sql-server-role-membership"></a>Associação a funções do SQL Server  
 A conta em cujo nome é executado o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser membro das seguintes funções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   A conta deve ser membro da função de servidor fixa **sysadmin** .  
  
-   Para usar o processamento de trabalhos multisservidor, a conta deve ser membro da função de banco de dados **TargetServersRole** do **msdb** no servidor mestre.  
  
## <a name="supported-service-account-types"></a>Tipos de conta de serviço com suporte  
 A tabela a seguir lista os tipos de conta do Windows que podem ser usadas para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Tipo de conta de serviço|Servidor não clusterizado|Servidor em cluster|Controlador de domínio (não clusterizado)|  
|--------------------------|---------------------------|----------------------|------------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Conta de domínio do Windows (membro do grupo Administradores do Windows)|Tem suporte|Tem suporte|Tem suporte|  
|Conta de domínio do Windows (não administrativa)|Com suporte<sup>1</sup>|Com suporte<sup>1</sup>|Com suporte<sup>1</sup>|  
|Conta de Serviço de Rede (NT AUTHORITY\NetworkService)|Com suporte<sup>1, 3, 4</sup>|Sem suporte|Sem suporte|  
|Conta de usuário local (não administrativa)|Com suporte<sup>1</sup>|Sem suporte|Não aplicável|  
|Conta Sistema Local (NT AUTHORITY\System)|Com suporte<sup>2</sup>|Sem suporte|Com suporte<sup>2</sup>|  
|Conta do Serviço Local (NT AUTHORITY\LocalService)|Sem suporte|Sem suporte|Sem suporte|  
  
 <sup>1</sup> consulte a limitação 1 abaixo.  
  
 <sup>2</sup> consulte a limitação 2 abaixo.  
  
 <sup>3</sup> consulte a limitação 3 abaixo.  
  
 <sup>4</sup> consulte a limitação 4 abaixo.  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>Limitação 1: usar contas não administrativas para administração multisservidor  
 A inscrição de servidores de destino para um servidor mestre pode falhar com a seguinte mensagem de erro: "Falha na operação de inscrição".  
  
 Para resolver esse erro, reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Iniciar, parar, pausar, retomar e reiniciar os serviços SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>Limitação 2: usar a conta Sistema Local para administração multisservidor  
 Quando o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado com a conta Sistema Local, só haverá suporte para administração multisservidor se o servidor mestre e o servidor de destino residirem no mesmo computador. Se você usar essa configuração, será retornada a seguinte mensagem quando você inscrever servidores de destino para o servidor mestre:  
  
 "Verifique se a conta de inicialização de agente de *<target_server_computer_name>* tem direitos para fazer logon como um servidor de destino".  
  
 Você pode ignorar essa mensagem informativa. A operação de inscrição deve ser concluída com êxito. Para obter mais informações, veja [Criar um ambiente multisservidor](create-a-multiserver-environment.md).  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>Limitação 3: usar a conta de Serviço de Rede, quando ela é um usuário do SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent poderá não conseguir iniciar se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com a conta de Serviço de Rede e esta tiver recebido acesso explicitamente para fazer logon em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para resolver isso, reinicialize o computador em que está sendo executado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isso só precisa ser feito uma vez.  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>Limitação 4: usar a conta de Serviço de Rede quando o SQL Server Reporting Services é executado no mesmo computador  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent poderá não conseguir iniciar se você executar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com a conta do Serviço de Rede e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também estiver em execução no mesmo computador.  
  
 Para resolver isso, reinicie o computador em que está sendo executado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, reinicialize os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Isso só precisa ser feito uma vez.  
  
## <a name="common-tasks"></a>Tarefas comuns  
 **Para especificar a conta de inicialização do serviço do SQL Server Agent**  
  
-   [Definir a conta de inicialização de serviço para o SQL Server Agent &#40;SQL Server Configuration Manager&#41;](set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
 **Para especificar o perfil de email do SQL Server Agent**  
  
-   [Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
> [!NOTE]  
>  Use o Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser iniciado quando o sistema operacional for iniciado.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Tópicos de instruções sobre gerenciamento de serviços &#40;SQL Server Configuration Manager&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)   
 [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md)  
  
  
