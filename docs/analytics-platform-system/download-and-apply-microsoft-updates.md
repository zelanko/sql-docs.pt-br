---
title: Baixar atualizações da Microsoft
description: Este tópico discute como baixar atualizações do catálogo Microsoft Update para o Windows Server Update Services (WSUS) e aplicar essas atualizações aos servidores do dispositivo do Analytics Platform System. Microsoft Update instalará todas as atualizações aplicáveis para o Windows e o SQL Server. O WSUS é instalado na máquina virtual do VMM do dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e5f336c3c2c475523d2081bcf01189e67b77fe19
ms.sourcegitcommit: ce15cbbcb0d5f820f328262ff5451818e508b480
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94947911"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Baixar e aplicar atualizações da Microsoft para o Analytics Platform System
Este tópico discute como baixar atualizações do catálogo Microsoft Update para o Windows Server Update Services (WSUS) e aplicar essas atualizações aos servidores do dispositivo do Analytics Platform System. Microsoft Update instalará todas as atualizações aplicáveis para o Windows e o SQL Server. O WSUS é instalado na máquina virtual do VMM do dispositivo.  
  
## <a name="before-you-begin"></a><a name="TOP"></a>Antes de começar  
  
> [!WARNING]  
> Não tente aplicar atualizações se seu dispositivo ou qualquer componente de dispositivo estiver inoperante ou em um estado de failover. Nesse caso, entre em contato com o suporte para obter assistência.  
>   
> Não aplique atualizações da Microsoft enquanto o dispositivo estiver em uso. A aplicação de atualizações pode fazer com que os nós do dispositivo reiniciem. As atualizações devem ser aplicadas durante uma janela de manutenção quando o dispositivo não está sendo usado.  
  
### <a name="prerequisites"></a>Pré-requisitos  
Antes de executar essas etapas, você precisa:  
  
