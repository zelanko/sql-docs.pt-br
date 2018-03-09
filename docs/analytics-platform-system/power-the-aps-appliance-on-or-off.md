---
title: Ligar o dispositivo de APS ativado ou desativado (Analytics Platform System)
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
ms.assetid: 2258f8e3-e7a1-4455-8a5e-10d4d15775d6
caps.latest.revision: "45"
ms.openlocfilehash: 5e96898197098556d256c46b517ea42650c4c3ac
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="power-the-aps-appliance-on-or-off"></a>Ligar o dispositivo de APS ou desligar
Este tópico descreve como ligar ou desligar o Systemappliance de plataforma de análise que esteja executando o Parallel Data Warehouse e, opcionalmente, executando uma região de HDInsight. Use este tópico quando um dispositivo Analytics Platform System é movido ou a potência em um dispositivo após uma falha catastrófica de energia.  
  
Alimentar o dispositivo e desativar não é o mesmo que iniciar e parar os serviços de dispositivo. Para obter informações sobre o assunto, consulte [PDW serviços Status &#40; Analytics Platform System &#41; ](pdw-services-status.md). Para obter informações sobre a habilitação de ativar ou desativar um SQL Server 2008 Parallel Data Warehouse, consulte o arquivo de Ajuda do SQL Server 2008 Parallel Data Warehouse. Para obter informações sobre a habilitação ou desativar um SQL Server 2012 AU1 ou AU2 Parallel Data Warehouse, consulte o arquivo de ajuda para essas versões.  
  
Quando essas instruções especifiquem a conexão a um nó do SQL Server PDW, a conexão pode ser local usando dispositivos conectados (KVM) ou remoto usando a área de trabalho remota. Algumas ações devem ser físico (ativar um chave liga / desliga) e alguns (como desligar) pode ser físico ou usando o Windows comandos.  
  
Conexões para nós do SQL Server PDW podem ser feitas usando os endereços IP atribuídos a nós ou do **HST01** computador usando o **Gerenciador de Cluster de Failover** (**cluadmin.msc**) ou **Gerenciador Hyper-V** (**virtmgmt.msc**) clicando duas vezes o nome do nó e aplicativos.  
  
## <a name="PowerOff"></a>Desligar o dispositivo  
  
### <a name="before-you-begin"></a>Antes de começar  
Antes de desligar o dispositivo, você deve encerrar todas as atividades no dispositivo. Para encerrar todas as atividades:  
  
-   Use o **sessões** página do Console de administração para identificar os usuários atuais. Entre em contato com eles e solicite a fazer logoff.  
  
-   Se necessário você pode usar o **KILL** instrução para forçar o encerramento de uma conexão de cliente. Tenha cuidado quando a eliminação de conexões. Quando interrompida, alguns processos transacionais, como uma atualização de longa execução deve atividade de reversão antes do SQL Server pode concluir a recuperação do banco de dados. Revertendo uma atualização parcialmente concluída ou delete, pode ser demorado.  
  
### <a name="to-power-off-the-appliance"></a>Para desligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída para a próxima etapa é executada, a menos que indicado o contrário. Executar etapas fora de ordem ou sem aguardar concluir cada etapa pode resultar em erros quando o dispositivo é ligado em um momento posterior.  
  
1.  Conecte-se ao nó de controle do PDW (***PDW_region*-CTL01** ) e faça logon com a conta de administrador de domínio de aplicativo Analytics Platform System.  
  
2.  Executar `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para abrir o **do Configuration Manager**.  
  
3.  No Configuration Manager, sob o **topologia de depósito de dados paralela** menu, clique no **Status de serviços** guia e, em seguida, clique em **região parar** para interromper os serviços do PDW.  
  
4.  Se houver uma região de HDInsight, no **HDInsight topologia** menu, clique no **Status de serviços** guia e, em seguida, clique em **região parar** para interromper os serviços do HDInsight.  
  
5.  Conecte-se ao  ***appliance_domain*-HST01** e faça logon com a conta de administrador de domínio do dispositivo.  
  
6.  Usando o **Gerenciador de Cluster de Failover** se conectem a  ***appliance_domain*-WFOHST01** cluster, se conectado automaticamente e, em seguida, no painel de navegação, clique em **Funções**. No **funções** painel:  
  
    1.  Multisseleção de todas as máquinas virtuais. -Los e selecione **desligar**.  
  
    2.  Aguarde até que todas as máquinas virtuais selecionadas concluir o desligamento.  
  
7.  Se houver uma região de HDInsight:  
  
    1.  Conecte-se ao cluster HDInsight. Para fazer isso, clique duas vezes em **Gerenciador de Cluster de Failover**, selecione **conectar-se ao Cluster**e especifique  ***appliance_domain*-WFOHST02** o nome do cluster.  
  
    2.  Sob o cluster HDInsight, clique em **funções**. No **funções** painel:  
  
        1.  Multisseleção de todas as máquinas virtuais, eles e selecione **desligar**.  
  
        2.  Aguarde até que as máquinas virtuais desligar.  
  
8.  Fechar o **Gerenciador de Cluster de Failover** aplicativo.  
  
9. Desligar todos os servidores, exceto  ***appliance_domain*-HST01**.  
  
10. Desligar o  ***appliance_domain*-HST01** server.  
  
11. Desligue as unidades de distribuição de alimentação (PDUs).  
  
## <a name="PowerOn"></a>Ligar o dispositivo  
  
### <a name="to-power-on-the-appliance"></a>Para ligar o dispositivo  
  
> [!WARNING]  
> Todas as etapas devem ser executadas na ordem exata listada e cada etapa deve ser concluída para a próxima etapa é executada, a menos que indicado o contrário. Executar etapas fora de ordem ou sem aguardar concluir cada etapa pode resultar em erros de inicialização.  
  
1.  Ligue o unidades de distribuição de alimentação (PDU) e aguarde as opções para iniciar automaticamente.  
  
2.  Ligue o  ***appliance_domain*-HST01** server.  
  
3.  Faça logon no  ***appliance_domain*-HST01** como o administrador de domínio do dispositivo.  
  
4.  Iniciar o **Gerenciador Hyper-V** programa (**virtmgmt.msc**) e conecte-se ao  ***appliance_domain*-HST01** se não conectado por padrão.  
  
    1.  Se você não pode se conectar por nome porque a  ***PDW_region*-AD01** é não em execução, tente conectar-se usando o endereço IP.  
  
    2.  No **máquinas virtuais** painel, localize  ***PDW_region*-AD01** e confirme se ele está em execução. Caso contrário, inicie essa VM e aguarde até que ele seja totalmente iniciado.  
  
5.  Ligue o restante dos servidores no dispositivo.  
  
6.  Na **HST01** estiver conectado como administrador de domínio do dispositivo, no **Gerenciador Hyper-V**:  
  
    1.  Conecte-se ao  ***appliance_domain*-HST02**.  
  
    2.  No **máquinas virtuais** painel, localize  ***PDW_region*-AD02** e confirme se ele está em execução.  Caso contrário, inicie essa VM e aguarde até que ele seja totalmente iniciado.  
  
7.  Usando o **Gerenciador de Cluster de Failover** se conectem a  ***appliance_domain*-WFOHST01** de cluster, se conectado automaticamente e, em seguida, no  **Navegação** painel, clique em **funções**. No **funções** painel:  
  
    1.  Multisseleção de todas as máquinas virtuais, com o botão direito-las e, em seguida, clique em **iniciar**.  
  
    2.  Aguarde até que todas as máquinas virtuais selecionadas concluir a inicialização antes de prosseguir para a próxima etapa.  
  
    3.  Se for necessário para as VMs que falhou, fechá-los, movê-los e reiniciá-los no host principal adequado.  
  
8.  Se o dispositivo tem uma região de HDInsight, conecte-se ao cluster HDInsight. (Para fazer isso, clique duas vezes em **Gerenciador de Cluster de Failover**, selecione **conectar-se ao Cluster**e especifique  ***appliance_domain*-WFOHST01** o nome do cluster.)  
  
    1.  Sob o cluster HDInsight, clique em **funções**. No **funções** painel.  
  
        1.  Multisseleção de todas as máquinas virtuais, eles e selecione **iniciar**,  
  
        2.  Aguarde até que todas as máquinas virtuais selecionadas concluir a inicialização antes de prosseguir para a próxima etapa.  
  
        3.  Se for necessário para as VMs que falhou, fechá-los, movê-los e reiniciá-los no host principal adequado.  
  
9. Desconectar **HST01** se desejar.  
  
10. Conecte-se ao  ***PDW_region*-CTL01** usando a conta de administrador de domínio do dispositivo.  
  
11. Executar `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` para iniciar o **do Configuration Manager**.  
  
12. No **do Configuration Manager**, no **topologia de depósito de dados paralela** menu, clique no **Status de serviços** guia e, em seguida, clique em **iniciar região**para iniciar serviços do PDW.  
  
13. Se o dispositivo tiver uma região de HDInsight, no menu de topologia de HDInsight, clique o **Status de serviços** guia e, em seguida, clique em **iniciar região** para iniciar os serviços do HDInsight.  
  
### <a name="to-verify-the-appliance-health"></a>Para verificar a integridade do dispositivo  
Depois que o dispositivo foi iniciado, abra o **Console de administração** e verificar a página de integridade para alertas que indicam as condições de falha. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração &#40; Analytics Platform System &#41; ](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Consulte Também  
[Tarefas de gerenciamento de dispositivo &#40; Analytics Platform System &#41;](appliance-management-tasks.md)  
  
