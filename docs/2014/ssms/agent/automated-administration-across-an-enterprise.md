---
title: Administração automatizada em toda a empresa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c3b9d1885aefc738355f9f891680ebcfaf9d19a2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813062"
---
# <a name="automated-administration-across-an-enterprise"></a>Administração automatizada em toda a empresa
  A automatização de administração em várias instâncias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é chamada *administração multisservidor*. Use a administração multisservidor para fazer o seguinte:  
  
-   Gerenciar dois ou mais servidores.  
  
-   Programar fluxos de informações entre servidores corporativos para data warehousing.  
  
> [!NOTE]  
>  Como parte dos esforços contínuos da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para reduzir o custo total de propriedade, o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] apresentou dois recursos: um método de gerenciamento de servidor chamado de Gerenciamento Baseado em Políticas e consultas multisservidores que usam servidores de configuração e grupos de servidores. Esses recursos podem ser usados com, ou em vez de, alguns dos recursos que são descritos neste tópico. Para obter mais informações, consulte [administrar servidores usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md) e [administrar vários servidores usando servidores de gerenciamento Central](../../relational-databases/administer-multiple-servers-using-central-management-servers.md).  
  
 Para aproveitar a administração multisservidores, é necessário ter pelo menos um servidor mestre e um servidor de destino. Um servidor mestre distribui trabalhos para servidores de destino e também recebe eventos desses servidores. Ele também armazena a cópia central das definições de trabalho para trabalhos que são executados em servidores de destino. Os servidores de destino conectam-se periodicamente ao servidor mestre para atualizar a agenda de trabalhos. Se um trabalho novo existir no servidor mestre, o servidor de destino descarregará o trabalho. Depois que o servidor de destino concluir o trabalho, ele se reconectará ao servidor mestre e reportará o status do trabalho.  
  
 A ilustração a seguir mostra a relação entre servidores mestre e de destino:  
  
 ![Configuração da administração multisservidor](../../database-engine/media/multisvr.gif "Configuração da administração multisservidor")  
  
 Se você administrar servidores departamentais em uma grande corporação, poderá definir o seguinte:  
  
-   Um trabalho de backup com etapas de trabalho.  
  
-   Operadores para notificação no caso de falha no backup.  
  
-   Uma agenda de execução para o trabalho de backup.  
  
 Grave este trabalho de backup uma vez no servidor mestre e, em seguida, relacione cada servidor de departamento como um servidor de destino. Nesse momento, todos os servidores de departamento executam o mesmo trabalho de backup, mesmo que você defina o trabalho apenas uma vez.  
  
> [!NOTE]  
>  Os recursos de administração multisservidor são projetados para membros da função sysadmin. Entretanto, um membro da função sysadmin no servidor de destino não pode editar as operações que são executadas no servidor de destino pelo servidor mestre. Esta medida de segurança impede que etapas de trabalho sejam excluídas acidentalmente e operações no servidor de destino sejam interrompidas.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criar um ambiente multisservidor](create-a-multiserver-environment.md)  
 Contém informações sobre como criar e gerenciar os servidores mestre e de destino.  
  
 [Escolher a conta de serviço do SQL Server Agent certa para ambientes multisservidor](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md)  
 Contém informações sobre como o uso contas não administrativas do Windows ou a conta Sistema Local para o serviço de agente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode afetar os ambientes multisservidores.  
  
 [Definir opções de criptografia em servidores de destino](set-encryption-options-on-target-servers.md)  
 Contém informações sobre como definir a subchave de Registro MsxEncryptChannelOptions do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent em servidores de destino.  
  
 [Gerenciar trabalhos em toda a empresa](manage-jobs-across-an-enterprise.md)  
 Contém informações sobre a verificação do status de trabalho, alteração de servidores de destino para os trabalhos, sincronização de relógios do servidor de destino e sondagem de servidores mestres para o status de trabalho atual.  
  
 [Solucionar problemas de trabalhos multisservidor que usam proxies](troubleshoot-multiserver-jobs-that-use-proxies.md)  
 Contém informações sobre a solução de problemas de trabalhos multisservidor que usam proxies que falham.  
  
 [Sondar servidores](poll-servers.md)  
 Contém informações sobre como fazer com que os servidores mestre de sondagem de servidores de destino sincronizem informações de trabalhos, implícita e explicitamente.  
  
 [Gerenciar eventos](manage-events.md)  
 Contém informações sobre o encaminhamento de eventos dos servidores de destino para os servidores mestre.  
  
 [Ajustar a administração automatizada em toda a empresa](tune-automated-administration-across-an-enterprise.md)  
 Contém informações sobre como a administração automatizada em um ambiente multisservidor aproveita os recursos de autoajuste do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Registrar servidores](../register-servers/register-servers.md)   
 [sp_add_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql)   
 [sp_delete_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql)   
 [sp_help_downloadlist &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql)   
 [sp_help_jobserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobserver-transact-sql)   
 [sp_help_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)   
 [sp_update_targetservergroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql)   
 [dbo.sysjobservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobservers-transact-sql)   
 [sys. syslogins &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)   
 [dbo.systargetservers &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-systargetservers-transact-sql)  
  
  
