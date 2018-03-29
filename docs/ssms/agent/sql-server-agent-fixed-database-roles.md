---
title: Funções de banco de dados fixas do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, roles
- SQLAgentUserRole database role
- SQLAgentReaderRole database role
- multiple roles
- security [SQL Server Agent], fixed database roles
- fixed database roles [SQL Server]
- SQLAgentOperatorRole database role
ms.assetid: 719ce56b-d6b2-414a-88a8-f43b725ebc79
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: e0420ff4be2260855e1f15f9d1711df2a906ac0b
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="sql-server-agent-fixed-database-roles"></a>Funções de banco de dados fixas do SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tem as seguintes funções de banco de dados fixas do **msdb** , que propiciam aos administradores um melhor controle do acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. As funções, ordenadas do menor para o maior acesso privilegiado, são:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
Quando usuários que não são membros de uma dessas funções se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], o nó **SQL Server Agent** no Pesquisador de Objetos não fica visível. O usuário deve ser membro de uma dessas funções de banco de dados fixas ou membro da função de servidor fixo **sysadmin** para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Permissões das funções de banco de dados fixas do SQL Server Agent  
As permissões de função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent são concêntricas uma às outras: funções mais privilegiadas herdam as permissões de funções menos privilegiadas nos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent (inclusive alertas, operadores, tarefas, agendas e proxies). Por exemplo, se membros da função de menor privilégio **SQLAgentUserRole** ganharem acesso ao proxy_A, os membros das funções **SQLAgentReaderRole** e **SQLAgentOperatorRole** terão automaticamente acesso a esse proxy mesmo que o acesso ao proxy_A não lhes tenha sido explicitamente concedido. Isto pode ter implicações de segurança, discutidas nas seções sobre cada função, mais abaixo.  
  
### <a name="sqlagentuserrole-permissions"></a>Permissões de SQLAgentUserRole  
**SQLAgentUserRole** é a menos privilegiada das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Ela só tem permissões em operadores, trabalhos locais e agendas de trabalho. Membros de **SQLAgentUserRole** só têm permissões em trabalhos locais e agendas de trabalho que eles possuem. Não podem usar trabalhos multisservidor (trabalhos de servidor mestre e de destino), nem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem. Membros de**SQLAgentUserRole** podem exibir uma lista de proxies disponíveis apenas na caixa de diálogo **Propriedades da Etapa de Trabalho** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] é visível a membros de **SQLAgentUserRole**.  
  
> [!IMPORTANT]  
> Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**Agentdatabase**. Membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
A tabela a seguir resume as permissões de **SQLAgentUserRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais<br /><br />(apenas trabalhos possuídos)|Agendas de trabalho<br /><br />(apenas agendas possuídas)|Proxies|  
|----------|-------------|-----------------------------------|-------------------------------------------|-----------|  
|Criar/modificar/excluir|não|Sim<br /><br />Não pode alterar a propriedade do trabalho.|Sim|não|  
|Exibir lista (enumerar)|Sim<br /><br />Pode obter lista de operadores disponíveis para uso em **sp_notify_operator** e na caixa de diálogo **Propriedades do trabalho** do Management Studio.|Sim|Sim|Sim<br /><br />Lista de proxies disponível apenas na caixa de diálogo **Propriedades da Etapa de Trabalho** do Management Studio.|  
|Habilitar/desabilitar|não|Sim|Sim|Não aplicável|  
|Exibir propriedades|não|Sim|Sim|não|  
|Executar/interromper/iniciar|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|não<br /><br />Membros de **SQLAgentUserRole** devem ter permissão EXECUTE em **sp_purge_jobhistory** concedida explicitamente para poderem excluir históricos de trabalhos que possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Sim|Não aplicável|  
  
### <a name="sqlagentreaderrole-permissions"></a>Permissões de SQLAgentReaderRole  
A função**SQLAgentReaderRole** inclui todas as permissões de **SQLAgentUserRole** , mais permissões para exibir a lista de trabalhos multisservidor disponíveis, suas propriedades e seu histórico. Os membros desta função também podem exibir a lista de todos os trabalhos e agendas de trabalho disponíveis, bem como suas propriedades, e não apenas aqueles que possuem. Membros de**SQLAgentReaderRole** não podem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] é visível a membros de **SQLAgentReaderRole**.  
  
