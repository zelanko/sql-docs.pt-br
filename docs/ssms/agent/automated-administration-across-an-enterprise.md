---
title: "Administração automatizada em toda a empresa | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 618e199812a39ec29e032f8371419ec6184c713f
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="automated-administration-across-an-enterprise"></a>Administração automatizada em toda a empresa
A automatização de administração em várias instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é chamada *administração multisservidor*. Use a administração multisservidor para fazer o seguinte:  
  
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
Contém informações sobre como o uso contas não administrativas do Windows ou a conta Sistema Local para o serviço de agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pode afetar os ambientes multisservidores.  
  
[Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md)  
Contém informações sobre como definir a subchave de Registro MsxEncryptChannelOptions do[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent em servidores de destino.  
  
[Gerenciar trabalhos em toda a empresa](../../ssms/agent/manage-jobs-across-an-enterprise.md)  
Contém informações sobre a verificação do status de trabalho, alteração de servidores de destino para os trabalhos, sincronização de relógios do servidor de destino e sondagem de servidores mestres para o status de trabalho atual.  
  
[Solucionar problemas de trabalhos multisservidor que usam proxies](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
Contém informações sobre a solução de problemas de trabalhos multisservidor que usam proxies que falham.  
  
[Sondar servidores](../../ssms/agent/poll-servers.md)  
Contém informações sobre como fazer com que os servidores mestre de sondagem de servidores de destino sincronizem informações de trabalhos, implícita e explicitamente.  
  
[Gerenciar eventos](../../ssms/agent/manage-events.md)  
Contém informações sobre o encaminhamento de eventos dos servidores de destino para os servidores mestre.  
  
[Ajustar a administração automatizada em toda a empresa](../../ssms/agent/tune-automated-administration-across-an-enterprise.md)  
Contém informações sobre como a administração automatizada em um ambiente multisservidor aproveita os recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte também  
[Tópicos de compatibilidade com versões anteriores sobre a instalação do Mecanismo de Banco de Dados do SQL Server](http://msdn.microsoft.com/en-us/10de5ec6-d3cf-42ef-aa62-1bdf3fbde841)  
[Registrando servidores](http://msdn.microsoft.com/en-us/c2a2513e-fa09-419c-99e7-a12d57c5a0db)  
[sp_add_targetservergroup](http://msdn.microsoft.com/en-us/acb69343-d766-46ff-b771-0c7655c5231a)  
[sp_delete_targetserver](http://msdn.microsoft.com/en-us/cc438701-ad91-419d-9f23-ebc4c548c700)  
[sp_delete_targetservergroup](http://msdn.microsoft.com/en-us/d8dd838e-64aa-419f-9ccb-ff04908cf3e4)  
[sp_help_downloadlist](http://msdn.microsoft.com/en-us/745b265b-86e8-4399-b928-c6969ca1a2c8)  
[sp_help_jobserver](http://msdn.microsoft.com/en-us/57971787-f9f5-4199-9f64-c2b61a308906)  
[sp_help_targetservergroup](http://msdn.microsoft.com/en-us/ec3a4a68-b591-431c-9518-053ede522d0c)  
[sp_resync_targetserver](http://msdn.microsoft.com/en-us/40e44df7-d3e3-44ee-b149-08aba629a21f)  
[sp_update_targetservergroup](http://msdn.microsoft.com/en-us/4ac65ed6-e07e-40e4-a282-13bfd92dfa41)  
[sysjobservers](http://msdn.microsoft.com/en-us/9abcc20f-a421-4591-affb-62674d04575e)  
[syslogins](http://msdn.microsoft.com/en-us/4cb34f17-a4bb-469f-a218-71f074e6308f)  
[systargetservers](http://msdn.microsoft.com/en-us/479d1314-be37-4d19-ac9c-419fc9110e53)  
  

