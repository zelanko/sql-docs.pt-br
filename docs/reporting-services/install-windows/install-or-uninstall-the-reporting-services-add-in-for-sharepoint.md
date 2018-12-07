---
title: Instalar ou desinstalar o suplemento Reporting Services para SharePoint | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.assetid: c2804a9a-08ea-4f4a-805d-a2c19c68733d
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 55c88749d84290636fd6a9fc3ac3866f5499450f
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711607"
---
# <a name="install-or-uninstall-the-reporting-services-add-in-for-sharepoint"></a>Instalar ou desinstalar o suplemento Reporting Services para SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  Execute o pacote de instalação do Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint (rsSharePoint.msi) em servidores do SharePoint para habilitar recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma implantação do SharePoint. Os recursos incluem o Power View, uma Web Part do Visualizador de Relatórios, um ponto de extremidade de proxy de URL, tipos de conteúdo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e páginas de aplicativos para que você possa criar, exibir e gerenciar relatórios, modelos de relatórios, fontes de dados e outro conteúdo do servidor de relatório em um site do SharePoint. O Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint é um componente necessário para um servidor de relatório executado no modo do SharePoint. O suplemento pode ser instalado por meio do assistente de configuração do SQL Server 2016 ou baixando o rsSharePoint.msi do feature pack do SQL Server 2016. Para obter uma lista das versões do suplemento e páginas de download, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
##  <a name="bkmk_prereq"></a> Pré-requisitos  
 A instalação do Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é uma das várias etapas necessárias para a integração de um servidor de relatório a uma instância de um produto do SharePoint. Para obter mais informações sobre a instalação e a configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).  
  
-   Se você estiver integrando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a um farm do SharePoint que tenha vários aplicativos front-end da Web, instale o suplemento para cada computador no farm que tenha um front-end de servidor Web. Faça isso somente para front-ends da Web que serão usados para acessar conteúdo do servidor de relatório.  
  
-   Para instalar o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você deve ser um administrador no computador. Por exemplo, se você for executar o rsSharePoint.msi no prompt de comando, deverá abrir o prompt de comando com privilégios de administrador usando a opção **Executar como administrador** .  
  
-   Para instalar o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , você deve ser membro do grupo de Administradores do Farm do SharePoint.  
  
-   Você deve ser um administrador da coleção de sites para ativar o recurso de integração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .   
  
##  <a name="bkmk_whatinstalled"></a> O que o suplemento instala?  
 O processo de instalação do suplemento é composto de duas fases, ambas são concluídas automaticamente ao concluir uma instalação padrão:  
  
-   A primeira fase é instalar arquivos nas pastas apropriadas. As pastas são padrão para implantações do SharePoint. Um dos arquivos instalado é o rsCustomAction.exe.  
  
-   A segunda parte da instalação é a execução de um conjunto de ações personalizadas para registrar os arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com o SharePoint. As ações personalizadas são executadas do rsCustomAction.exe. O exe é removido quando as duas fases de instalação são totalmente concluídas. Você pode executar uma instalação **somente arquivos** ; o rsCustomAction.exe não é executado ao término da instalação e é deixado na unidade.  
  
## <a name="the-reporting-services-installation-order"></a>A ordem de instalação do Reporting Services  
 O suplemento pode ser instalado antes ou depois da instalação do SharePoint. O suplemento segue padrões de pré-implantação do SharePoint e instala arquivos em locais usados pela instalação do SharePoint.  
  
> [!NOTE]  
>  A vantagem da instalação do suplemento antes do produto do SharePoint é que, à medida que novos servidores forem adicionados ao farm, o Suplemento Reporting Services será configurado e ativado pelo farm do SharePoint.  
  
##  <a name="bkmk_3ways_to_install"></a> Visão geral dos métodos de instalação  
 O Suplemento SQL Server 2016 Reporting Services para produtos do SharePoint pode ser instalado usando um dos dois seguintes métodos:  
  
-   **O assistente de instalação:** ![note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "note") No SQL Server 2016, o suplemento pode ser instalado pelo assistente de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Escolha **suplemento Reporting Services para produtos do SharePoint** na página **Seleção de recursos** do assistente.  
  
