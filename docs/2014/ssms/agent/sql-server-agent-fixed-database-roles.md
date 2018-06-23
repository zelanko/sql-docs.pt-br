---
title: Funções de banco de dados fixas do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
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
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7890daf6c0ff4b77bbb8bb44e29d7921a58dd612
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117574"
---
# <a name="sql-server-agent-fixed-database-roles"></a>Funções de banco de dados fixas do SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem as seguintes funções de banco de dados fixas do **msdb** , que propiciam aos administradores um melhor controle do acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. As funções, ordenadas do menor para o maior acesso privilegiado, são:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Quando usuários que não são membros de uma dessas funções se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o nó **SQL Server Agent** no Pesquisador de Objetos não fica visível. O usuário deve ser membro de uma dessas funções de banco de dados fixas ou membro da função de servidor fixo **sysadmin** para usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="permissions-of-sql-server-agent-fixed-database-roles"></a>Permissões das funções de banco de dados fixas do SQL Server Agent  
 As permissões de função de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent são concêntricas uma às outras: funções mais privilegiadas herdam as permissões de funções menos privilegiadas nos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (inclusive alertas, operadores, tarefas, agendas e proxies). Por exemplo, se membros da função de menor privilégio **SQLAgentUserRole** ganharem acesso ao proxy_A, os membros das funções **SQLAgentReaderRole** e **SQLAgentOperatorRole** terão automaticamente acesso a esse proxy mesmo que o acesso ao proxy_A não lhes tenha sido explicitamente concedido. Isto pode ter implicações de segurança, discutidas nas seções sobre cada função, mais abaixo.  
  
### <a name="sqlagentuserrole-permissions"></a>Permissões de SQLAgentUserRole  
 **SQLAgentUserRole** é a menos privilegiada das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Ela só tem permissões em operadores, trabalhos locais e agendas de trabalho. Membros de **SQLAgentUserRole** só têm permissões em trabalhos locais e agendas de trabalho que eles possuem. Não podem usar trabalhos multisservidor (trabalhos de servidor mestre e de destino), nem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem. Membros de**SQLAgentUserRole** podem exibir uma lista de proxies disponíveis apenas na caixa de diálogo **Propriedades da Etapa de Trabalho** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é visível a membros de **SQLAgentUserRole**.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabase**. Membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** e **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentUserRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais<br /><br /> (apenas trabalhos possuídos)|Agendas de trabalho<br /><br /> (apenas agendas possuídas)|Proxies|  
|------------|---------------|----------------------------------------|------------------------------------------------|-------------|  
|Criar/modificar/excluir|não|Sim <sup>1</sup>|Sim|não|  
|Exibir lista (enumerar)|Sim <sup>2</sup>|Sim|Sim|Sim <sup>3</sup>|  
|Habilitar/desabilitar|não|Sim|Sim|Não aplicável|  
|Exibir propriedades|não|Sim|Sim|não|  
|Executar/interromper/iniciar|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não <sup>4</sup>|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Sim|Não aplicável|  
  
 <sup>1</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>2</sup> pode obter a lista de operadores disponíveis para uso em **sp_notify_operator** e **propriedades do trabalho** caixa de diálogo do Management Studio.  
  
 <sup>3</sup> lista de proxies disponíveis apenas no **propriedades da etapa de trabalho** caixa de diálogo do Management Studio.  
  
 <sup>4</sup> membros de **SQLAgentUserRole** deve ser concedida explicitamente a permissão EXECUTE em **sp_purge_jobhistory** excluir históricos de trabalhos que possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.  
  
