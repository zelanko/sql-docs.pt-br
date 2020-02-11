---
title: Funções de banco de dados fixas do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a8067aaa2133648c1a1ea4fff81db08c139d5278
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67793399"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Funções de banco de dados fixas do SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tem as seguintes funções de banco de dados fixas do **msdb** , que oferecem aos administradores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um melhor controle sobre o acesso ao Agent. As funções, ordenadas do menor para o maior acesso privilegiado, são:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Quando usuários que não são membros de uma dessas funções se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o nó **SQL Server Agent** no Pesquisador de Objetos não fica visível. O usuário deve ser membro de uma dessas funções de banco de dados fixas ou membro da função de servidor fixo **sysadmin** para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Permissões das funções de banco de dados fixas do SQL Server Agent  
 As permissões de função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são concêntricas uma às outras: funções mais privilegiadas herdam as permissões de funções menos privilegiadas nos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (inclusive alertas, operadores, tarefas, agendas e proxies). Por exemplo, se membros da função de menor privilégio **SQLAgentUserRole** ganharem acesso ao proxy_A, os membros das funções **SQLAgentReaderRole** e **SQLAgentOperatorRole** terão automaticamente acesso a esse proxy mesmo que o acesso ao proxy_A não lhes tenha sido explicitamente concedido. Isto pode ter implicações de segurança, discutidas nas seções sobre cada função, mais abaixo.  
  
### <a name="sqlagentuserrole-permissions"></a>Permissões de SQLAgentUserRole  
 **SQLAgentUserRole** é o menos privilegiado das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de banco de dados fixas do agente. Ela só tem permissões em operadores, trabalhos locais e agendas de trabalho. Membros de **SQLAgentUserRole** só têm permissões em trabalhos locais e agendas de trabalho que eles possuem. Não podem usar trabalhos multisservidor (trabalhos de servidor mestre e de destino), nem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem. Os membros do **SQLAgentUserRole** podem exibir uma lista de proxies disponíveis somente na caixa de diálogo Propriedades da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]etapa de **trabalho** do. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é visível a membros de **SQLAgentUserRole**.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a **membros do**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentUserRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais<br /><br /> (apenas trabalhos possuídos)|Agendas de trabalho<br /><br /> (apenas agendas possuídas)|Proxies|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|Criar/modificar/excluir|Não|Sim <sup>1</sup>|Sim|Não|  
|Exibir lista (enumerar)|Sim <sup>2</sup>|Sim|Sim|Sim <sup>3</sup>|  
|Habilitar/desabilitar|Não|Sim|Sim|Não aplicável|  
|Exibir propriedades|Não|Sim|Sim|Não|  
|Executar/interromper/iniciar|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não <sup>4</sup>|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Sim|Não aplicável|  
  
 <sup>1</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>2</sup> pode obter a lista de operadores disponíveis para uso no **sp_notify_operator** e na caixa de diálogo **Propriedades do trabalho** de Management Studio.  
  
 <sup>3</sup> a lista de proxies só está disponível na caixa de diálogo **Propriedades da etapa de trabalho** do Management Studio.  
  
 <sup>4</sup> os membros de **SQLAgentUserRole** devem receber explicitamente a permissão EXECUTE em **sp_purge_jobhistory** para excluir o histórico de trabalho nos trabalhos que eles possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.  
  
### <a name="sqlagentreaderrole-permissions"></a>Permissões de SQLAgentReaderRole  
 O **SQLAgentReaderRole** inclui todas as permissões de **SQLAgentUserRole** , bem como permissões para exibir a lista de trabalhos multisservidor disponíveis, suas propriedades e seu histórico. Os membros desta função também podem exibir a lista de todos os trabalhos e agendas de trabalho disponíveis, bem como suas propriedades, e não apenas aqueles que possuem. Os membros do **SQLAgentReaderRole** não podem alterar a propriedade do trabalho para obter acesso aos trabalhos que ainda não possuem. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é visível a membros de **SQLAgentReaderRole**.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a **membros do**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Membros de **SQLAgentReaderRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentReaderRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Criar/modificar/excluir|Não|Sim <sup>1</sup> (somente trabalhos de propriedade)|Não|Sim (somente agendas possuídas)|Não|  
