---
title: Criar um servidor de destino | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.tsxwiz.complete.f1
- sql13.ag.tsxwiz.cover.f1
- sql13.ag.tsxwiz.credentials.f1
- sql13.ag.tsxwiz.msx.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a7757802d802bddcac7b5738b20b2c66a73189f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="make-a-target-server"></a>Criar um servidor de destino
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como criar um servidor de destino no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o [!INCLUDE[tsql](../../includes/tsql_md.md)] ou SQL Server Management Objects (SMO).  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para criar um servidor de destino, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Trabalhos distribuídos que possuem etapas associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Certifique-se de que as seguintes condições sejam atendidas, ou as etapas de trabalho associadas a um proxy não serão baixadas do servidor mestre para o destino:  
  
-   A subchave do Registro do servidor mestre **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) é definida como 1 (verdadeiro). Por padrão, essa subchave encontra-se definida como 0 (falso).  
  
-   Existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre para o servidor de destino, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino."  
  
    Para resolver este erro, defina a subchave **AllowDownloadedJobsToMatchProxyName** do Registro como 1.  
  
-   "Proxy não localizado."  
  
    Para resolver este erro, certifique-se de que existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
#### <a name="Permissions"></a>Permissões  
As permissões para executar esse procedimento usam como padrão membros da função de servidor fixa **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>Para criar um servidor de destino  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda essa instância.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Tornar este de destino**. O **Assistente de Servidor de Destino** o guiará no processo de criação de um servidor de destino.  
  
3.  Na página **Selecione um Servidor Mestre** , selecione o servidor mestre do qual esse servidor de destino receberá trabalhos.  
  
    **Escolher Servidor**  
    Conecte-se ao servidor mestre.  
  
    **Descrição deste Servidor**  
    Digite uma descrição para esse servidor de destino. O servidor de destino carrega essa descrição no servidor mestre.  
  
4.  Na página **Credenciais de logon de servidor mestre** , crie um logon novo no servidor de destino, se necessário.  
  
    **Criar um novo logon, se necessário, e atribuir-lhe direitos ao MSX**  
    Cria um novo logon no servidor de destino se o logon especificado ainda não existir.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>Para criar um servidor de destino  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo inscreve o servidor atual no servidor mestre AdventureWorks1. O local do servidor atual é Prédio 21, Sala 309, Rack 5.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
    Para obter mais informações, veja [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
## <a name="see-also"></a>Consulte Também  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
