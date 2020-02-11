---
title: Criar um servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.msxwiz.complete.f1
- sql12.ag.msxwiz.target.f1
- sql12.ag.msxwiz.login.f1
- sql12.ag.msxwiz.cover.f1
- sql12.ag.msxwiz.operator.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca0e79c617db6cc2906ac9225efd92e156699951
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68189135"
---
# <a name="make-a-master-server"></a>Make a Master Server
  Este tópico descreve como criar um servidor mestre do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar um servidor mestre usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Trabalhos distribuídos que possuem etapas associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Certifique-se de que as seguintes condições sejam atendidas, ou as etapas de trabalho associadas a um proxy não serão baixadas do servidor mestre para o destino:  
  
-   A subchave do registro do servidor mestre **\\\<HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server*instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) é definida como 1 (true). Por padrão, essa subchave encontra-se definida como 0 (falso).  
  
-   Existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
 Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre para o servidor de destino, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino."  
  
     Para resolver este erro, defina a subchave **AllowDownloadedJobsToMatchProxyName** do Registro como 1.  
  
-   "Proxy não localizado."  
  
     Para resolver este erro, certifique-se de que existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
####  <a name="Permissions"></a> Permissões  
 As permissões para executar esse procedimento para membros da função de servidor fixa `sysadmin`.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-make-a-master-server"></a>Para criar um servidor mestre  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Tornar este um mestre**. O **Assistente de Servidor Mestre** o guiará no processo de criação de um servidor mestre e de adição de servidores de destino.  
  
3.  Na página **Operador de Servidor Mestre** , configure um operador para o servidor mestre. Para enviar notificações a operadores usando email ou pagers, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve estar configurado para enviar email. Para enviar notificações aos operadores usando **net send**, o serviço Messenger deve estar sendo executado no servidor no qual está o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
     **Endereço de email**  
     Define o endereço de email para o operador.  
  
     **Endereço do pager**  
     Define o endereço de email de pager para o operador.  
  
     **Endereço de net send**  
     Define o endereço de **net send** para o operador.  
  
4.  Na página **Servidor de Destino** , selecione servidores de destino para o servidor mestre.  
  
     **Servidores Registrados**  
     Lista os servidores registrados no Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] que já não são servidores de destino.  
  
     **Servidores de destino**  
     Lista os servidores que são servidores de destino.  
  
     **>**  
     Mova o servidor selecionado para a lista de servidor de destino.  
  
     **>>**  
     Mova todos os servidores para a lista de servidor de destino.  
  
     **<**  
     Remova o servidor selecionado da lista de servidor de destino.  
  
     **<<**  
     Remova todos os servidores da lista de servidor de destino.  
  
     **Adicionar conexão**  
     Adicione um servidor à lista de servidor de destino sem registrar o servidor.  
  
     **Conexão**  
     Altere as propriedades de conexão para o servidor selecionado.  
  
5.  Na página **Credenciais de logon de servidor mestre** , para especificar se você deseja criar um novo logon para o servidor de destino e atribuir-lhe direitos ao servidor mestre.  
  
     **Criar um novo logon, se necessário, e atribuir direitos de ti ao MSX**  
     Cria um novo logon no servidor de destino se o logon especificado ainda não existir.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>Para criar um servidor mestre  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo inscreve o servidor atual no servidor mestre AdventureWorks1. O local do servidor atual é Prédio 21, Sala 309, Rack 5.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
 Para obter mais informações, consulte [sp_msx_enlist &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um ambiente multisservidor](create-a-multiserver-environment.md)   
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)  
  
  