|Exibir lista (enumerar)|Sim <sup>2</sup>|Sim|Sim|Sim|Sim <sup>3</sup>|  
|Habilitar/desabilitar|Não|Sim (apenas trabalhos possuídos)|Não|Sim (somente agendas possuídas)|Não aplicável|  
|Exibir propriedades|Não|Sim|Sim|Sim|Não|  
|Editar propriedades|Não|Sim (apenas trabalhos possuídos)|Não|Sim (somente agendas possuídas)|Não|  
|Executar/interromper/iniciar|Não aplicável|Sim (apenas trabalhos possuídos)|Não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não <sup>4</sup>|Não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
 <sup>1</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>2</sup> pode obter a lista de operadores disponíveis para uso no **sp_notify_operator** e na caixa de diálogo **Propriedades do trabalho** de Management Studio.  
  
 <sup>3</sup> a lista de proxies só está disponível na caixa de diálogo **Propriedades da etapa de trabalho** do Management Studio.  
  
 <sup>4</sup> os membros de **SQLAgentReaderRole** devem receber explicitamente a permissão EXECUTE em **sp_purge_jobhistory** para excluir o histórico de trabalho nos trabalhos que eles possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.  
  
### <a name="sqlagentoperatorrole-permissions"></a>Permissões de SQLAgentOperatorRole  
 **SQLAgentOperatorRole** é a mais privilegiada das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funções de banco de dados fixas do agente. Ela inclui todas as permissões de **SQLAgentUserRole** e **SQLAgentReaderRole**. Os membros desta função também podem exibir propriedades de operadores e proxies, bem como enumerar os proxies e alertas disponíveis no servidor.  
  
 Os membros do **SQLAgentOperatorRole** têm permissões adicionais em trabalhos locais e agendas. Podem executar, interromper ou iniciar todos os trabalhos locais, bem como excluir o histórico de trabalhos de qualquer trabalho local no servidor. Também podem habilitar ou desabilitar todos os trabalhos locais e agendas no servidor. Para habilitar ou desabilitar trabalhos locais ou agendas, os membros desta função devem usar os procedimentos armazenados **sp_update_job** e **sp_update_schedule**. Somente os parâmetros que especificam o nome do trabalho ou da agenda ou ** \@** o identificador e o parâmetro habilitado podem ser especificados por membros de **SQLAgentOperatorRole**. Se especificarem algum outro parâmetro, a execução desses procedimentos armazenados falhará. Os membros do **SQLAgentOperatorRole** não podem alterar a propriedade do trabalho para obter acesso aos trabalhos que ainda não possuem.  
  
 Os nós **Trabalhos**, **Alertas**, **Operadores**e **Proxies** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são visíveis a membros de **SQLAgentOperatorRole**. Somente o nó **Logs de Erros** não é visível a membros desta função.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a **membros do**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabaseroles**. Membros de **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole** e **SQLAgentReaderRole**. Isso significa que membros de **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos às funções **SQLAgentUserRole** ou **SQLAgentReaderRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentOperatorRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Alertas|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Criar/modificar/excluir|Não|Não|Sim <sup>2</sup> (somente trabalhos de propriedade)|Não|Sim (somente agendas possuídas)|Não|  
|Exibir lista (enumerar)|Sim|Sim <sup>1</sup>|Sim|Sim|Sim|Sim|  
|Habilitar/desabilitar|Não|Não|Sim <sup>3</sup>|Não|Sim <sup>4</sup>|Não aplicável|  
|Exibir propriedades|Sim|Sim|Sim|Sim|Sim|Sim|  
|Editar propriedades|Não|Não|Sim (apenas trabalhos possuídos)|Não|Sim (somente agendas possuídas)|Não|  
|Executar/interromper/iniciar|Não aplicável|Não aplicável|Sim|Não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não aplicável|Sim|Não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
 <sup>1</sup> pode obter a lista de operadores disponíveis para uso em **sp_notify_operator** e a caixa de diálogo **Propriedades do trabalho** de Management Studio.  
  
 <sup>2</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>3</sup> os membros do **SQLAgentOperatorRole** podem habilitar ou desabilitar trabalhos locais que não possuem, usando o procedimento armazenado **sp_update_job** e especificando valores para os ** \@parâmetros enabled** e ** \@job_id** (ou ** \@job_name**). Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.  
  
 <sup>4</sup> os membros do **SQLAgentOperatorRole** podem habilitar ou desabilitar agendas que não possuem, usando o procedimento armazenado **sp_update_schedule** e especificando valores ** \@** para os parâmetros enabled e ** \@schedule_id** (ou ** \@Name**). Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.  
  
## <a name="assigning-users-multiple-roles"></a>Atribuindo várias funções aos usuários  
 Membros da função de servidor fixa **sysadmin** têm acesso a toda a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso um usuário não seja membro da função **sysadmin** , mas seja membro de mais de uma função de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, é importante ter em mente o modelo de permissões concêntricas dessas funções. Como funções mais privilegiadas sempre detêm todas as permissões das funções menos privilegiadas, o usuário que for membro de mais de uma função terá, automaticamente, as permissões associadas à função mais privilegiada de que é membro.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar segurança de SQL Server Agent](implement-sql-server-agent-security.md)   
 [&#41;&#40;Transact-SQL de sp_update_job](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_update_schedule](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_notify_operator](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