### <a name="sqlagentreaderrole-permissions"></a>Permissões de SQLAgentReaderRole  
 A função**SQLAgentReaderRole** inclui todas as permissões de **SQLAgentUserRole** , mais permissões para exibir a lista de trabalhos multisservidor disponíveis, suas propriedades e seu histórico. Os membros desta função também podem exibir a lista de todos os trabalhos e agendas de trabalho disponíveis, bem como suas propriedades, e não apenas aqueles que possuem. Membros de**SQLAgentReaderRole** não podem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem. Somente o nó **Trabalhos** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é visível a membros de **SQLAgentReaderRole**.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabase**. Membros de **SQLAgentReaderRole** tornam-se, automaticamente, membros de **SQLAgentUserRole**. Isso significa que membros de **SQLAgentReaderRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos à função **SQLAgentUserRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentReaderRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Criar/modificar/excluir|não|Sim <sup>1</sup> (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Exibir lista (enumerar)|Sim <sup>2</sup>|Sim|Sim|Sim|Sim <sup>3</sup>|  
|Habilitar/desabilitar|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|Não aplicável|  
|Exibir propriedades|não|Sim|Sim|Sim|não|  
|Editar propriedades|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Executar/interromper/iniciar|Não aplicável|Sim (apenas trabalhos possuídos)|não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não <sup>4</sup>|não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
 <sup>1</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>2</sup> pode obter a lista de operadores disponíveis para uso em **sp_notify_operator** e **propriedades do trabalho** caixa de diálogo do Management Studio.  
  
 <sup>3</sup> lista de proxies disponíveis apenas no **propriedades da etapa de trabalho** caixa de diálogo do Management Studio.  
  
 <sup>4</sup> membros de **SQLAgentReaderRole** deve ser concedida explicitamente a permissão EXECUTE em **sp_purge_jobhistory** excluir históricos de trabalhos que possuem. Não podem excluir históricos de trabalho de nenhum outro trabalho.  
  
### <a name="sqlagentoperatorrole-permissions"></a>Permissões de SQLAgentOperatorRole  
 A função**SQLAgentOperatorRole** é a mais privilegiada das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Ela inclui todas as permissões de **SQLAgentUserRole** e **SQLAgentReaderRole**. Os membros desta função também podem exibir propriedades de operadores e proxies, bem como enumerar os proxies e alertas disponíveis no servidor.  
  
 Membros de**SQLAgentOperatorRole** têm permissões adicionais em trabalhos locais e agendas. Podem executar, interromper ou iniciar todos os trabalhos locais, bem como excluir o histórico de trabalhos de qualquer trabalho local no servidor. Também podem habilitar ou desabilitar todos os trabalhos locais e agendas no servidor. Para habilitar ou desabilitar trabalhos locais ou agendas, os membros desta função devem usar os procedimentos armazenados **sp_update_job** e **sp_update_schedule**. Apenas os parâmetros que especificam o nome do trabalho ou da agenda ou o identificador e o parâmetro **@enabled** podem ser especificados por membros de **SQLAgentOperatorRole**. Se especificarem algum outro parâmetro, a execução desses procedimentos armazenados falhará. Membros de**SQLAgentOperatorRole** não podem alterar a propriedade do trabalho para ganhar acesso a trabalhos que ainda não possuem.  
  
 Os nós **Trabalhos**, **Alertas**, **Operadores**e **Proxies** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são visíveis a membros de **SQLAgentOperatorRole**. Somente o nó **Logs de Erros** não é visível a membros desta função.  
  
> [!IMPORTANT]  
>  Considere as implicações de segurança antes de conceder acesso de proxy a membros das **funções**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agentdatabase**. Membros de **SQLAgentOperatorRole** tornam-se, automaticamente, membros de **SQLAgentUserRole** e **SQLAgentReaderRole**. Isso significa que membros de **SQLAgentOperatorRole** têm acesso a todos os proxies do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent concedidos às funções **SQLAgentUserRole** ou **SQLAgentReaderRole** e podem utilizá-los.  
  
 A tabela a seguir resume as permissões de **SQLAgentOperatorRole** em objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Ação|Alertas|Operadores|Trabalhos locais|Trabalhos multisservidor|Agendas de trabalho|Proxies|  
|------------|------------|---------------|----------------|----------------------|-------------------|-------------|  
|Criar/modificar/excluir|não|não|Sim <sup>2</sup> (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Exibir lista (enumerar)|Sim|Sim <sup>1</sup>|Sim|Sim|Sim|Sim|  
|Habilitar/desabilitar|não|não|Sim <sup>3</sup>|não|Sim <sup>4</sup>|Não aplicável|  
|Exibir propriedades|Sim|Sim|Sim|Sim|Sim|Sim|  
|Editar propriedades|não|não|Sim (apenas trabalhos possuídos)|não|Sim (somente agendas possuídas)|não|  
|Executar/interromper/iniciar|Não aplicável|Não aplicável|Sim|não|Não aplicável|Não aplicável|  
|Exibir histórico de trabalho|Não aplicável|Não aplicável|Sim|Sim|Não aplicável|Não aplicável|  
|Excluir histórico de trabalho|Não aplicável|Não aplicável|Sim|não|Não aplicável|Não aplicável|  
|Anexar/desanexar|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Sim (somente agendas possuídas)|Não aplicável|  
  
 <sup>1</sup> pode obter a lista de operadores disponíveis para uso em **sp_notify_operator** e **propriedades do trabalho** caixa de diálogo do Management Studio.  
  
 <sup>2</sup> não é possível alterar a propriedade do trabalho.  
  
 <sup>3</sup> **SQLAgentOperatorRole** membros podem habilitar ou desabilitar trabalhos locais que não possuem, por meio do procedimento armazenado **sp_update_job** e especificar valores para o **@enabled** e **@job_id** (ou **@job_name**) parâmetros. Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.  
  
 <sup>4</sup> **SQLAgentOperatorRole** membros podem habilitar ou desabilitar agendas que não possuem, por meio do procedimento armazenado **sp_update_schedule** e especificar valores para o **@enabled** e **@schedule_id** (ou **@name**) parâmetros. Se um membro desta função especificar algum outro parâmetro para esse procedimento armazenado, a execução do procedimento falhará.  
  
## <a name="assigning-users-multiple-roles"></a>Atribuindo várias funções aos usuários  
 Membros da função de servidor fixa **sysadmin** têm acesso a toda a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Caso um usuário não seja membro da função **sysadmin** , mas seja membro de mais de uma função de banco de dados fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, é importante ter em mente o modelo de permissões concêntricas dessas funções. Como funções mais privilegiadas sempre detêm todas as permissões das funções menos privilegiadas, o usuário que for membro de mais de uma função terá, automaticamente, as permissões associadas à função mais privilegiada de que é membro.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md)   
 [sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)   
 [sp_update_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)   
 [sp_notify_operator &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)   
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql)  
  
  
