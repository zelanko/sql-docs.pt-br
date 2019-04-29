---
title: Baixar atualizações da Microsoft - Analytics Platform System | Microsoft Docs
description: Este tópico discute como baixar atualizações do catálogo do Microsoft Update para o Windows Server Update Services (WSUS) e aplicar essas atualizações para os servidores de dispositivo do Analytics Platform System. Microsoft Update instalará todas as atualizações aplicáveis do Windows e o SQL Server. O WSUS está instalado na máquina virtual VMM do dispositivo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d71a6ddc965b422f0f96f40788352213501b4db2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042288"
---
# <a name="download-and-apply-microsoft-updates-for-analytics-platform-system"></a>Baixe e aplique as atualizações da Microsoft para o Analytics Platform System
Este tópico discute como baixar atualizações do catálogo do Microsoft Update para o Windows Server Update Services (WSUS) e aplicar essas atualizações para os servidores de dispositivo do Analytics Platform System. Microsoft Update instalará todas as atualizações aplicáveis do Windows e o SQL Server. O WSUS está instalado na máquina virtual VMM do dispositivo.  
  
## <a name="TOP"></a>Antes de começar  
  
> [!WARNING]  
> Não tente aplicar atualizações se seu dispositivo ou qualquer componente do dispositivo está inativo ou em uma falha ao longo de estado. Nesse caso, contate o suporte para obter assistência.  
>   
> Não aplique Microsoft Updates enquanto o dispositivo está em uso. Aplicação de atualizações pode causar a nós de dispositivo a reinicialização. As atualizações devem ser aplicadas durante uma janela de manutenção quando o dispositivo não está sendo usado.  
  
### <a name="prerequisites"></a>Prerequisites  
Antes de executar essas etapas, você precisa:  
  
