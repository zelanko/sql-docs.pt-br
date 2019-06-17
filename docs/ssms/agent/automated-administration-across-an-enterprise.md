---
title: Administração automatizada em toda a empresa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enterprise automatic administration [SQL Server]
- multiserver administration [SQL Server]
- SQL Server Agent jobs, multiserver administration
- jobs [SQL Server Agent], multiserver administration
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- master servers [SQL Server]
- multiple instances of SQL Server
- target servers [SQL Server]
ms.assetid: 44d8365b-42bd-4955-b5b2-74a8a9f4a75f
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 905a470c09c1fff750900764134846925d7899b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095876"
---
# <a name="automated-administration-across-an-enterprise"></a>Administração automatizada em toda a empresa
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A automatização de administração em várias instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é chamada *administração multisservidor*. Use a administração multisservidor para fazer o seguinte:  
  
-   Gerenciar dois ou mais servidores.  
  
-   Programar fluxos de informações entre servidores corporativos para data warehousing.  
  
Para aproveitar a administração multisservidores, é necessário ter pelo menos um servidor mestre e um servidor de destino. Um servidor mestre distribui trabalhos para servidores de destino e também recebe eventos desses servidores. Ele também armazena a cópia central das definições de trabalho para trabalhos que são executados em servidores de destino. Os servidores de destino conectam-se periodicamente ao servidor mestre para atualizar a agenda de trabalhos. Se um trabalho novo existir no servidor mestre, o servidor de destino descarregará o trabalho. Depois que o servidor de destino concluir o trabalho, ele se reconectará ao servidor mestre e reportará o status do trabalho. Observe que a definição de trabalho deve ser igual ao executar alguma atividade relacionada do banco de dados.  
  
A ilustração a seguir mostra a relação entre servidores mestre e de destino:  
  
![Configuração da administração multisservidor](../../ssms/agent/media/multisvr.gif "Configuração da administração multisservidor")  
  
Se você administrar servidores departamentais em uma grande corporação, poderá definir o seguinte:  
  
-   Um trabalho de backup com etapas de trabalho.  
  
-   Operadores para notificação no caso de falha no backup.  
  
-   Uma agenda de execução para o trabalho de backup.  
  
Grave este trabalho de backup uma vez no servidor mestre e, em seguida, relacione cada servidor de departamento como um servidor de destino. Nesse momento, todos os servidores de departamento executam o mesmo trabalho de backup, mesmo que você defina o trabalho apenas uma vez.  
  
> [!NOTE]  
> Os recursos de administração multisservidor são projetados para membros da função sysadmin. Entretanto, um membro da função sysadmin no servidor de destino não pode editar as operações que são executadas no servidor de destino pelo servidor mestre. Esta medida de segurança impede que etapas de trabalho sejam excluídas acidentalmente e operações no servidor de destino sejam interrompidas.  
  
## <a name="in-this-section"></a>Nesta seção  
[Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md)  
Contém informações sobre como criar e gerenciar os servidores mestre e de destino.  
  
[Escolher a conta de serviço do SQL Server Agent certa para ambientes multisservidor](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
Contém informações sobre como o uso contas não administrativas do Windows ou a conta Sistema Local para o serviço de agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode afetar os ambientes multisservidores.  
  
[Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md)  
Contém informações sobre como definir a subchave de Registro de agente MsxEncryptChannelOptions do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em servidores de destino.  
  
[Gerenciar trabalhos em toda a empresa](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
Contém informações sobre a verificação do status de trabalho, alteração de servidores de destino para os trabalhos, sincronização de relógios do servidor de destino e sondagem de servidores mestres para o status de trabalho atual.  
  
[Solucionar problemas de trabalhos multisservidor que usam proxies](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
Contém informações sobre a solução de problemas de trabalhos multisservidor que usam proxies que falham.  
  
[Sondar servidores](../../ssms/agent/poll-servers.md)  
Contém informações sobre como fazer com que os servidores mestre de sondagem de servidores de destino sincronizem informações de trabalhos, implícita e explicitamente.  
  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
Contém informações sobre o encaminhamento de eventos dos servidores de destino para os servidores mestre.  
  
[Ajustar a administração automatizada em toda a empresa](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
Contém informações sobre como a administração automatizada em um ambiente multisservidor aproveita os recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Tópicos de compatibilidade com versões anteriores sobre a instalação do Mecanismo de Banco de Dados do SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
[Registrando servidores](../register-servers/register-servers.md)  
[sp_add_targetservergroup](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)  
[sp_delete_targetserver](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)  
[sp_delete_targetservergroup](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)  
[sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)  
[sp_help_jobserver](../../relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql.md)  
[sp_help_targetservergroup](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)  
[sp_resync_targetserver](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
[sp_update_targetservergroup](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
[sysjobservers](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)  
[syslogins](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
[systargetservers](../../relational-databases/system-tables/dbo-systargetservers-transact-sql.md)  
  
