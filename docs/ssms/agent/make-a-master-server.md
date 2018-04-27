---
title: Criar um servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5ae94b15a4396fe86941476866038fd1493a8643
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como criar um servidor mestre do [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para criar um servidor mestre, usando:**  
  
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
  
#### <a name="to-make-a-master-server"></a>Para criar um servidor mestre  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda essa instância.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Tornar este um mestre**. O **Assistente de Servidor Mestre** o guiará no processo de criação de um servidor mestre e de adição de servidores de destino.  
  
3.  Na página **Operador de Servidor Mestre** , configure um operador para o servidor mestre. Para enviar notificações a operadores usando email ou pagers, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve estar configurado para enviar email. Para enviar notificações aos operadores usando **net send**, o serviço Messenger deve estar sendo executado no servidor no qual está o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
    **Endereço de email**  
    Define o endereço de email para o operador.  
  
    **Endereço de pager**  
    Define o endereço de email de pager para o operador.  
  
    **Endereço de net send**  
    Define o endereço de **net send** para o operador.  
  
4.  Na página **Servidor de Destino** , selecione servidores de destino para o servidor mestre.  
  
    **Servidores Registrados**  
    Lista os servidores registrados no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] que já não são servidores de destino.  
  
    **Servidores de Destino**  
    Lista os servidores que são servidores de destino.  
  
    **>**  
    Mova o servidor selecionado para a lista de servidor de destino.  
  
    **>>**  
    Mova todos os servidores para a lista de servidor de destino.  
  
    **<**  
    Remova o servidor selecionado da lista de servidor de destino.  
  
    **<<**  
    Remova todos os servidores da lista de servidor de destino.  
  
    **Adicionar Conexão**  
    Adicione um servidor à lista de servidor de destino sem registrar o servidor.  
  
    **Conexão**  
    Altere as propriedades de conexão para o servidor selecionado.  
  
5.  Na página **Credenciais de logon de servidor mestre** , para especificar se você deseja criar um novo logon para o servidor de destino e atribuir-lhe direitos ao servidor mestre.  
  
    **Criar um novo logon, se necessário, e atribuir-lhe direitos ao MSX**  
    Cria um novo logon no servidor de destino se o logon especificado ainda não existir.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>Para criar um servidor mestre  
  
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
[Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md)  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