-   Configure o WSUS em seu dispositivo seguindo as instruções em [Configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conhecimento de uma conta de administrador de domínio da malha informações de logon.  
  
-   Ter um logon com permissões para acessar o console de administração do sistema da plataforma de análise e exibir informações de estado do dispositivo.  
  
-   Na maioria dos casos, o WSUS precisa acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso, o DNS do sistema da plataforma de análise pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que os hosts do sistema da plataforma de análise e VMs (máquinas virtuais) usem servidores DNS externos para resolver nomes fora do dispositivo. Para obter mais informações, consulte [usar um encaminhador DNS para resolver nomes DNS que não são de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="to-download-and-apply-microsoft-updates"></a><a name="bkmk_ImportUpdates"></a>Para baixar e aplicar atualizações da Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Verificar os indicadores de estado do dispositivo  
  
1.  Abra o console do administrador e navegue até a página estado do dispositivo. Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Verifique os indicadores de status de todos os nós no estado do dispositivo.  
  
    -   É seguro continuar com indicadores verdes ou NA.  
  
    -   Avalie erros de aviso não críticos (amarelos). Em alguns casos, as mensagens de aviso não bloquearão as atualizações. Se houver um erro de volume de disco não crítico que não esteja em C:\ , você pode prosseguir para a próxima etapa antes de resolver o erro de volume de disco.  
  
    -   A maioria dos indicadores vermelhos deve ser resolvida antes de continuar. Se houver falhas de disco, use a página de alertas do console de administração para verificar se não há mais de uma falha de disco em cada servidor ou matriz SAN. Se não houver mais de uma falha de disco em cada servidor ou matriz SAN, você poderá prosseguir para a próxima etapa antes de corrigir as falhas de disco. Lembre-se de entrar em contato com o suporte da Microsoft para corrigir as falhas de disco assim que possível.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizar o servidor do WSUS  
  
1.  Faça logon na máquina virtual do VMM como um administrador de domínio.  
  
2.  No **painel de Gerenciador do servidor**, no menu **ferramentas** , clique em **Windows Server Update Services** (**WSUS. msc**).  
  
3.  No console de administração do WSUS, clique em **sincronizações**.  
  
4.  Se a sincronização não estiver em execução, clique em **sincronizar agora** no painel à direita. No painel inferior, haverá um status de sincronização. Aguarde até que a sincronização seja concluída.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Aprovar atualizações da Microsoft no WSUS  
  
1. Recusar quaisquer pacotes cumulativos de atualizações que não sejam do **System Center**.

2. No painel esquerdo, no console do WSUS, clique em **todas as atualizações**.  
  
3.  No painel **todas as atualizações** , clique no menu suspenso **aprovação** , defina **aprovação** como qualquer, **exceto recusada**. Clique no menu suspenso **status** , defina **status** como **any**. Clique em **Atualizar**.  
  
    Clique com o botão direito do mouse na coluna **título** e selecione **status do arquivo** para verificar o status do arquivo após a conclusão do download.  
  
    Você também pode selecionar atualizações **críticas** ou **atualizações de segurança** no painel esquerdo e exibir as atualizações disponíveis para essas categorias.  
  
    ![Selecione todas as atualizações e altere o status para Qualquer.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
4.  Selecione todas as atualizações e, em seguida, clique no link **aprovar** no painel direito.  
  
    Você também pode clicar com o botão direito do mouse nas atualizações selecionadas e, em seguida, clicar em **aprovar**. Você pode ser solicitado a aceitar os "termos de licença para software Microsoft". Nesse caso, clique em **aceito** na janela para continuar.  
  
    ![Selecione todas as atualizações aplicáveis e clique em Aprovar.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
5.  Selecione o grupo de servidores de dispositivo que você criou em [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
6.  Clique **Aprovado para Instalação** e clique em **OK**.  
  
    ![Aprove as atualizações do seu grupo de computadores.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
7.  Na caixa de diálogo **progresso da aprovação** , quando o processo de aprovação estiver concluído, clique em **fechar**.  
  
    ![Feche a janela quando as atualizações forem aprovadas.](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Verificar se as atualizações estão no WSUS  
  
-  Verifique o status do arquivo de todas as atualizações. Cada arquivo precisa ter um ícone de seta verde à esquerda do título. Isso indica que o arquivo está pronto para instalação.  
  
    ![Status de arquivo bem-sucedido](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Antes de instalar as atualizações, verifique se elas estão todas baixadas e disponíveis no console do WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Para verificar se todas as atualizações foram baixadas  
  
-  Verifique o **status de download** das atualizações no console do WSUS, conforme mostrado na captura de tela a seguir. Verifique se as **atualizações que precisam de arquivos** são 0 para confirmar se todas as atualizações foram baixadas. Se esse número for maior que zero, talvez seja necessário voltar e aprovar atualizações adicionais.  
  
    ![Verificar se todas as atualizações foram baixadas.](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Aplicar atualizações da Microsoft  
  
1.  Antes de começar, abra o [utilitário monitorar o dispositivo usando o console de administração &#40;&#41;do sistema de plataforma de análise](monitor-the-appliance-by-using-the-admin-console.md), clique na guia **estado do dispositivo** e verifique se as colunas do **cluster** e da **rede** mostram verde (ou na) para todos os nós. Se houver alertas em uma dessas colunas, o dispositivo poderá não ser capaz de instalar as atualizações corretamente. Resolva todos os alertas existentes nas colunas de **rede** e de **cluster** antes de continuar.  
  
2.  Faça logon no nó _<domain_name>_ **-HST01** como administrador de domínio de malha.  
  
3.  Para aplicar todas as atualizações aprovadas para o WSUS, execute o programa de atualização. Consulte [executar o programa de atualização](#RunUpdateWizard) abaixo para obter instruções.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Verificar as atualizações em todos os nós  
  
1.  No nó do VMM, inicie o console de administração do WSUS. Esse aplicativo pode ser encontrado em **Iniciar**, **Ferramentas administrativas** **Windows Server Update Services**.  
  
2.  Expanda **computadores**.  
  
3.  Expanda **todos os computadores**.  
  
4.  Selecione o grupo de servidores de dispositivo que você criou em [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  No menu suspenso **status** , selecione **qualquer** e clique em **Atualizar**.  
  
6.  Expanda **serviços de atualização**, *<appliance name>* -VMM, **atualizações**, **todas as atualizações**, em que *<appliance name>* é o nome do dispositivo.  
  
7.  Na janela **todas as atualizações** , defina **aprovação** como **qualquer, exceto recusada**.  
  
8.  Na janela **todas as atualizações** , defina **status** como **falha ou necessário**.  
  
9. Clique em **Atualizar**.  
  
10. Se **as atualizações necessárias** forem maiores que zero, entre em contato com o suporte para obter assistência.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Verifique se não há alertas críticos no console do administrador do SQL Server PDW  
  
1.  Abra o console do administrador, clique na guia estado do dispositivo. Consulte [monitorar o dispositivo usando o console de administração &#40;&#41;do sistema de plataforma de análise ](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Verifique se as colunas de **rede** e de **cluster** mostram verde (ou na) para todos os nós. Se houver alertas em uma dessas colunas, o dispositivo poderá não ser capaz de instalar as atualizações corretamente. Contate o suporte se houver alertas críticos.  
  
## <a name="run-the-update-program"></a><a name="RunUpdateWizard"></a>Executar o programa de atualização  
Siga estas instruções para executar o programa de atualização do sistema da plataforma de análise.  
  
> [!NOTE]  
> O sistema WSUS é projetado para ser executado de forma assíncrona pode levar algum tempo para aplicar totalmente todas as atualizações. Iniciar uma atualização agenda uma atualização, mas não garante a atividade de atualização imediata.  
  
1.  Verifique se você está conectado ao nó HST01 como o administrador de domínio de malha.  
  
2.  Abra uma janela de prompt de comando e insira os comandos a seguir. Substituir *<parameter>* pelas informações designadas.  
  
**Para executar o Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Para relatar o status de Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Consulte Também  
[Desinstalar o Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar hotfixes do sistema de plataforma de análise &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Desinstale os hotfixes do Analytics Platform System &#40;o Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;o sistema de plataforma de análise&#41;](software-servicing.md)  
  
