---
title: Configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4cb77175ae38aafd80d6247eca3677aa26f0acda
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980149"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como configurar um usuário para criar ou executar trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para configurar um usuário para criar e gerenciar trabalhos do SQL Server Agent, usando:**  [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para configurar um usuário para criar ou executar trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, primeiro você deve adicionar um logon existente do SQL Server ou uma função do msdb a uma das seguintes funções de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no banco de dados msdb: SQLAgentUserRole, SQLAgentReaderRole ou SQLAgentOperatorRole.  
  
Por padrão, os membros dessas funções de banco de dados podem criar suas próprias etapas de trabalho, executadas como eles mesmos. Se esses usuários não administrativos quiserem executar trabalhos que executam outros tipos de etapa de trabalho (por exemplo, pacotes [!INCLUDE[ssIS](../../includes/ssis_md.md)] ), eles precisarão ter acesso a uma conta proxy. Todos os membros da função de servidor fixa sysadmin têm permissão para criar, modificar e excluir contas proxy. Para obter mais informações sobre as permissões associadas a essas funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
#### <a name="Permissions"></a>Permissões  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
**Para adicionar um logon de SQL ou função msdb a uma função de banco de dados fixa do SQL Server Agent**  
  
1.  No **Pesquisador de Objetos**, expanda um servidor.  
  
2.  Expanda **Segurança**e, em seguida, **Logons**.  
  
3.  Clique com o botão direito do mouse no logon que deseja adicionar a uma função de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent e selecione **Propriedades**.  
  
4.  Na página **Mapeamento de Usuário** da caixa de diálogo **Propriedades de Logon** , selecione a linha que contém **msdb**.  
  
5.  Em **Associação à função de banco de dados para: msdb**, selecione a função de banco de dados fixa apropriada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
**Para configurar uma conta proxy para criar e gerenciar etapas de trabalho do SQL Server Agent**  
  
1.  No **Pesquisador de Objetos**, expanda um servidor.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Proxies** e selecione **Novo Proxy**.  
  
4.  Na página **Geral** da caixa de diálogo **Nova Conta Proxy** , especifique o nome do proxy, o nome da credencial e a descrição do novo proxy. Observe que primeiramente você deve criar uma credencial para poder criar um proxy do SQL Server Agent. Para obter mais informações sobre como criar uma credencial, consulte [Como criar uma credencial (SQL Server Management Studio)](http://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586) e [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d).  
  
5.  Marque os subsistemas apropriados para esse proxy.  
  
6.  Na página **Entidades** , adicione ou remova logons ou funções para conceder ou remover acesso à conta proxy.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