-   **rsSharepoint.msi:** o suplemento pode ser instalado diretamente da mídia de instalação ou baixado e instalado. O rsSharepoint.msi dá suporte à interface gráfica do usuário e à instalação pela linha de comando. Para executar o .msi com privilégios de administrador, abra primeiro um prompt de comando com permissões elevadas e execute o rsSharepoint.msi na linha de comando. Para obter mais informações sobre como baixar o suplemento, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
    > [!NOTE]  
    >  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
##  <a name="bkmk_install_rssharepoint"></a> Instalar o suplemento usando o arquivo de instalação rsSharePoint.msi  
 Esta seção trata da instalação do rssharepoint.msi diretamente, executando o assistente de instalação .msi ou uma instalação de linha de comando. Se você instalou o suplemento usando o assistente de instalação do SQL Server, não precisará seguir estas etapas.  
  
 Você pode ver uma lista completa de opções de linha de comando executando o seguinte comando:  
  
```  
Rssharepoint.msi /?  
```  
  
1.  Baixe e execute o programa de Instalação (**rsSharepoint.msi**) para o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações sobre como baixar o suplemento, veja [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
2.  Como administrador, execute **rsSharepoint.msi** para executar o Assistente de Instalação. O assistente exibe uma página de boas-vindas, os termos de licença do software e uma página de informações sobre o registro. A instalação cria pastas no seguinte caminho e copia arquivos nas pastas:  
  
     `%program files%\common files\Microsoft Shared\Web Server Extensions\15\` (SharePoint 2013)
  
     ou em  
  
     `%program files%\common files\Microsoft Shared\Web Server Extensions\16\` (SharePoint 2016)  
  
3.  Configure as definições do servidor de relatório e a ativação de recursos na Administração Central do SharePoint. para obter informações sobre a ferramenta de configuração e recursos adicionais. Para obter mais informações sobre a instalação e a configuração do modo do SharePoint do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).  
  
###  <a name="bkmk_files_only_installation"></a> Instalação somente de arquivos  
 Para instalar os arquivos, mas ignorar a fase de ações personalizadas da instalação, execute o rssharepoint.msi na linha de comando com a opção SKIPCA.  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i rsSharePoint.msi SKIPCA=1  
    ```  
  
 A interface do usuário de instalação abrirá e executará como normal e o arquivo **rsCustomAction.exe** será instalado. Porém, o .exe não executará no final da instalação e o **rsCustomAction.exe** permanecerá no computador quando a instalação tiver sido concluída.  
  
### <a name="use-a-two-step-installation-to-troubleshoot-installation-issues"></a>Use uma instalação de duas etapas para solucionar problemas de instalação  
 Se houver erros durante a instalação, será possível executá-la como um processo de duas etapas na linha de comando:  
  
1.  Abra um prompt de comando **com permissões de administrador** e execute uma instalação somente de arquivos, conforme descrito na seção anterior.  
  
2.  Execute o executável de ações personalizadas:  
  
    1.  Navegue até a pasta que contém o arquivo **rsCustomAction.exe**. Esse arquivo é copiado no seu computador através da instalação somente de arquivos do suplemento. O**rsCustomAction.exe** está localizado no diretório **%Temp%** . Para navegar até o arquivo, digite o seguinte no prompt de comando:  
  
         **CD %temp%**.  
  
         O arquivo deve estar localizado em: **\Users\\<your name\>\AppData\Local\Temp**  
  
    2.  Digite o comando a seguir. Esta etapa de configuração demorará alguns minutos para ser concluída. O serviço W3SVC será reiniciado durante esse processo. Várias mensagens de status serão exibidas como os arquivos de cópias de programa, registrarão componentes e executarão o Assistente de Configuração de Produto do SharePoint.  
  
        ```  
        rsCustomAction.exe /i  
        ```  
  
    3.  A quantidade de tempo necessária para que as alterações entrem em vigor pode variar, dependendo de seu ambiente de servidor. Você também pode executar **iisreset** para forçar uma atualização mais rápida.  
  
### <a name="quiet-installation-for-scripting"></a>Instalação silenciosa para script  
 Você pode usar a opção **/q** ou **/quiet** para uma instalação "silenciosa" que não exibirá caixas de diálogo nem avisos. A instalação silenciosa é útil quando você deseja gerar scripts da instalação do suplemento.  
  
> [!NOTE]  
>  Se você usar a opção **/q** para uma instalação de linha de comando silenciosa, o contrato de licença de usuário final não será exibido. Independentemente do método de instalação, o uso deste software é controlado por um contrato de licença e você é responsável por respeitar o contrato de licença.  
  
 Para executar uma instalação silenciosa:  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /i rsSharePoint.msi /q  
    ```  
  
##  <a name="bkmk_remove_addin"></a> Como remover o Suplemento Reporting Services  
 Você pode desinstalar o Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para Produtos SharePoint do painel de controle do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ou da linha de comando.  
  
1.  Usar o painel de controle executará uma desinstalação completa dos arquivos no computador atual **E** removerá o objeto e os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do farm do SharePoint. Quando o objeto e os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] são removidos, você não pode mais revisar e atualizar relatórios.  
  
2.  O método de linha de comando para desinstalar o suplemento permite usar o parâmetro LocalOnly para somente remover os arquivos de suplemento do computador local e o objeto e os recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no farm não serão alterados.  
  
 A desinstalação do suplemento removerá recursos de integração de servidor usados para processar relatórios em um servidor de relatório. Ela também removerá as páginas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da Administração Central do SharePoint e outras páginas personalizadas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Você também pode querer remover os relatórios e outros itens do servidor de relatório que não estejam mais sendo usados nos sites do SharePoint afetados. Eles não serão executados após a remoção do Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para desinstalar o Suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , é necessário ter uma instalação do SharePoint ainda em execução. Se você desinstalar o SharePoint primeiro, reinstale-o para desinstalar o Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 As etapas para a desinstalação do suplemento são as mesmas para servidores autônomos e farms de servidores. A Instalação removerá arquivos de programas e quaisquer parâmetros de configuração que foram adicionados durante a instalação.  
  
 Desinstalar o suplemento não removerá o seguinte:  
  
-   Logons criados para a conta de serviço do Servidor de Relatório usados para acessar a configuração do SharePoint e os bancos de dados de conteúdo. Você deve excluir todos os logons da conta de serviço do Servidor de Relatório da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usada para hospedar os bancos de dados do SharePoint.  
  
-   Permissões ou grupos que você criou para usuários do relatório. Se você tiver criado níveis de permissão personalizados ou grupos do SharePoint para conceder acesso a recursos do servidor de relatório, deverá revogar quaisquer permissões que não sejam mais necessárias.  
  
-   Arquivos de dados que você carregou para uma biblioteca do SharePoint, incluindo arquivos de definição de relatório (.rdl), modelo de relatório (.smdl), fonte de dados compartilhada (.rsds) e itens de relatório publicados (.rsc). Eles não são excluídos, mas não serão mais executados. Você deve excluir manualmente os arquivos.  
  
-   A Instalação não excluirá o banco de dados do servidor de relatório e nem modificará a instância do servidor de relatório que foi usada para operações integradas.  
  
### <a name="to-uninstall-from-windows-control-panel"></a>Para desinstalar a partir do Painel de Controle do Windows  
 Para iniciar o assistente do Painel de Controle do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e remover o suplemento:  
  
1.  No Painel de Controle, em **Programas**, selecione **Desinstalar um Programa**  
  
2.  Selecione **Suplemento do Microsoft SQL Server RS para SharePoint**. Você também pode iniciar o assistente de desinstalação executando **rssharepoint.msi** no prompt de comando sem alterações.  
  
3.  Clique em **Remover**.  
  
### <a name="uninstall-from-the-command-line"></a>Desinstalar da linha de comando  
 Para desinstalar o suplemento a partir da linha de comando:  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    msiexec.exe /uninstall rsSharePoint.msi  
    ```  
  
3.  Você verá uma caixa de mensagem de confirmação. Clique em **Sim**.  
  
### <a name="uninstall-the-add-in-from-the-local-server-only"></a>Desinstale o suplemento apenas do servidor local  
 Os métodos anteriores de desinstalar o suplemento removerão os recursos e o objeto do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do farm. Se você tiver um farm multisservidor e desejar desinstalar o suplemento somente do computador local e deixar o farm do SharePoint em um estado funcional, conclua as etapas a seguir:  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    Msiexec.exe /uninstall rsSharePoint.msi LocalOnly=1  
    ```  
  
 Isso cancelará o registro de componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SharePoint e removerá os arquivos, mas apenas para o computador local.  
  
 Se quiser cancelar o registro de recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint, mas manter os arquivos no disco para uso posterior, conclua as etapas a seguir:  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    rsCustomAction.exe /p  
    ```  
  
 As etapas acima pressupõem que você concluiu uma instalação do .msi com SkipCA=1 e que o rscusstomaction.exe está disponível. Para obter mais informações, consulte a seção que descreve a instalação somente de arquivos.  
  
##  <a name="bkmk_repair"></a> Como reparar o rssharepoint.msi na linha de comando  
 Para reparar ou desinstalar o suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando a linha de comando, conclua as etapas a seguir:  
  
1.  Abra um prompt de comando **com permissões de administrador**.  
  
2.  Execute o seguinte comando:  
  
    ```  
    msiexec.exe /f rssharepoint.msi  
    ```  
  
##  <a name="bkmk_logfiles"></a> Arquivos de log de instalação  
 Quando a Instalação é executada, ela registra informações em um arquivo de log na pasta **%temp%** do usuário que instalou o Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por exemplo, **c:\Users\\<username\>\AppData\Local\Temp**. O nome do arquivo é **RS_SP_\<number>.log**, por exemplo, **RS_SP_0.log**. Cada erro no log é iniciado com a cadeia de caracteres "SSRSCustomActionError".  
  
> [!NOTE]  
>  AppData é uma pasta oculta no sistema operacional Windows. Talvez seja necessário modificar as configurações da sua pasta Windows Explorer para que você visualize arquivos e pastas ocultas.  
  
#### <a name="view-a-log-file-with-windows-notepad"></a>Exiba um arquivo de log com o Bloco de Notas do Windows  
  
1.  Os seguintes comandos alterarão o caminho de prompt de comando, listarão os arquivos de log de rs e abrirão um dos arquivos com Bloco de Notas di Windows:  
  
    ```  
    cd %temp%  
    ```  
  
    ```  
    Dir rs_sp*.log  
    ```  
  
    ```  
    notepad rs_sp_3.log  
    ```  
  
#### <a name="view-a-log-file-with-powershell"></a>Exiba um arquivo de log com o PowerShell  
  
1.  Digite o seguinte comando no Shell de Gerenciamento do SharePoint para retornar uma lista filtrada de linhas do arquivo, contendo "ssrscustomactionerror":  
  
    ```  
    Get-content -path C:\Users\<UserName\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
    ```  
  
2.  A saída terá esta aparência:  
  
     `2011-05-23 12:40:12: SSRSCustomActionError: SharePoint is installed, but not configured`.  
  
##  <a name="bkmk_upgrade"></a> Atualizar  
 Se você tiver uma instalação existente do Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , poderá atualizá-la para a versão atual. A configuração do suplemento detectará a versão existente e solicitará uma confirmação para a atualização. A mensagem será semelhante a:  
  
 **Uma versão Inferior deste produto foi detectada no sistema. Gostaria de atualizar sua instalação existente?**  
  
 Se você confirmar, a versão anterior do suplemento será removida, e a nova versão será instalada.  
  
 Observe que o Suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não reconhece a instância. Só pode haver uma única instância do suplemento em um computador. Não é possível executar versões diferentes e a versão atual lado a lado.  
  
##  <a name="bkmk_rscustomaction"></a> RsCustomAction.exe  
 A seguinte tabela resume as opções de rscustomaction.exe:  
  
|Opção|Descrição|  
|------------|-----------------|  
|i|Instale as ações personalizadas. Isso registrará os componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no SharePoint. Isso reiniciará o W3SVCservice.|  
|r|Reparar|  
|u|Desinstalar. Isso cancelará os componentes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do farm do SharePoint inteiro, mas manterá os arquivos em disco. Isso reiniciará o W3SVCservice.|  
|p|Desinstalação local. Isso cancelará o registro dos componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] apenas do computador local. Os arquivos permanecerão em disco. Isso reiniciará o W3SVCservice.|  
|t|Somente SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005. A opção verifica se o servidor de relatórios tem uma conexão ativa com o banco de dados do servidor de relatórios.|  
  
## <a name="configuring-reporting-services"></a>Configurando o Reporting Services  
 Depois de instalar o suplemento em todos os computadores necessários, configure o servidor de relatório na Administração Central do SharePoint. As etapas necessárias dependem da ordem em que as diferentes tecnologias foram instaladas. Para obter mais informações, veja [Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md) e [Servidor de relatório do Reporting Services (Modo do SharePoint)](../../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)  
  
## <a name="see-also"></a>Consulte Também

[Instalar o primeiro servidor de relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md)   
[Servidor de relatório do Reporting Services &#40;Modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
