---
title: Desinstalar o PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3941a2f0-0d0c-4d1a-8618-7a6a7751beac
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 49f29fe95801b792444dcd69edfc630b78fe580b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37970318"
---
# <a name="uninstall-power-pivot-for-sharepoint"></a>Desinstalar o Power Pivot para SharePoint
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Desinstalar uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] é uma operação de várias etapas que inclui a preparação para desinstalação, a remoção de recursos e soluções do farm e a remoção de arquivos de programas e configurações de registro.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **Neste artigo:**  
  
-   [Pré-requisitos](#prereq)  
  
-   [Etapa 1: lista de verificação pré-desinstalação](#bkmk_before)  
  
-   [Etapa 2: remover recursos e soluções do SharePoint](#bkmk_remove)  
  
-   [Etapa 3: executar a Instalação do SQL Server para remover programas do computador local](#bkmk_uninstall)  
  
-   [Etapa 4: desinstalar o suplemento do Power Pivot para SharePoint](#bkmk_addin)  
  
-   [Etapa 5: verificar a desinstalação](#verify)  
  
-   [Etapa 6: lista de verificação pós-desinstalação](#bkmk_post)  
  
##  <a name="prereq"></a> Pré-requisitos  
  
-   Você deve ser administrador de farm do SharePoint ou administrador de aplicativo de serviço para desinstalar recursos e soluções no farm.  
  
-   Você deverá ser um Administrador do Sistema do SQL Server e membro do grupo de administradores local se também estiver desinstalando o Mecanismo de Banco de Dados.  
  
-   Você deve ser um Administrador do Sistema do Analysis Services e membro do grupo administradores local para desinstalar o Analysis Services e o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].  
  
##  <a name="bkmk_before"></a> Etapa 1: lista de verificação pré-desinstalação  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] O acesso aos dados será desabilitado quando o software que dá suporte ao processamento de consulta e dados for removido do farm. A primeira etapa é excluir preventivamente arquivos e bibliotecas que não funcionarão mais. Isso permite que você solucione dúvidas ou preocupações sobre a ‘falta de dados’ antes de desinstalar o software.  
  
1.  Exclua todas as pastas de trabalho, documentos e bibliotecas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] com associação a uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Nenhuma das bibliotecas nem os documentos funcionarão depois que o software for desinstalado.  
  
    -   [Excluir Galeria do Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Excluir uma Biblioteca de Feeds de Dados Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
2.  Exclua pastas de trabalho do Excel ou relatórios do Reporting Services de outras bibliotecas que contenham ou façam referência a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
3.  Remova qualquer web part de um painel PerformancePoint que faça referência a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  Revise as permissões do SharePoint nos sites e bibliotecas existentes para determinar se é necessário alterá-las. Alguns cenários de acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , particularmente o acesso a dados secundários por meio de uma cadeia de conexão de URL a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em outra pasta de trabalho, exigem permissões de leitura, que é superior às permissões de exibição normalmente atribuídas aos usuários do SharePoint que apenas visitam um site. Se você não precisar mais de permissões de leitura, poderá reduzir as permissões de acordo.  
  
5.  Opcionalmente, interrompa os serviços e aguarde alguns dias antes de desinstalar o software. Essa etapa não é necessária na desinstalação, mas ela oferece a opção de retomar temporariamente o serviço, enquanto você tenta resolver problemas de migração de dados ou substituição de tecnologia que possam ter passado despercebidos.  
  
##  <a name="bkmk_remove"></a> Etapa 2: remover recursos e soluções do SharePoint  
 Use a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para remover os serviços e aplicativos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do SharePoint.  
  
-   Você deve ser um administrador de farm, um administrador do servidor na instância do Analysis Services e um **db_owner** no banco de dados de configuração do farm.  
  
-   Use a versão apropriada da ferramenta de configuração para a versão do SharePoint. Não use a ferramenta com instalações do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] .  
  
-   Verifique se o serviço Administração do SharePoint está em execução.  
  
1.  **Executar a ferramenta de configuração:** observe que as ferramentas de configuração são listadas somente quando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] está instalado no servidor local. No menu **Iniciar** , aponte para **Todos os Programas**, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], em **Ferramentas de Configuração**e clique em uma das seguintes opções:  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para configuração do SharePoint 2013**  
  
    -   **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Ferramenta de Configuração**  
  
2.  Selecione **Remover Recursos, Serviços, Aplicativos e Soluções** e clique em **OK**.  
  
3.  Opcionalmente, expanda a janela para o tamanho total. Você verá uma barra de botões na parte inferior da janela que inclui os comandos **Validar**, **Executar**e **Sair** .  
  
4.  Revise cada ação da lista de tarefas para entender o que faz cada uma delas.  
  
     Em **Remover Aplicativos de Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, você tem a opção de excluir dados associados ao aplicativo de serviço. Os dados do aplicativo são um banco de dados do SQL Server que foi criado com o aplicativo de serviço com a finalidade de armazenar agendas de atualização de dados, informações de instância de banco de dados, dados de uso e outros dados usados pelo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Ele não armazena arquivos de usuário, como pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . A menos que você tenha uma razão específica para manter os dados do aplicativo (por exemplo, se você tiver políticas de retenção de dados relacionadas à atualização de dados ou ao acesso aos dados), você poderá excluir o banco de dados do aplicativo sem remover nenhum arquivo criado ou salvo por usuários do SharePoint.  
  
     Para excluir o banco de dados, selecione **Remover Aplicativos de Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** e selecione **Exclua dados de aplicativo associados a este aplicativo de serviço**.  
  
5.  Opcionalmente, revise as informações detalhadas na guia **Saída** ou na guia **Script** .  
  
     A guia Saída é um resumo das ações que serão executadas pela ferramenta. Essas informações são salvas em arquivos de log em:  
  
     `C:\Program Files\Microsoft SQL Server\130\Tools\PowerPivotTools\SPAddinConfiguration\Log`  
  
     A guia Script mostra os cmdlets PowerShell ou referencia os arquivos de script PowerShell que serão executados pela ferramenta.  
  
6.  Clique em **Validar** para verificar se cada ação é válida. Se **Validar** não estiver disponível, isso indicará que todas as ações são válidas para o sistema.  
  
7.  Clique em **Executar** para executar todas as ações válidas para esta tarefa. **Executar** estará disponível apenas depois que a verificação da validação tiver sido aprovada. Quando você clica em **Executar**, o seguinte aviso é exibido, lembrando a você que as ações são processadas em modo de lote: "Todos os parâmetros da configuração sinalizados como válidos na ferramenta serão aplicados ao farm do SharePoint. Deseja continuar?"  
  
8.  Clique em **Sim** para continuar.  
  
 **Solucionando erros:**  
  
 Na ferramenta de configuração, você pode exibir informações de erro no painel Parâmetros de cada ação. Para problemas relacionados à implantação ou retração da solução, verifique se o serviço Administração do SharePoint foi iniciado. Esse serviço executa os trabalhos de timer que disparam alterações na configuração em um farm. Se o serviço não estiver em execução, a implantação ou a retração da solução apresentará falha. Erros persistentes indicam que um trabalho de implantação ou retração existente já está na fila e bloqueando ação adicional da ferramenta de configuração. Você pode usar o seguinte comando do PowerShell para verificar se o serviço está sendo executado.  
  
```  
Get-Service | where {$_.displayname -like "*sharepoint* administration*"}  
```  
  
 Para localizar e remover um trabalho de implantação ou retração que já esteja na fila, proceda da seguinte maneira:  
  
1.  Para todos os outros erros, verifique os logs ULS. Para obter informações, veja [Configurar e exibir arquivos de log do SharePoint e log de diagnósticos &#40;Power Pivot para SharePoint&#41;](~/analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
2.  Inicie o Shell de Gerenciamento do SharePoint como administrador e execute o comando a seguir para exibir os trabalhos na fila:  
  
    ```  
    Stsadm –o enumdeployments  
    ```  
  
3.  Reveja as implantações existentes para obter as seguintes informações: **Tipo** é Retração ou Implantação, **Arquivo** é powerpivotwebapp.wsp ou powerpivotfarm.wsp.  
  
4.  Para implantações ou retrações relacionadas a soluções [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , copie o valor do GUID de **JobId** e cole-o no seguinte comando (use os comandos Marcar, Copiar e Colar no menu Editar do Shell para copiar o GUID):  
  
    ```  
    Stsadm –o canceldeployment –id “<GUID>”  
    ```  
  
5.  Tente a tarefa novamente na ferramenta de configuração clicando em **Validar** e, em seguida, em **Executar**.  
  
 Opcionalmente, você pode usar o PowerShell para remover recursos e soluções do farm. Para obter mais informações, consulte [Referência do PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_uninstall"></a> Etapa 3: executar a Instalação do SQL Server para remover programas do computador local  
 A exclusão de arquivos de programa requer que você execute a Instalação do SQL Server para desinstalar o software. A desinstalação remove os arquivos e as entradas de registro criadas pela Instalação. Você pode usar a página Programas e Recursos para desinstalar o software. Uma instalação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] faz parte de uma instalação do SQL Server.  
  
 Você pode desinstalar parte de uma instalação sem afetar outras instâncias do SQL Server (ou recursos na mesma instância) que já estejam instaladas. Por exemplo, você pode desinstalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint e manter outros componentes, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou Mecanismo de Banco de Dados, instalados.  
  
1.  Selecione **Microsoft SQL Server 2014 (64 bits)** na lista de programas.  
  
2.  Clique em **Desinstalar/Alterar**.  
  
3.  Clique em **Remover**. Isso inicia a Instalação do SQL Server.  
  
     Na Instalação, você pode selecionar a instância do **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** e as opções **Analysis Services** e **Integração com o SharePoint do Analysis Services** para remover apenas esse recurso, deixando os demais itens inalterados.  
  
##  <a name="bkmk_addin"></a> Etapa 4: desinstalar o suplemento do Power Pivot para SharePoint  
 Se sua implantação do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] tem dois ou mais servidores e você instalou o Suplemento do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] , desinstale o suplemento do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] de cada servidor em que ele foi instalado para desinstalar completamente todos os arquivos do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Para obter informações, veja [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
##  <a name="verify"></a> Etapa 5: verificar a desinstalação  
  
1.  Na Administração Central, em **Gerenciar serviços no servidor**, conecte-se ao servidor do qual você desinstalou o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
2.  -   Se você desinstalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013, verifique se o **Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do SQL Server** não aparece mais na lista.  
  
    -   Se você desinstalou o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010, verifique se o **SQL Server Analysis Services** e o **Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do SQL Server** não aparecem mais na lista.  
  
3.  Depois de desinstalar o último servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no farm, faça o seguinte:  
  
    1.  Em Gerenciamento de Aplicativos, em **Gerenciar aplicativos de serviço**, verifique se o aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não aparece mais na lista.  
  
    2.  Em Configurações do Sistema, em **Gerenciar recursos do farm**, verifique se o Recurso de Integração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não está mais na página. Em **Gerenciar soluções do farm**, verifique se as soluções do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não aparecem mais na página.  
  
    3.  Em Monitoração, em **Configurar log de diagnóstico** e em **Configurar uso e coleta de dados de integridade**, verifique se os eventos e as categorias de evento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não aparecem mais.  
  
    4.  Em Configurações Gerais do Aplicativo, verifique se o **Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** não está mais na página.  
  
##  <a name="bkmk_post"></a> Etapa 6: lista de verificação pós-desinstalação  
 Use a lista a seguir para remover o software e os arquivos que não foram excluídos durante a desinstalação.  
  
1.  Exclua todos os arquivos de dados e as subpastas de `C:\Program Files\Microsoft SQL Server\MSAS13.PowerPivot`e depois exclua a pasta. Essa etapa também exclui arquivos armazenados em cache anteriormente no diretório DATA.  
  
2.  Exclua todas as pastas de trabalho, documentos e bibliotecas do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] caso ainda não o tenha feito.  
  
    -   [Excluir Galeria do Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-power-pivot-gallery.md)  
  
    -   [Excluir uma Biblioteca de Feeds de Dados Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)  
  
3.  No Serviço de Repositório Seguro, exclua os aplicativos de destino que contêm credenciais armazenadas usadas pelo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Algumas entradas, mas não todas, no Serviço de Repositório Seguro são excluídas quando você desinstala o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Os aplicativos de destino criados para a conta de atualização de dados autônoma do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , além dos aplicativos de destino criados para atualização de dados, ainda existem e devem ser excluídos manualmente.  
  
     Por outro lado, os aplicativos de destino individuais que foram gerados automaticamente pelo Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serão excluídos automaticamente quando o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for desinstalado.  
  
4.  No Painel de Controle, clique em **Programas**e em **Desinstalar um programa** Desinstale qualquer biblioteca cliente do Analysis Services que não estiver mais sendo usada. O Analysis Services ADOMD.NET e os Objetos de Gerenciamento de Análise do Microsoft SQL Server não são removidos quando você desinstala o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Como as bibliotecas podem ser usadas por outro programa que utiliza dados do Analysis Services, a Instalação do SQL Server não as desinstala automaticamente. Você deverá desinstalar essas bibliotecas de cliente individualmente se não precisar mais delas.  
  
     Não desinstale o Suplemento do SQL Server Reporting Services SharePoint 2010 a menos que esteja seguindo instruções de solução de problemas ou de instalação que o instruem especificamente a desinstalá-lo. O Suplemento Reporting Services é usado pelo Access Services. É instalado pela ferramenta Preparação de Produtos do SharePoint 2010 e deve permanecer no sistema para oferecer suporte à funcionalidade exigida pelo SharePoint.  
  
     Não instale o provedor OLE DB do Analysis Services. O SharePoint instala o provedor OLE DB como pré-requisito para as pastas de trabalho do Excel que se conectam a bancos de dados do Analysis Services. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] instala uma versão mais recente, mas essa versão é compatível com versões anteriores para você deixar o sistema encarregado de evitar problemas com conexão de dados mais tarde.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Ferramentas de Configuração do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
  
