---
title: Instalação e configuração do dispositivo
description: Orienta os administradores do dispositivo do Analytics Platform System (APS) por meio das etapas iniciais para configurar e começar a usar seu novo dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9f96d953dbd427bfb6cf94470c0ee80ade3aed48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401443"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Instalação e configuração do dispositivo para o Analytics Platform System
Orienta os administradores do dispositivo do Analytics Platform System (APS) por meio das etapas iniciais para configurar e começar a usar seu novo dispositivo.  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. instalar o hardware  
Seu novo dispositivo será entregue em paletes para o Dock em seu data center.  
  
> [!IMPORTANT]  
> Em alguns casos, seu IHV desempacotará, colocará em rack e conectará o dispositivo para você em seu data center. Nesse caso, essas instruções não são necessárias e você pode pular para a [3. Configure a seção do dispositivo](#ConfigureAppliance) abaixo.  
  
Se o seu IHV não estiver executando a instalação de hardware, use as etapas a seguir para instalar o hardware.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Confirmar documentação|Confirme que você recebeu todos os documentos e informações necessários do seu fornecedor de hardware independente (IHV). Confira [as informações a serem obtidas do seu sistema de plataforma de análise &#40;do IHV&#41;](information-to-obtain-from-your-ihv.md).|  
|Instalar o hardware|Verifique se o data center pode acomodar o dispositivo. Mova os componentes do dispositivo para a data center. Rack de comutadores de rede, PDUs e cabeamento. Consulte [instalação de Hardware &#40;&#41;do sistema de plataforma de análise ](hardware-installation.md).|  
  
## <a name="PowerOnAppliance"></a>2. ligar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Ligar o dispositivo|Ligue cada nó de componente de dispositivo na ordem necessária, aguardando a necessidade de confirmar se nenhum erro foi encontrado.|  
  
## <a name="ConfigureAppliance"></a>3. configurar o dispositivo  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|||  
|Configurar o dispositivo usando o SQL Server PDW**Configuration Manager**|Use o Configuration Manager para definir senhas de dispositivo, fusos horários, configurações de rede e firewall, certificados de segurança, desempenho e outras configurações em seu dispositivo. Consulte [configuração do dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md).|  
  
> [!WARNING]  
> As alterações de configuração só devem ser feitas usando o SQL Server PDW**Configuration Manager**. Não há suporte para as alterações não expostas por meio de **Configuration Manager** . Por exemplo, o dispositivo SQL Server PDW só dá suporte à configuração de idioma inglês dos EUA.  
  
## <a name="SoftwareServicing"></a>4. configurar a manutenção de software  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Aplicar atualizações de SQL Server PDW|Adicional Talvez seja necessário aplicar uma ou mais atualizações SQL Server PDW para atualizar o software SQL Server PDW para a versão mais recente. Consulte [aplicar hotfixes do sistema de plataforma de análise &#40;Analytics Platform system&#41;](apply-analytics-platform-system-hotfixes.md).|  
|Configurar o Windows Server Update Services|Configure o dispositivo para receber atualizações de Windows Server Update Services para software de suporte. Confira [baixar e aplicar as atualizações da Microsoft &#40;o sistema de plataforma de análise&#41;](download-and-apply-microsoft-updates.md).|  
  
## <a name="NextSteps"></a>Próximas etapas  
Depois de concluir todas as etapas anteriores, seu dispositivo estará pronto para uso. Você ou outras pessoas em seu local podem prosseguir com as tarefas a seguir.  
  
|||  
|-|-|  
|**Tarefa**|**Descrição**|  
|Instalar SQL Server PDW drivers e configurar a conectividade|Configure computadores locais para se conectarem ao SQL Server PDW usando SQL Server Data Tools, sqlcmd, business intelligence software ou outras ferramentas. <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|Criar logons e funções de servidor e atribuir permissões|Planeje e crie logons e funções de servidor que permitirão que os usuários façam logon no SQL Server PDW com as permissões apropriadas. <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Configurar o gateway de Gerenciamento de Dados do Azure|O Gateway permite que os usuários do Azure acessem dados do APS local expondo dados do APS como feeds OData seguros. O gateway já está instalado no nó de controle. Peça à Microsoft para obter assistência com a configuração.|  
|Monitorar consultas e usuários do dispositivo|Use o console de administração e outros recursos para monitorar as consultas e os usuários do dispositivo. Consulte [monitorar o dispositivo usando o console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|Carregar dados para SQL Server PDW|Carregar dados em seu dispositivo. <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|Criar um plano de recuperação de desastres|Planeje como você protegerá seus dados contra falhas de hardware ou substituições de dados. Crie um plano usando backups regulares e os planos de restauração em caso de corrupção ou perda de dados. <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|Monitorar o dispositivo|Monitore o estado, a integridade e o desempenho do dispositivo usando exibições do sistema, logs e o console do administrador. Corrija ou relate problemas. Consulte [monitorar o estado de integridade do dispositivo &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md).|  
