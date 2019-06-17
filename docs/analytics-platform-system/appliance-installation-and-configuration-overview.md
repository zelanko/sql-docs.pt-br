---
title: Dispositivo instale e configure - o Analytics Platform System | Microsoft Docs
description: Orienta os administradores de dispositivo do Analytics Platform System (APS) pelas etapas iniciais para configurar e começar a usar seu novo aplicativo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5b6aa75cdab85fce9ef308d3e853ddb0107c28ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276348"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Instalação de dispositivo e configuração para o Analytics Platform System
Orienta os administradores de dispositivo do Analytics Platform System (APS) pelas etapas iniciais para configurar e começar a usar seu novo aplicativo.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. Instalar o Hardware  
Seu novo aplicativo será entregue em paletes ao encaixe no seu data center.  
  
> [!IMPORTANT]  
> Em alguns casos, IHV será desempacotar, montar em rack e conecte-se o dispositivo para você em seu data center. Nesse caso, essas instruções não são necessárias, e você poderá pular para o [3. Configurar o dispositivo](#ConfigureAppliance) seção abaixo.  
  
Se seu IHV não estiver executando a instalação de hardware, use as seguintes etapas para instalar o hardware.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Confirme se a documentação|Confirme que você tenha recebido todos os documentos necessários e informações de seu fornecedor de hardware independentes (IHVS). Ver [informações a serem obtidas do IHV &#40;Analytics Platform System&#41;](information-to-obtain-from-your-ihv.md).|  
|Instalar o hardware|Verifique se que o data center pode acomodar o dispositivo. Mova os componentes do dispositivo para o data center. Os comutadores de rede, PDUs, montar em rack e cabeamento. Ver [instalação de Hardware &#40;Analytics Platform System&#41;](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. Ligar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Ligar o dispositivo|Alimentação em cada nó de componente de dispositivo na ordem necessária, esperando conforme necessário para confirmar que nenhum erro for encontrado.|  
  
## <a name="ConfigureAppliance"></a>3. Configurar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|||  
|Configurar o dispositivo usando o SQL Server PDW**do Configuration Manager**|Use o Configuration Manager para definir as senhas do dispositivo, fusos horários, configurações de rede e firewall, certificados de segurança, desempenho e outras configurações em seu dispositivo. Ver [configuração do dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> Alterações de configuração só devem ser realizadas usando o SQL Server PDW**Configuration Manager**. As alterações não são expostos por meio **Configuration Manager** não têm suporte. Por exemplo, o dispositivo de PDW do SQL Server suporta apenas a configuração de idioma do inglês-EUA.  
  
## <a name="SoftwareServicing"></a>4. Configurar o Software de manutenção  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Aplicar atualizações do SQL Server PDW|(Opcional) Talvez você precise aplicar uma ou mais atualizações do SQL Server PDW para atualizar o software do SQL Server PDW para a versão mais recente. Ver [aplicar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Configurar o Windows Server Update Services|Configure o dispositivo para receber atualizações do Windows Server Update Services para dar suporte a software. Ver [Baixe e aplique as atualizações da Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Próximas etapas  
Depois de concluir todas as etapas anteriores, o dispositivo está pronto para uso. Você ou outros funcionários em seu local podem prosseguir com as seguintes tarefas.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Instalar drivers do SQL Server PDW e configurar a conectividade|Configure computadores locais para se conectar ao SQL Server PDW, usando o SQL Server Data Tools, sqlcmd, software de inteligência de negócios ou outras ferramentas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Criar logons e funções de servidor e atribuir permissões|Planeje e crie logons e funções de servidor que permitirá que os usuários façam logon SQL Server PDW com as permissões apropriadas. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurar o Gateway de gerenciamento de dados do Azure|O Gateway permite que os usuários do Azure acessar dados APS de local, expondo dados de pontos de acesso seguro feeds de OData. O Gateway já está instalado no nó de controle. Pergunte à Microsoft para obter assistência com a configuração.|  
|Monitor de consultas e os usuários do dispositivo|Use o Console de administração e outros recursos para monitorar as consultas e os usuários do dispositivo. Ver [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Carregar dados para o SQL Server PDW|Carregar dados para seu dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Criar um plano de recuperação de desastre|Planeje como você protegerá seus dados contra falhas de hardware ou substituem dados. Criar um plano usando backups regulares e planos no caso de corrupção de dados ou perda de restauração. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Monitorar o dispositivo|Monitore o estado do dispositivo, integridade e desempenho com exibições do sistema, logs e o Console de administração. Corrija ou reportar problemas. Ver [estado de integridade do Monitor de dispositivo &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
