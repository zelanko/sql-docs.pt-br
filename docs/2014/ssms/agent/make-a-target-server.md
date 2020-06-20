---
title: Criar um servidor de destino | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: bd60a19234d186bb0912978589fa60fd8e8a8c22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008658"
---
# <a name="make-a-target-server"></a>Criar um servidor de destino
  Este tópico descreve como criar um servidor de destino no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], ou SQL Server Management Objects (SMO).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar um servidor de destino, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Trabalhos distribuídos que possuem etapas associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Certifique-se de que as seguintes condições sejam atendidas, ou as etapas de trabalho associadas a um proxy não serão baixadas do servidor mestre para o destino:  
  
-   A subchave do registro do servidor mestre **\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server \\ < *instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) é definida como 1 (true). Por padrão, essa subchave encontra-se definida como 0 (falso).  
  
-   Existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
 Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre para o servidor de destino, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino."  
  
     Para resolver este erro, defina a subchave **AllowDownloadedJobsToMatchProxyName** do Registro como 1.  
  
-   "Proxy não localizado."  
  
     Para resolver este erro, certifique-se de que existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 As permissões para executar esse procedimento para membros da função de servidor fixa `sysadmin`.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-make-a-target-server"></a>Para criar um servidor de destino  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Tornar este de destino**. O **Assistente de Servidor de Destino** o guiará no processo de criação de um servidor de destino.  
  
3.  Na página **Selecione um Servidor Mestre** , selecione o servidor mestre do qual esse servidor de destino receberá trabalhos.  
  
     **Escolher Servidor**  
     Conecte-se ao servidor mestre.  
  
     **Descrição deste Servidor**  
     Digite uma descrição para esse servidor de destino. O servidor de destino carrega essa descrição no servidor mestre.  
  
4.  Na página **Credenciais de logon de servidor mestre** , crie um logon novo no servidor de destino, se necessário.  
  
     **Criar um novo logon, se necessário, e atribuir-lhe direitos ao MSX**  
     Cria um novo logon no servidor de destino se o logon especificado ainda não existir.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-make-a-target-server"></a>Para criar um servidor de destino  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo inscreve o servidor atual no servidor mestre AdventureWorks1. O local do servidor atual é Prédio 21, Sala 309, Rack 5.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     Para obter mais informações, consulte [sp_msx_enlist &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
##  <a name="using-sql-server-management-objects-smo"></a><a name="PowerShellProcedure"></a>Usando o SQL Server Management Objects (SMO)  
  
## <a name="see-also"></a>Consulte Também  
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)  
