---
title: "Power Pivot a atualização de dados com o SharePoint 2013 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34f03407-2ec4-4554-b16b-bc9a6c161815
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 59648b6a3f3dc221fa1e80be1e737606b5fede04
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="power-pivot-data-refresh-with-sharepoint-2013"></a>Atualização de dados do Power Pivot com o SharePoint 2013
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O design para atualização de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modelos de dados no SharePoint 2013 utiliza serviços do Excel como componente primário para carregar e atualizar modelos de dados em uma instância de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no modo do SharePoint. O servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executado externamente ao farm do SharePoint. A arquitetura dos Serviços do Excel do SharePoint 2013 oferece suporte para a **atualização de dados interativa** e para a **atualização de dados agendada**.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013  
  
 **Neste tópico:**  
  
-   [Interactive Data Refresh](#bkmk_interactive_refresh)  
  
-   [Autenticação do Windows com conexões de dados da pasta de trabalho e atualização de dados interativa](#bkmk_windows_auth_interactive_data_refresh)  
  
-   [Scheduled Data Refresh](#bkmk_scheduled_refresh)  
  
-   [Arquitetura de atualização no SharePoint 2013](#bkmk_refresh_architecture)  
  
-   [Considerações adicionais sobre autenticação](#datarefresh_additional_authentication)  
  
-   [Mais informações](#bkmk_moreinformation)  
  
## <a name="background"></a>Plano de fundo  
 Os Serviços do Excel do SharePoint Server 2013 gerenciam a atualização de dados de pastas de trabalho do Excel 2013 e disparam o processamento de modelo de dados em um servidor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está executando no modo do SharePoint. No caso de pastas de trabalho do Excel 2010, os Serviços do Excel também gerenciam as ações de carregar e salvar pastas de trabalho e modelos de dados. No entanto, os Serviços do Excel se baseiam no Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para enviar os comandos de processamento ao modelo de dados. A tabela a seguir resume os componentes que enviam comandos de processamento para atualização de dados, dependendo da versão da pasta de trabalho. Pressupõe-se que o ambiente seja um farm do SharePoint 2013 configurado para usar um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server em execução no modo do SharePoint.  
  
||||  
|-|-|-|  
||Pastas de Trabalho do Excel 2013|Pastas de Trabalho do Excel 2010|  
|Disparam a atualização de dados|**Interativo:** Usuário Autenticado<br /><br /> **Agendado:** [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Serviço do sistema|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Serviço do sistema|  
|Carregam a pasta de trabalho com base em bancos de dados de conteúdo|Serviços do Excel do SharePoint 2013|Serviços do Excel do SharePoint 2013|  
|Carregam o modelo de dados na instância do Analysis Services|Serviços do Excel do SharePoint 2013|Serviços do Excel do SharePoint 2013|  
|Enviam comandos de processamento à instância do Analysis Services|Serviços do Excel do SharePoint 2013|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Serviço do sistema|  
|Atualizam dados da pasta de trabalho|Serviços do Excel do SharePoint 2013|Serviços do Excel do SharePoint 2013|  
|Salvam a pasta de trabalho e o modelo de dados no banco de dados de conteúdo|**Interativo:** N/D<br /><br /> **Agendado:** Serviços do Excel do SharePoint 2013|Serviços do Excel do SharePoint 2013|  
  
 A tabela a seguir resume os recursos de atualização com suporte em um farm do SharePoint 2013 configurado para usar um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Analysis Server em execução no modo do SharePoint:  
  
|Pasta de trabalho criada em|atualização de dados agendada|Atualização interativa|  
|-------------------------|----------------------------|-------------------------|  
|2008 R2 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel|Sem suporte. Atualizar a pasta de trabalho **(\*)**|Sem suporte. Atualizar a pasta de trabalho **(\*)**|  
|2012 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel|Tem suporte|Sem suporte. Atualizar a pasta de trabalho **(\*)**|  
|Excel 2013|Tem suporte|Tem suporte|  
  
 **(\*)** Para obter mais informações, consulte [Atualizar pastas de trabalho e atualização de dados agendada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
##  <a name="bkmk_interactive_refresh"></a> Interactive Data Refresh  
 A atualização de dados, interativa ou manual, em Serviços do Excel do SharePoint Server 2013 pode atualizar modelos de dados com dados da fonte de dados original. A atualização de dados interativa estará disponível depois que você configurar um aplicativo de Serviços do Excel registrando um servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , em execução no modo do SharePoint. Para obter mais informações, consulte [Gerenciar configurações do modelo de dados dos Serviços do Excel (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780.aspx) (http://technet.microsoft.com/library/jj219780.aspx).  
  
> [!NOTE]  
>  A atualização de dados interativa está disponível somente para as pastas de trabalho criadas no Excel 2013. Se você tentar atualizar uma pasta de trabalho do Excel 2010, os Serviços do Excel exibirão uma mensagem de erro semelhante à esta: "Falha na operação do[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] : a pasta de trabalho foi criada em uma versão antiga do Excel e o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não pode ser atualizado até que o arquivo seja atualizado". Para obter mais informações sobre como atualizar pastas de trabalho, consulte [Atualizar pastas de trabalho e atualização de dados agendada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 **Ponto de interesse principal da atualização interativa:**  
  
-   A atualização de dados interativa atualiza somente os dados na sessão de usuário atual. Os dados não são salvos automaticamente no item de pasta de trabalho no banco de dados de conteúdo do SharePoint.  
  
-   **Credenciais:** a atualização de dados interativa pode usar a identidade do usuário atualmente conectado como credenciais ou credenciais armazenadas para se conectar à fonte de dados. As credenciais usadas dependem das Configurações de Autenticação dos Serviços do Excel definidas para a conexão da pasta de trabalho com a fonte de dados externa.  
  
-   **Pastas de Trabalho com Suporte:**  pastas de trabalho criadas no Excel 2013.  
  
 **Para atualizar dados:**  
  
-   Consulte a ilustração após as etapas.  
  
1.  Em uma biblioteca de documentos do SharePoint, abra uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no navegador.  
  
2.  Na janela do navegador, clique no menu **Dados** e clique em **Atualizar Conexão Selecionada** ou **Atualizar Todas as Conexões**.  
  
3.  Os Serviços do Excel carregam o banco de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , processam esse banco de dados e o consultam para atualizar o cache da pasta de trabalho do Excel.  
  
4.  **Observação:** a pasta de trabalho atualizada não é salva automaticamente na biblioteca de documentos.  
  
 ![atualização de dados interativa](../../analysis-services/power-pivot-sharepoint/media/as-interactive-datarefresh-sharepoint2013.gif "atualização de dados interativa")  
  
###  <a name="bkmk_windows_auth_interactive_data_refresh"></a> Autenticação do Windows com conexões de dados da pasta de trabalho e atualização de dados interativa  
 Os Serviços do Excel enviam ao servidor do Analysis Services um comando de processo que instrui o servidor a representar uma conta de usuário. Para obter direitos de sistema suficientes para executar o processo de representação-delegação do usuário, a conta de serviço do Analysis Services exige o privilégio **Atuar como parte do sistema operacional** no servidor local. O servidor do Analysis Services também precisa ser capaz de delegar as credenciais do usuário a fontes de dados. O resultado da consulta é enviado aos Serviços do Excel.  
  
 Experiência típica do usuário: quando um cliente seleciona “Atualizar Todas as Conexões” em uma pasta de trabalho do Excel 2013 que contém um modelo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , ele recebe uma mensagem de erro semelhante à seguinte:  
  
-   **Falha na Atualização de Dados Externos:** erro ao trabalhar com o Modelo de Dados na pasta de trabalho. Tente novamente. Não foi possível atualizar uma ou mais conexões de dados nesta pasta de trabalho.  
  
 Dependendo do provedor de dados utilizado, você receberá mensagens semelhantes às seguintes no log ULS.  
  
 **Com o SQL Native Client:**  
  
-   Falha ao criar uma conexão externa ou ao executar uma consulta. Mensagem do provedor: o objeto fora de linha 'DataSource', que referencia a(s) ID(s) '20102481-39c8-4d21-bf63-68f583ad22bb', foi especificado, mas não foi usado.  Erro OLE DB ou ODBC: um erro relativo à rede ou específico da instância ocorreu ao estabelecer conexão com o SQL Server. O servidor não foi encontrado ou não está acessível. Verifique se o nome da instância está correto e se o SQL Server está configurado para permitir conexões remotas. Para obter mais informações, consulte os Manuais Online do SQL Server.; 08001; Provedor SSL: o pacote de segurança necessário não existe; 08001; O cliente não conseguiu estabelecer a conexão; 08001; A criptografia não tem suporte no cliente.; 08001.  , ConnectionName: ThisWorkbookDataModel, Pasta de trabalho: book1.xlsx.  
  
 **Com o Microsoft OLE DB Provider para SQL Server:**  
  
-   Falha ao criar uma conexão externa ou ao executar uma consulta. Mensagem do provedor: O objeto fora de linha 'DataSource', fazendo referência à(s) ID(s) '6e711bfa-b62f-4879-a177-c5dd61d9c242', foi especificado, mas não foi usado. Erro de OLE DB ou ODBC. , ConnectionName: ThisWorkbookDataModel, Pasta de trabalho: OLEDB Provider.xlsx.  
  
 **Com o Provedor de Dados .NET Framework para SQL Server:**  
  
-   Falha ao criar uma conexão externa ou ao executar uma consulta. Mensagem do provedor: O objeto fora de linha 'DataSource', que referencia a(s) ID(s) 'f5fb916c-3eac-4d07-a542-531524c0d44a', foi especificado, mas não foi usado.  Erros no mecanismo relacional de alto nível. A exceção a seguir ocorreu enquanto a interface IDbConnection estava sendo usada: Não foi possível carregar o arquivo ou o assembly 'System.Transactions, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ou uma de suas dependências. O nível de representação necessário não foi fornecido ou o nível de representação fornecido é inválido. (Exceção de HRESULT: 0x80070542).  , ConnectionName: ThisWorkbookDataModel, Pasta de trabalho: NETProvider.xlsx.  
  
 **Resumo das etapas de configuração** Para configurar o privilégio de **Atuar como parte do sistema operacional** no servidor local:  
  
1.  No Servidor do Analysis Services Server em execução no modo do SharePoint, adicione a conta de serviço do Analysis Services ao privilégio "Atuar como parte do sistema operacional":  
  
    1.  Execute “`secpol.msc`”  
  
    2.  Clique em **Política de Segurança Local**, em **Políticas locais**e em **Atribuição de direitos de usuário**.  
  
    3.  Adicione a conta de serviço.  
  
2.  Reinicie os Serviços do Excel e reinicialize o servidor do Analysis Services.  
  
3.  A delegação da conta de serviço dos Serviços do Excel ou de declarações para serviço de token do Windows (C2WTS) para a instância do Analysis Services não é necessária. Assim, nenhuma configuração para KCD dos Serviços do Excel ou C2WTS para o serviço AS do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é necessária. Se a fonte de dados de back-end estiver no mesmo servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , a delegação restrita de Kerberos não será necessária. No entanto, a conta de serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requer a permissão para Atuar como parte do sistema operacional.  
  
 ![as_interactive_data_refresh2012SP1_windowsauth](../../analysis-services/power-pivot-sharepoint/media/as-interactive-data-refresh2012sp1-windowsauth.gif "as_interactive_data_refresh2012SP1_windowsauth")  
  
 Para obter mais informações, consulte [Atuar como parte do sistema operacional](http://technet.microsoft.com/library/cc784323\(WS.10\).aspx) (http://technet.microsoft.com/library/cc784323(WS.10).aspx).  
  
##  <a name="bkmk_scheduled_refresh"></a> Scheduled Data Refresh  
 **Pontos de interesse principais da atualização de dados agendada:**  
  
-   Exige a implantação do suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Para obter mais informações, consulte [Instalar ou desinstalar o suplemento do Power Pivot para SharePoint &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md).  
  
-   Um usuário configura um agendamento de atualização para uma pasta de trabalho. No momento agendado, o Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] envia uma solicitação aos Serviços do Excel para:  
  
    -   Carregar e processar o banco de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
    -   Atualizar a pasta de trabalho.  
  
    -   Salvar a pasta de trabalho no banco de dados de conteúdo novamente.  
  
-   **Credenciais:** usa credenciais armazenadas. Não usa a identidade do usuário atual.  
  
-   **Pastas de trabalho com suporte:** pastas de trabalho criadas usando o suplemento [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel 2010 ou usando o Excel 2013. Não há suporte para pastas de trabalho criadas no Excel 2010 com o suplemento [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Atualize a pasta de trabalho para, pelo menos, o formato do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações, consulte [Atualizar pastas de trabalho e atualização de dados agendada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).  
  
 Para exibir a página **Gerenciar Atualização de Dados** :  
  
-   Consulte a ilustração após as etapas.  
  
1.  Em uma biblioteca de documentos do SharePoint, clique no **menu Abrir** (**...**) de uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
2.  Clique no segundo **menu Abrir** e clique em **Gerenciar Atualização de Dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Na página **Gerenciar Atualização de Dados** , clique em **Habilitar** e configure o agendamento de atualização.  
  
4.  No momento especificado, o Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] envia uma solicitação aos Serviços do Excel para:  
  
    -   Carregar e processar o modelo de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
    -   Atualizar a pasta de trabalho.  
  
    -   Salvar a pasta de trabalho no banco de dados de conteúdo novamente.  
  
 ![gerenciar o menu de contexto de atualização de dados](../../analysis-services/power-pivot-sharepoint/media/as-manage-datarefresh-sharepoint2013.gif "gerenciar o menu de contexto de atualização de dados")  
  
> [!TIP]  
>  Para obter informações sobre como atualizar pastas de trabalho do SharePoint online, consulte [Refreshing Excel workbooks with embedded Power Pivot models from SharePoint Online (white paper)](http://technet.microsoft.com/library/jj992650.aspx) (Atualizando pastas de trabalho do Excel com modelos PowerPivot inseridos do SharePoint Online)(http://technet.microsoft.com/library/jj992650.aspx).  
  
##  <a name="bkmk_refresh_architecture"></a> Arquitetura de atualização no SharePoint 2013  
 A ilustração a seguir resume a arquitetura de atualização de dados no SharePoint 2013 e no SQL Server 2012 SP1.  
  
 ![arquitetura de atualização de dados do SQL Server 2012 SP1](../../analysis-services/power-pivot-sharepoint/media/as-scheduled-data-refresh2012sp1-architecture.gif "arquitetura de atualização de dados do SQL Server 2012 SP1")  
  
||Description||  
|-|-----------------|-|  
|**(1)**|Mecanismo do Analysis Services|Um servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está executando no modo do SharePoint. O servidor é executado fora do farm do SharePoint.|  
|**(2)**|Interface do usuário|A interface do usuário é composta por duas páginas. Uma para definir o agendamento e a segunda para exibir o histórico de atualização. As páginas não acessam diretamente os bancos de dados de aplicativo do Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , mas usam o serviço do sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para acessar os bancos de dados.|  
|**(3)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Serviço do sistema|O serviço é instalado quando você implanta o suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> O serviço é usado para o seguinte:|  
|||Esse serviço hospeda o mecanismo de agendamento de atualização, que chama as APIs dos Serviços do Excel para a atualização de dados de pastas de trabalho do Excel 2013. Para pastas de trabalho do Excel 2010, o serviço executa diretamente o processamento do modelo de dados, mas continua respondendo nos Serviços do Excel para carregar o modelo de dados e atualizar a pasta de trabalho.|  
|||Esse serviço fornece métodos de comunicação com o serviço do sistema para componentes, como páginas da interface do usuário.|  
|||Gerencia as solicitações de acesso externo a pastas de trabalho como uma fonte de dados, recebidas pelo Serviço Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|||Gerenciamento de solicitação de atualização de dados agendada para trabalhos de timer e páginas de configuração. O serviço gerencia solicitações de leitura de dados dentro e fora do banco de dados do aplicativo de serviço e dispara a atualização de dados com os Serviços do Excel.|  
|||Processamento de uso e trabalho de timer relacionado.|  
|**(4)**|Serviços de Cálculo do Excel|Responsáveis por carregar os modelos de dados.|  
|**(5)**|Serviço de Repositório Seguro|Se as configurações de autenticação na pasta de trabalho estiverem definidas como **Usar a conta do usuário autenticado** ou **Nenhuma**, as credenciais armazenadas na ID do aplicativo de destino de Repositório Seguro serão usadas para atualização de dados. Para obter mais informações, consulte a seção [Considerações adicionais sobre autenticação](#datarefresh_additional_authentication) neste tópico.|  
|**(6)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Trabalho do temporizador da atualização de dados|Instrui o serviço do sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a se conectar com os Serviços do Excel para atualizar modelos de dados.|  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requer provedores de dados e bibliotecas de cliente apropriados para que o servidor do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint possa acessar fontes de dados.  
  
> [!NOTE]  
>  Como o serviço do sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não carrega nem salva mais modelos do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , a maioria das configurações para caching de modelos em um servidor de aplicativos não se aplica a um farm do SharePoint 2013.  
  
## <a name="data-refresh-log-data"></a>Dados de log de atualização de dados  
 **Dados de Uso:** você pode exibir os dados de uso de atualização de dados no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para consultar os dados de uso:  
  
1.  Na Administração Central do SharePoint, clique em **Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**, no grupo **Configurações gerais do aplicativo**.  
  
2.  Na parte inferior do painel, consulte **Atualização de Dados – Atividade Recente** e **Atualização de Dados – Falhas Recentes**.  
  
3.  Para obter mais informações sobre dados de uso e como habilitá-los, consulte [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
 **Dados do log de diagnóstico:** é possível exibir os dados do log de diagnóstico do SharePoint relacionados à atualização de dados. Primeiro, verifique a configuração de log de diagnóstico do **Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** na página **Monitoramento** da Administração Central do SharePoint. Talvez seja necessário aumentar o nível de log para “evento menos crítico” no log. Por exemplo, defina o valor temporariamente como **Detalhado** e execute as operações de atualização de dados novamente.  
  
 As entradas de log contêm:  
  
-   A **Área** do **Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
-   A categoria de **Atualização de Dados**.  
  
 Examine **configurar log de diagnóstico**. Para obter informações, veja [Configurar e exibir arquivos de log do SharePoint e log de diagnósticos &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).
  
##  <a name="datarefresh_additional_authentication"></a> Considerações adicionais sobre autenticação  
 As configurações na caixa de diálogo **Configurações de Autenticação dos Serviços do Excel** no Excel 2013 determinam a identidade do Windows que os Serviços do Excel e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usam para atualização de dados.  
  
-   **Usar a conta do usuário autenticado**: os Serviços do Excel executam a atualização de dados com a identidade do usuário conectado no momento.  
  
-   **Usar uma conta armazenada**: pressupõe uma ID de aplicativo do Serviço de Repositório Seguro do SharePoint, que os Serviços do Excel usam para recuperar o nome do usuário e a senha para autenticação de atualização de dados.  
  
-   **Nenhum**: a **Conta de Serviço sem Supervisão** dos Serviços do Excel é usada. A conta de serviço está associada a um Proxy de Repositório Seguro. Defina as configurações na página **Configurações de Aplicativo dos Serviços do Excel** , na seção **Dados Externos** .  
  
 Para abrir a caixa de diálogo de configurações de autenticação:  
  
1.  Clique na guia **Dados** no Excel 2013.  
  
2.  Clique em **Conexões** na faixa de opções.  
  
3.  Na caixa de diálogo **Conexões da pasta de trabalho**, selecione a conexão e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades de conexão** , clique em **Definição**e no botão **Configurações de Autenticação…** .  
  
 ![excel services authentication settings](../../analysis-services/power-pivot-sharepoint/media/as-authentication-settings-4-ecs-in-excel2013.gif "excel services authentication settings")  
  
 Para obter mais informações sobre autenticação de atualização de dados e uso de credenciais, consulte a postagem de blog [Atualizando dados do PowerPivot no SharePoint 2013](http://blogs.msdn.com/b/analysisservices/archive/2012/12/21/refreshing-powerpivot-data-in-sharepoint-2013.aspx).  
  
##  <a name="bkmk_moreinformation"></a> Mais informações  
 [Solucionando problemas de atualização de dados do PowerPivot](http://social.technet.microsoft.com/wiki/contents/articles/3870.troubleshooting-powerpivot-data-refresh.aspx).  
  
 [Serviços do Excel no SharePoint 2013](http://msdn.microsoft.com/library/sharepoint/jj164076\(v=office.15\)) (http://msdn.microsoft.com/library/sharepoint/jj164076 (v=office.15).  
  
## <a name="see-also"></a>Consulte Também  
 [Instale o Analysis Services no modo do Power Pivot.](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
