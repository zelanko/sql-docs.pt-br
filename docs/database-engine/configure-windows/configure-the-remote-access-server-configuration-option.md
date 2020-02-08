---
title: Configurar a opção de configuração de servidor remote access | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], stored procedure execution
ms.assetid: f5de748d-1c55-4714-9661-38fe62e5095f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 52d6f73b585f3d0857186bef9c6c440e8655adc1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012346"
---
# <a name="configure-the-remote-access-server-configuration-option"></a>Configurar a opção remote access de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico é sobre o recurso "Acesso Remoto". Essa opção de configuração é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obscuro para o recurso de comunicação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que foi preterido e talvez você não deva usá-lo. Se você chegou a esta página porque está com problemas para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte um dos tópicos a seguir:  
  
-   [Tutorial: Introdução ao Mecanismo de Banco de Dados](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
-   [Fazendo o logon no SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
-   [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
-   [Conectar-se a um servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)  
  
-   [Conectar a qualquer componente do SQL Server a partir do SQL Server Management Studio](../../ssms/f1-help/connect-to-any-sql-server-component-from-sql-server-management-studio.md)  
  
-   [Conectar-se ao Mecanismo de Banco de Dados com sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)  
  
-   [Como solucionar problemas na conexão ao Mecanismo de Banco de Dados do SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
 Os tópicos a seguir podem interessar programadores:  
  
-   [Como conectar-se ao SQL Server usando a Autenticação do SQL no ASP.NET 2.0](https://msdn.microsoft.com/library/ff648340.aspx)  
  
-   [Conectando-se a uma instância do SQL Server](../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)  
  
-   [Como: criar conexões com bancos de dados do SQL Server](https://msdn.microsoft.com/library/s4yys16a.aspx)  
  
 **O corpo principal deste tópico começa aqui.**  
  
 Este tópico descreve como configurar a opção de configuração de servidor **remote access** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **remote access** controla a execução de procedimentos armazenados de servidores locais ou remotos nos quais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão sendo executadas. O valor padrão dessa opção é 1. Isso concede permissão para executar procedimentos armazenados locais de servidores remotos ou procedimentos armazenados remotos do servidor local. Para evitar que procedimentos armazenados locais sejam executados a partir de um servidor remoto ou que procedimentos armazenados remotos sejam executados no servidor local, defina a opção como 0.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Em vez disso, use [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção remote access, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção remote access](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A opção **remote access** se aplica apenas aos servidores que são adicionados usando [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)e está incluída para ter compatibilidade com versões anteriores.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-access-option"></a>Para configurar a opção remote access  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Conexões** .  
  
3.  Em **Conexões do servidor remoto**, marque ou desmarque a caixa de seleção **Permitir conexões remotas com este servidor** .  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-remote-access-option"></a>Para configurar a opção remote access  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `remote access` como `0`.  
  
```sql  
EXEC sp_configure 'remote access', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de configurar a opção remote access  
 Essa configuração não entrará em vigor até que você reinicie o SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