-   Configurar o WSUS em seu dispositivo seguindo as instruções em [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
-   Conhecimento de informações de logon de conta um administrador de domínio de malha.  
  
-   Ter um logon com permissões para acessar o Console de administração do sistema de plataforma de análise e exibir informações de estado do dispositivo.  
  
-   Na maioria dos casos, o WSUS precisa acessar servidores fora do dispositivo. Para dar suporte a esse cenário de uso que o sistema de plataforma de análise de DNS pode ser configurado para dar suporte a um encaminhador de nome externo que permitirá que o Analytics Platform System hosts e máquinas virtuais (VMs) usar servidores DNS externos para resolver nomes fora das dispositivo. Para obter mais informações, consulte [usar um encaminhador DNS para resolver nomes de DNS não são de dispositivo &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
## <a name="bkmk_ImportUpdates"></a>Para baixar e aplicar as atualizações da Microsoft  
  
#### <a name="verify-the-appliance-state-indicators"></a>Verifique se os indicadores de estado do dispositivo  
  
1.  Abra o Console do administrador e navegue até a página de estado do dispositivo. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
2.  Verifique se os indicadores de status para todos os nós no estado do dispositivo.  
  
    -   É seguro continuar com indicadores NA ou verde.  
  
    -   Avalie os erros não críticos de aviso (amarelo). Em alguns casos as mensagens de aviso não bloqueará as atualizações. Se houver um erro de volume de disco não críticos que não está na unidade C:\, você pode prosseguir para a próxima etapa antes de resolver o erro de volume de disco.  
  
    -   A maioria dos indicadores vermelhos devem ser resolvidos antes de continuar. Se houver falhas de disco, use a página de alertas do Console de administrador para verificar se não há não mais de uma falha de disco em cada servidor ou uma matriz de SAN. Se houver falha de não mais de um disco em cada servidor ou uma matriz de SAN, você pode prosseguir para a próxima etapa antes de corrigir as falhas de disco. Certifique-se de entrar em contato com o suporte da Microsoft para corrigir as falhas de disco mais rápido possível.  
  
#### <a name="synchronize-the-wsus-server"></a>Sincronizar o servidor do WSUS  
  
1.  Faça logon máquina virtual do VMM como um administrador de domínio.  
  
2.  No **painel do Gerenciador do servidor**diante a **ferramentas** menu, clique em **Windows Server Update Services** (**wsus.msc**).  
  
3.  No Console de administração do WSUS, clique em **sincronizações**.  
  
4.  Se a sincronização não está em execução, clique em **sincronizar agora** no painel direito. No painel inferior, haverá um status de sincronização. Aguarde até que a sincronização foi concluída.  
  
#### <a name="approve-microsoft-updates-in-wsus"></a>Aprovar atualizações da Microsoft no WSUS  
  
1.  No painel esquerdo do console do WSUS, clique em **todas as atualizações**.  
  
2.  No **todas as atualizações** painel, clique no **aprovação** menu suspenso, defina **aprovação** para **qualquer exceto recusada**. Clique o **Status** menu suspenso, defina **Status** para **qualquer**. Clique em **Atualizar**.  
  
    Clique com botão direito do **Title** coluna e selecione **Status do arquivo** para verificar o status do arquivo após a conclusão do download.  
  
    Você também pode selecionar **atualizações críticas** ou **atualizações de segurança** à esquerda painel e o modo de exibição disponíveis atualizações para essas categorias.  
  
    ![Selecione todas as atualizações e altere o status para qualquer. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectAllUpdates.png "SQL_Server_PDW_WSUSSelectAllUpdates")  
  
3.  Selecione todas as atualizações e, em seguida, clique no **aprovar** link no painel direito.  
  
    Você pode também com o botão direito nas atualizações selecionadas e, em seguida, clique em **aprovar**. Você será solicitado a aceitar "Microsoft Software License Terms". Nesse caso, clique em **aceito** na janela para continuar.  
  
    ![Selecione todas as atualizações que se aplicam e clique em Aprovar. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprove.png "SQL_Server_PDW_WSUSSelectApprove")  
  
4.  Selecione o grupo de servidores de dispositivo que você criou na [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  Clique em **aprovadas para instalação**e, em seguida, clique em **Okey**.  
  
    ![Aprove atualizações para seu grupo de computadores. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSSelectApprovalType.png "SQL_Server_PDW_WSUSSelectApprovalType")  
  
6.  No **progresso da aprovação** caixa de diálogo, quando o processo de aprovação for concluído, clique em **fechar**.  
  
    ![Feche a janela quando as atualizações são aprovadas. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUSCloseApprovalProgressWindow.png "SQL_Server_PDW_WSUSCloseApprovalProgressWindow")  
  
#### <a name="verify-that-the-updates-are-in-wsus"></a>Verifique se as atualizações no WSUS  
  
-  Verifique se o status de todas as atualizações do arquivo. Cada arquivo deve ter um ícone de seta verde à esquerda do título. Isso indica que o arquivo está pronto para instalação.  
  
    ![Status do arquivo for bem-sucedido](./media/download-and-apply-microsoft-updates/SQL_Server_PDW_WSUS_File_Status.png "SQL_Server_PDW_WSUS_File_Status")  
  
    Antes de instalar as atualizações, certifique-se de que eles estão todos baixado e disponível no console do WSUS.  
  
#### <a name="to-verify-that-all-updates-are-downloaded"></a>Para verificar se todas as atualizações são baixadas  
  
-  Verifique as **Status do Download** de atualizações no console do WSUS, conforme mostrado na seguinte captura de tela. Verifique se **atualizações que precisam de arquivos** é 0 para confirmar que todas as atualizações são baixadas. Se esse número for maior que zero, você precisa voltar e aprovar atualizações adicionais.  
  
    ![Verifique se que todas as atualizações são baixadas. ](./media/download-and-apply-microsoft-updates/SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG.png "SQL_Server_PDS_WSUS_VerifyDownloadUpdateJPG")  
  
#### <a name="apply-microsoft-updates"></a>Aplicar atualizações da Microsoft  
  
1.  Antes de começar, abra o [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md), clique no **estado de dispositivo** guia e, em seguida, verifique o  **Cluster** e **rede** colunas Mostrar verde (ou NA) para todos os nós. Se todos os alertas existirem em qualquer uma dessas colunas, o dispositivo não poderá instalar atualizações corretamente. Lidar com todos os alertas existentes na **Cluster** e **rede** colunas antes de continuar.  
  
2.  Faça logon na _< nome_do_domínio >_**-HST01** nó como o administrador de domínio do Fabric.  
  
3.  Para aplicar todas as atualizações aprovadas para o WSUS, execute o programa de atualização. Ver [execute o programa de atualização](#RunUpdateWizard) abaixo para obter instruções.  
  
#### <a name="verify-the-updates-on-all-nodes"></a>Verifique se as atualizações em todos os nós  
  
1.  O nó do VMM, inicie o Console de administração do WSUS. Este aplicativo pode ser encontrado na **inicie**, **ferramentas administrativas**, **Windows Server Update Services**.  
  
2.  Expandir **computadores**.  
  
3.  Expandir **todos os computadores**.  
  
4.  Selecione o grupo de servidores de dispositivo que você criou na [configurar o Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md).  
  
5.  No **Status** menu suspenso, selecione **qualquer** e clique em **atualizar**.  
  
6.  Expandir **serviços de atualização**, *<appliance name>*- VMM, **atualizações**, **todas as atualizações**, onde *<appliance name>* é o nome do dispositivo.  
  
7.  No **todas as atualizações** janela conjunto **aprovação** para **qualquer exceto recusada**.  
  
8.  No **todas as atualizações** janela, defina **Status** para **falharam ou necessárias**.  
  
9. Clique em **Atualizar**.  
  
10. Se **as atualizações necessárias** é maior que zero, contate o suporte para obter assistência.  
  
#### <a name="ensure-there-are-no-critical-alerts-in-the-sql-server-pdw-admin-console"></a>Verifique se que não existem alertas críticos no Console de administração do SQL Server PDW  
  
1.  Abra o Console de administração, clique na guia de estado do dispositivo. Ver [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).  
  
2.  Verifique se que o **Cluster** e **rede** colunas Mostrar verde (ou NA) para todos os nós. Se todos os alertas existirem em qualquer uma dessas colunas, o dispositivo não poderá instalar atualizações corretamente. Contate o suporte se há alertas críticos.  
  
## <a name="RunUpdateWizard"></a>Execute o programa de atualização  
Siga estas instruções para executar o programa de atualização do sistema de plataforma de análise.  
  
> [!NOTE]  
> O sistema do WSUS foi projetado para execução assíncrona pode levar algum tempo para aplicar completamente todas as atualizações. Iniciar uma atualização agenda uma atualização, mas não garante a atividade de atualização imediata.  
  
1.  Verifique se que você está conectado ao nó HST01 como administrador de domínio do Fabric.  
  
2.  Abra uma janela de Prompt de comando e digite os seguintes comandos. Substitua *<parameter>* com as informações designadas.  
  
**Para executar o Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="MicrosoftUpdate" /DomainAdminPassword="<password>"  
```  
  
**Para relatar o status do Microsoft Update:**  
  
```  
C:\pdwinst\media\setup.exe /action="ReportMicrosoftUpdateClientStatus" /DomainAdminPassword="<password>"  
```  
  
## <a name="see-also"></a>Consulte também  
[Desinstalar atualizações da Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Desinstalar Hotfixes do Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Manutenção de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
