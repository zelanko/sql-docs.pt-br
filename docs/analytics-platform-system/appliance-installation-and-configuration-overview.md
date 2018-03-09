---
title: "Instalação do dispositivo e visão geral da configuração (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10934f62-4acf-4ca5-b550-f426ba81fe11
caps.latest.revision: "23"
ms.openlocfilehash: 719447d2f6d9376ec9db35f35c7f38b50ef460fa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="appliance-installation-and-configuration-overview"></a>Instalação do dispositivo e visão geral da configuração
Orienta os administradores de dispositivo do SQL Server PDW pelas etapas iniciais para configurar e começar a usar o novo dispositivo de PDW do SQL Server.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Instalar o Hardware  
Seu novo aplicativo será entregue em paletes de encaixe em seu data center.  
  
> [!IMPORTANT]  
> Em alguns casos, seu IHVS serão desembale, rack e conecte o dispositivo para você em seu data center. Se assim, essas instruções não são necessárias, e você pode ignorar o [3. Configurar o dispositivo](#ConfigureAppliance) seção abaixo.  
  
Se seu IHVS não está executando a instalação de hardware, use as etapas a seguir para instalar o hardware.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Confirme a documentação|Confirme que você tenha recebido todas as informações e documentos necessários de seu fornecedor de hardware independentes (IHVS). Consulte [informações para obter de sua IHVS &#40; Analytics Platform System &#41; ](information-to-obtain-from-your-ihv.md).|  
|Instale o hardware|Verifique se que o data center pode acomodar o dispositivo. Mova os componentes do dispositivo para o data center. Os comutadores de rede, PDUs, do rack e o cabeamento. Consulte [instalação do Hardware &#40; Analytics Platform System &#41; ](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Ligar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Ligar o dispositivo|Ligar cada nó de componente do dispositivo na ordem necessária, esperando conforme necessário para confirmar que nenhum erro for encontrado.|  
  
## <a name="ConfigureAppliance"></a>3. Configurar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|||  
|Configurar o dispositivo usando o SQL Server PDW**do Configuration Manager**|Use o Gerenciador de configurações para definir as senhas do dispositivo, fusos horários, configurações de rede e firewall, certificados de segurança, desempenho e outras configurações no seu dispositivo. Consulte [configuração de dispositivo &#40; Analytics Platform System &#41; ](appliance-configuration.md).|  
  
> [!WARNING]  
> Alterações de configuração só devem ser realizadas usando o SQL Server PDW**do Configuration Manager**. As alterações não são expostas por meio de **do Configuration Manager** não têm suporte. Por exemplo, o utilitário do SQL Server PDW suporta apenas a configuração do idioma inglês.  
  
## <a name="SoftwareServicing"></a>4. Configurar o serviço de Software  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Aplicar atualizações do SQL Server PDW|(Opcional) Talvez seja necessário aplicar uma ou mais atualizações de PDW do SQL Server para atualizar o software do SQL Server PDW para a versão mais recente. Consulte [aplicar Hotfixes do sistema de plataforma de análise &#40; Analytics Platform System &#41; ](apply-analytics-platform-system-hotfixes.md).|  
|Configurar o Windows Server Update Services|Configure o dispositivo para receber atualizações do Windows Server Update Services para dar suporte a software. Consulte [Baixe e aplique as atualizações da Microsoft &#40; Analytics Platform System &#41; ](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Próximas etapas  
Depois de concluir todas as etapas anteriores, o dispositivo está pronto para uso. Você ou outros pessoal em seu local pode prosseguir com as seguintes tarefas.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Instalar os drivers do SQL Server PDW e configurar a conectividade|Configure computadores locais para se conectar ao SQL Server PDW usando o SQL Server Data Tools, sqlcmd, softwares de inteligência de negócio ou outras ferramentas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Criar logons e funções de servidor e atribuir permissões|Planejar e criar logons e funções de servidor que permitirá que os usuários façam logon SQL Server PDW com as permissões apropriadas. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurar o Gateway de gerenciamento de dados do Azure|O Gateway permite que os usuários do Azure acessar dados de pontos de acesso local pela exposição de pontos de acesso de dados seguro feeds de OData. O Gateway já está instalado no nó de controle. Peça ao Microsoft para obter assistência com a configuração.|  
|Monitor de consultas e os usuários do dispositivo|Use o Console de administração e outros recursos para monitorar as consultas e os usuários do dispositivo. Consulte [monitorar o dispositivo usando o Console de administração &#40; Analytics Platform System &#41; ](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Carregar dados para o SQL Server PDW|Carregar dados em seu dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Criar um plano de recuperação de desastres|Planeje como você deseja proteger seus dados contra falhas de hardware ou substitui dados. Criar um plano usando backups regulares planos e restauração no caso de perda ou de corrupção de dados. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Monitor de dispositivo|Monitore o estado do aplicativo, a integridade e o desempenho usando exibições do sistema, logs e o Console de administração. Corrija ou relatar problemas. Consulte [estado de integridade do Monitor de dispositivo &#40; Analytics Platform System &#41; ](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
