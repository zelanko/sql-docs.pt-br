---
title: Ligar ou desligar o dispositivo
description: Ligar ou desligar o dispositivo para o Analytics Platform System
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400627"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Ligar ou desligar o dispositivo para o Analytics Platform System
Este tópico descreve como ligar ou desligar sua plataforma de análise Systemappliance que está executando data warehouse paralelas. Use este tópico quando um dispositivo de sistema de plataforma de análise for movido ou para ligar um dispositivo após uma falha catastrófica de energia.  
  
Ligar e desligar o dispositivo não é o mesmo que iniciar e parar os serviços do dispositivo. Para obter informações sobre esse assunto, consulte [status dos serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md). Para obter informações sobre como ligar ou desligar um data warehouse paralelo SQL Server 2008, consulte o arquivo de ajuda do SQL Server 2008 Parallel data warehouse. Para obter informações sobre como ligar ou desligar um data warehouse SQL Server 2012 AU1 ou AU2 paralelo, consulte o arquivo de ajuda para essas versões.  
  
Quando essas instruções especificam a conexão a um nó SQL Server PDW, a conexão pode ser local usando dispositivos conectados (KVM) ou remoto usando Área de Trabalho Remota. Algumas ações devem ser físicas (ligando um interruptor de energia) e algumas (como desligar) podem ser físicas ou usando comandos do Windows.  
  
Conexões com SQL Server PDW nós podem ser feitas usando os endereços IP atribuídos aos nós ou do computador **HST01** usando os aplicativos **Gerenciador de cluster de failover** (**cluadmin. msc**) ou **Gerenciador do Hyper-V** (**virtmgmt. msc**) e clicando com o botão direito do mouse no nome do nó.  
  
## <a name="PowerOff"></a>Desligar o dispositivo  
  
### <a name="before-you-begin"></a>Antes de começar  
Antes de desligar o dispositivo, você deve encerrar todas as atividades no dispositivo. Para encerrar todas as atividades:  
  
-   Use a página **sessões** do console de administração para identificar os usuários atuais. Entre em contato com eles e peça que eles façam logoff.  
  
-   Se necessário, você pode usar a instrução **Kill** para forçar o encerramento de uma conexão de cliente. Tenha cuidado ao eliminar conexões. Quando interrompido, alguns processos transacionais, como uma atualização de execução longa, devem reverter a atividade antes que SQL Server possa concluir a recuperação do banco de dados. Reverter uma atualização ou exclusão parcialmente concluída pode ser demorado.  
  
### <a name="to-power-off-the-appliance"></a>Para desligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída antes que a próxima etapa seja executada, salvo indicação em contrário. Executar as etapas fora de ordem ou sem aguardar a conclusão de cada etapa pode resultar em erros quando o dispositivo for ligado em um momento posterior.  
  
1.  Conecte-se ao nó de controle do PDW (**_PDW_region_-CTL01** ) e faça logon com a conta de administrador de domínio da solução de plataforma de análise.  
  
2.  Execute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir o **Configuration Manager**.  
  
3.  No Configuration Manager, no menu **data warehouse topologia paralela** , clique na guia **status dos serviços** e clique em **parar região** para parar os serviços do PDW.   
  
4.  Conecte-se a ** _appliance_domain_-HST01** e faça logon com a conta de administrador de domínio do dispositivo.  
  
5.  Usando o **Gerenciador de cluster de failover** conectar-se ao cluster ** _appliance_domain_-WFOHST01** , se não estiver conectado automaticamente e, em seguida, no painel de navegação, clique em **funções**. No painel **funções** :  
  
    1.  Seleção múltipla de todas as máquinas virtuais. Clique com o botão direito do mouse neles e selecione **desligar**.  
  
    2.  Aguarde até que todas as VMs selecionadas concluam o desligamento.  
  
6.  Feche o aplicativo **Gerenciador de cluster de failover** .  
  
7. Desligue todos os servidores, exceto ** _appliance_domain_-HST01**.  
  
8. Desligue o servidor ** _appliance_domain_-HST01** .  
  
9. Desligue as unidades de distribuição de energia (PDUs).  
  
## <a name="PowerOn"></a>Ligar o dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para ligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída antes que a próxima etapa seja executada, salvo indicação em contrário. Executar etapas fora de ordem ou sem aguardar a conclusão de cada etapa pode resultar em erros de inicialização.  
  
1.  Ligue as unidades de distribuição de energia (PDU) e aguarde até que as opções sejam iniciadas automaticamente.  
  
2.  Ligue o servidor ** _appliance_domain_-HST01** .  
  
3.  Faça logon no ** _appliance_domain_-HST01** como o administrador de domínio do dispositivo.  
  
4.  Inicie o programa **Gerenciador do Hyper-V** (**virtmgmt. msc**) e conecte-se a ** _appliance_domain_-HST01** se não estiver conectado por padrão.  
  
    1.  Se você não puder se conectar por nome porque o ** _PDW_region_-AD01** não está em execução, tente se conectar usando o endereço IP.  
  
    2.  No painel **máquinas virtuais** , localize ** _PDW_region_-AD01** e confirme se ele está em execução. Caso contrário, inicie essa VM e aguarde que ela seja totalmente iniciada.  
  
5.  Ligue o restante dos servidores no dispositivo.  
  
6.  Enquanto estiver no **HST01** conectado como o administrador de domínio do dispositivo, no **Gerenciador do Hyper-V**:  
  
    1.  Conecte-se a ** _appliance_domain_-HST02**.  
  
    2.  No painel **máquinas virtuais** , localize ** _PDW_region_-AD02** e confirme se ele está em execução.  Caso contrário, inicie essa VM e aguarde que ela seja totalmente iniciada.  
  
7.  Usando o **Gerenciador de cluster de failover** conectar-se ao cluster ** _appliance_domain_-WFOHST01** , se não estiver conectado automaticamente e, em seguida, no painel de **navegação** , clique em **funções**. No painel **funções** :  
  
    1.  Selecione várias das máquinas virtuais, clique com o botão direito do mouse nelas e clique em **Iniciar**.  
  
    2.  Aguarde até que todas as VMs selecionadas terminem de ser iniciadas antes de prosseguir para a próxima etapa.  
  
    3.  Se necessário, para as VMs que passaram por failover, desligue-as, mova-as e reinicie-as no host primário apropriado.  
  
8. Desconecte do **HST01** se desejar.  
  
9. Conecte-se a ** _PDW_region_-CTL01** usando a conta de administrador de domínio do dispositivo.  
  
10. Execute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar o **Configuration Manager**.  
  
11. Na **Configuration Manager**, no menu **topologia paralela data warehouse** , clique na guia **status dos serviços** e clique em **Iniciar região** para iniciar os serviços do PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Para verificar a integridade do dispositivo  
Depois que o dispositivo for iniciado, abra o **console de administração** e verifique a página de integridade para obter alertas que possam indicar condições de falha. Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração &#40;&#41;do sistema de plataforma de análise ](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
