---
title: O dispositivo ativado ou desativado - Analytics Platform System de energia | Microsoft Docs
description: Ativar ou desativar o dispositivo de energia para o Analytics Platform System
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d24f808365a8a04fdc6b469a8eaac98c208c19e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960241"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Ativar ou desativar o dispositivo de energia para o Analytics Platform System
Este tópico descreve como a liga / desliga sua Systemappliance de plataforma de análise que está executando o Parallel Data Warehouse. Use este tópico quando um dispositivo do Analytics Platform System é movido, ou a potência em um dispositivo após uma falha catastrófica de energia.  
  
Alimentar o dispositivo de intermitente não é o mesmo que iniciar e interromper os serviços do dispositivo. Para obter informações sobre esse assunto, consulte [Status de serviços do PDW &#40;Analytics Platform System&#41;](pdw-services-status.md). Para obter informações sobre a habilitação ou desativar um SQL Server 2008 Parallel Data Warehouse, consulte o arquivo de Ajuda do SQL Server 2008 Parallel Data Warehouse. Para obter informações sobre a habilitação ou desativar um SQL Server 2012 AU1 ou AU2 Parallel Data Warehouse, consulte o arquivo de ajuda para essas versões.  
  
Quando essas instruções especificam a conexão a um nó do SQL Server PDW, a conexão pode ser local usando dispositivos conectados (KVM) ou remoto usando a área de trabalho remota. Algumas ações devem ser física (ativar um chave liga / desliga) e alguns (como desligar) poderá ser físico ou usando o Windows comandos.  
  
Conexões para SQL Server PDW nós podem ser feitas usando os endereços IP atribuídos a nós ou do **HST01** computador usando o **Gerenciador de Cluster de Failover** (**cluadmin**) ou **Gerenciador do Hyper-V** (**virtmgmt.msc**) clicando duas vezes o nome do nó e aplicativos.  
  
## <a name="PowerOff"></a>Desligar o dispositivo  
  
### <a name="before-you-begin"></a>Antes de começar  
Antes de desligar o dispositivo, você deve encerrar todas as atividades no dispositivo. Para encerrar todas as atividades:  
  
-   Use o **sessões** página do Console do administrador para identificar os usuários atuais. Entre em contato com eles e peça para ele fazer logoff.  
  
-   Se necessário você pode usar o **KILL** instrução para forçar o encerramento de uma conexão de cliente. Tenha cuidado ao encerrar conexões. Quando interrompida, alguns processos transacionais, como uma atualização de longa execução, deverá atividade de reversão antes do SQL Server pode concluir a recuperação do banco de dados. Revertendo uma atualização parcialmente concluída ou exclusão, pode ser demorado.  
  
### <a name="to-power-off-the-appliance"></a>Para desligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída antes que a próxima etapa é executada, a menos que indicado o contrário. Executando etapas fora de ordem ou sem aguardar concluir cada etapa pode resultar em erros quando o dispositivo é ligado em um momento posterior.  
  
1.  Conectar-se ao nó de controle do PDW ( **_PDW_region_-CTL01** ) e faça logon com a conta de administrador de domínio de dispositivo do Analytics Platform System.  
  
2.  Execute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir o **Configuration Manager**.  
  
3.  No Configuration Manager, sob o **topologia de depósito de dados paralela** menu, clique no **Status dos serviços** guia e, em seguida, clique em **parar região** para interromper os serviços do PDW.   
  
4.  Conectar-se ao  **_appliance_domain_-HST01** e faça logon com a conta de administrador de domínio do dispositivo.  
  
5.  Usando o **Gerenciador de Cluster de Failover** conecte-se para o  **_appliance_domain_-WFOHST01** do cluster, se não é automaticamente conectado e, em seguida, no painel de navegação, clique em **Funções**. No **funções** painel:  
  
    1.  Multisseleção de todas as máquinas virtuais. Clique com botão direito-los e, em seguida, selecione **desligar**.  
  
    2.  Aguarde até que todas as VMs selecionadas concluir o desligamento.  
  
6.  Fechar o **Gerenciador de Cluster de Failover** aplicativo.  
  
7. Desligar todos os servidores, exceto  **_appliance_domain_-HST01**.  
  
8. Desligar o  **_appliance_domain_-HST01** server.  
  
9. Desligue a unidades de distribuição de alimentação (PDUs).  
  
## <a name="PowerOn"></a>Ligar o dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para ligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída antes que a próxima etapa é executada, a menos que indicado o contrário. Executando etapas fora de ordem ou sem aguardar concluir cada etapa pode resultar em erros de inicialização.  
  
1.  Ligue o unidades de distribuição de alimentação (PDU) e aguarde até que as opções para iniciar automaticamente.  
  
2.  Ligar o  **_appliance_domain_-HST01** server.  
  
3.  Faça logon no  **_appliance_domain_-HST01** como o administrador de domínio do dispositivo.  
  
4.  Iniciar o **Gerenciador do Hyper-V** programa (**virtmgmt.msc**) e conecte-se à  **_appliance_domain_-HST01** se não conectado por padrão.  
  
    1.  Se você não pode se conectar por nome porque o  **_PDW_region_-AD01** é não em execução, tente conectar-se usando o endereço IP.  
  
    2.  No **máquinas virtuais** painel, localize  **_PDW_region_-AD01** e confirme se ele está em execução. Caso contrário, inicie essa VM e aguarde até que ele seja totalmente iniciado.  
  
5.  Ligar o restante dos servidores no dispositivo.  
  
6.  Enquanto estiver em **HST01** estiver conectado como administrador de domínio do dispositivo, no **Gerenciador do Hyper-V**:  
  
    1.  Conectar-se ao  **_appliance_domain_-HST02**.  
  
    2.  No **máquinas virtuais** painel, localize  **_PDW_region_-AD02** e confirme se ele está em execução.  Caso contrário, inicie essa VM e aguarde até que ele seja totalmente iniciado.  
  
7.  Usando o **Gerenciador de Cluster de Failover** conectar-se para o  **_appliance_domain_-WFOHST01** do cluster, se não é automaticamente conectado e, em seguida, no  **Navegação** painel, clique em **funções**. No **funções** painel:  
  
    1.  Multisseleção de todas as máquinas virtuais, clique com botão direito-los e, em seguida, clique em **iniciar**.  
  
    2.  Aguarde até que todas as VMs selecionadas para concluir a inicialização antes de prosseguir para a próxima etapa.  
  
    3.  Se for necessário para as VMs com failover, desligá-los, movê-los e reiniciá-los no host principal adequado.  
  
8. Desconecte **HST01** se desejar.  
  
9. Conectar-se ao  **_PDW_region_-CTL01** usando a conta de administrador de domínio do dispositivo.  
  
10. Execute `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar o **Configuration Manager**.  
  
11. No **Configuration Manager**, no **topologia de depósito de dados paralela** menu, clique no **Status dos serviços** guia e, em seguida, clique em **iniciar região**para iniciar os serviços do PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Para verificar a integridade do dispositivo  
Depois que o dispositivo for iniciada, abra o **Console de administração** e verifique a página de integridade para alertas que podem indicar as condições de falha. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Consulte também  
[Tarefas de gerenciamento de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