> [!IMPORTANT]  
> Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**Agentdatabase**. Membros de **SQLAgentReaderRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
A tabela a seguir resume as permissões de **SQLAgentReaderRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Criar/modificar/excluir|não|Sim (apenas trabalhos possuídos)<br /><br />Não pode alterar a propriedade do trabalho.|não|Sim (somente agendas possuídas)|não|  
|Exibir lista (enumerar)|Sim<br /><br />Pode obter lista de operadores disponíveis para uso em **sp_notify_operator** e na caixa de diálogo **Propriedades do trabalho** do Management Studio.|Sim|Sim|Sim|Sim<br /><br />Lista de proxies disponível apenas na caixa de diálogo **Propriedades da Etapa de Trabalho** do Management Studio.|  
|Habilitar/desabilitar|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|Não aplicável|  
|Exibir propriedades|não|Sim|Sim|Sim|não|  
|Editar propriedades|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Executar/interromper/iniciar|Não aplicável|Sim (apenas trabalhos possuídos)|não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|não<br /><br />Membros de **SQLAgentReaderRole** devem ter permissão EXECUTE em **sp_purge_jobhistory** concedida explicitamente para poderem excluir históricos de trabalhos que possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.|não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
### <a name="sqlagentoperatorrole-permissions"></a>Permissões de SQLAgentOperatorRole  
A função**SQLAgentOperatorRole** é a mais privilegiada das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Ela inclui todas as permissões de **SQLAgentUserRole** e **SQLAgentReaderRole**. Os membros desta função também podem exibir propriedades de operadores e proxies, bem como enumerar os proxies e alertas disponíveis no servidor.  
  
Membros de**SQLAgentOperatorRole** têm permissões adicionais em trabalhos locais e agendas. Podem executar, interromper ou iniciar todos os trabalhos locais, bem como excluir o histórico de trabalhos de qualquer trabalho local no servidor. Também podem habilitar ou desabilitar todos os trabalhos locais e agendas no servidor. Para habilitar ou desabilitar trabalhos locais ou agendas, os membros desta função devem usar os procedimentos armazenados **sp_update_job** e **sp_update_schedule**. Apenas os parâmetros que especificam o nome do trabalho ou da agenda ou o identificador e o parâmetro **@enabled** podem ser especificados por membros de **SQLAgentOperatorRole**. Se especificarem algum outro parâmetro, a execução desses procedimentos armazenados falhará. Membros de**SQLAgentOperatorRole** não podem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem.  
  
Os nós **Trabalhos**, **Alertas**, **Operadores**e **Proxies** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] são visíveis a membros de **SQLAgentOperatorRole**. Somente o nó **Logs de Erros** não é visível a membros desta função.  
  
> [!IMPORTANT]  
> Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**Agentdatabase**. Membros de **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole** e **SQLAgentReaderRole**. Isso significa que membros de **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent concedidos às funções **SQLAgentUserRole** ou **SQLAgentReaderRole** e podem utilizá-los.  
  
A tabela a seguir resume as permissões de **SQLAgentOperatorRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
|Ação|Alertas|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|----------|----------|-------------|--------------|--------------------|-----------------|-----------|  
|Criar/modificar/excluir|não|não|Sim (apenas trabalhos possuídos)<br /><br />Não pode alterar a propriedade do trabalho.|não|Sim (somente agendas possuídas)|não|  
|Exibir lista (enumerar)|Sim|Sim<br /><br />Pode obter lista de operadores disponíveis para uso em **sp_notify_operator** e na caixa de diálogo **Propriedades do trabalho** do Management Studio.|Sim|Sim|Sim|Sim|  
|Habilitar/desabilitar|não|não|Sim<br /><br />**SQLAgentOperatorRole** podem habilitar ou desabilitar trabalhos locais que não possuem, por meio do procedimento armazenado **sp_update_job** e especificando valores para os parâmetros **@enabled** e **@job_id** (ou **@job_name**). Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.|não|Sim<br /><br />**SQLAgentOperatorRole** podem habilitar ou desabilitar agendas que não possuem, por meio do procedimento armazenado **sp_update_schedule** e especificando valores para os parâmetros **@enabled** e **@schedule_id** (ou **@name**). Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.|Não aplicável|  
|Exibir propriedades|Sim|Sim|Sim|Sim|Sim|Sim|  
|Editar propriedades|não|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Executar/interromper/iniciar|Não aplicável|Não aplicável|Sim|não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não aplicável|Sim|não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
## <a name="assigning-users-multiple-roles"></a>Atribuindo várias funções aos usuários  
Membros da função de servidor fixa **sysadmin** têm acesso a toda a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Caso um usuário não seja membro da função **sysadmin** , mas seja membro de mais de uma função de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, é importante ter em mente o modelo de permissões concêntricas dessas funções. Como funções mais privilegiadas sempre detêm todas as permissões das funções menos privilegiadas, o usuário que for membro de mais de uma função terá, automaticamente, as permissões associadas à função mais privilegiada de que é membro.  
  
## <a name="see-also"></a>Consulte Também  
[Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
[sp_update_job (Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623)  
[sp_update_schedule (Transact-SQL)](http://msdn.microsoft.com/en-us/97b3119b-e43e-447a-bbfb-0b5499e2fefe)  
[sp_notify_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/c440f5c9-9884-4196-b07c-55d87afb17c3)  
[sp_purge_jobhistory (Transact-SQL)](http://msdn.microsoft.com/en-us/237f9bad-636d-4262-9bfb-66c034a43e88)  
  
