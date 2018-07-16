---
title: Atualizar Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
caps.latest.revision: 65
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1ba06e961245cf1fe9ae5802abc26b575fe7683c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244506"
---
# <a name="upgrade-reports"></a>Upgrade Reports
  Os arquivos de definição de relatório (.rdl) são automaticamente atualizados da seguinte forma:  
  
-   Quando você abre um relatório no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a definição do relatório é atualizada para o esquema RDL com suporte no momento. Quando você especifica um [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] servidor de relatório nas propriedades do projeto, definição de relatório é salvo em um esquema que é compatível com o servidor de destino.  
  
-   Quando você atualiza uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para uma instalação do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , os relatórios e instantâneos existentes que foram publicados em um servidor de relatório são compilados e atualizados automaticamente para o novo esquema na primeira vez que são processados. Se não for possível atualizar um relatório automaticamente, o relatório será processado usando o modo da compatibilidade com versões anteriores. A definição de relatório permanece no esquema original.  
  
 Os relatórios não são atualizados quando você carrega um arquivo de definição de relatório diretamente no servidor de relatório ou no site do SharePoint. A atualização de uma definição de relatório no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] é a única maneira de atualizar o arquivo .rdl.  
  
 Após a atualização de um relatório localmente ou no servidor de relatório, talvez você encontre erros, avisos e mensagens adicionais. Esse é o resultado das alterações no modelo de objeto de relatório interno e nos componentes de processamento, que fazem com que mensagens sejam exibidas quando forem detectados problemas subjacentes no relatório. Para obter mais informações, consulte [Compatibilidade com versões anteriores do Reporting Services](../reporting-services-backward-compatibility.md).  
  
 Para obter mais informações sobre os novos recursos para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], consulte [novidades &#40;Reporting Services&#41;](../what-s-new-reporting-services.md).  
  
 Neste tópico:  
  
-   [Versões com suporte da atualização](#bkmk_versionsupported)  
  
-   [Arquivos de definição de relatório (.rdl) e Designer de Relatórios](#bkmk_rdlfiles)  
  
-   [Relatórios publicados e instantâneos de relatório](#bkmk_publishedreports_and_snapshots)  
  
-   [Modo de compatibilidade com versões anteriores](#bkmk_backcompat)  
  
-   [Atualizando um relatório com sub-relatórios](#bkmk_subreports)  
  
-   [Atualizando um relatório com itens de relatório personalizados](#bkmk_CRIs)  
  
-   [Caixa de diálogo Converter CRI](#bkmk_convertCRIdialog)  
  
##  <a name="bkmk_versionsupported"></a> Versões com suporte da atualização  
 Relatórios que foram criados em qualquer versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser atualizados. Isso inclui as seguintes versões:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 com Service Pack 1  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 com o Service Pack 2  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> Arquivos de definição de relatório (.rdl) e Designer de Relatórios  
 Um arquivo de definição de relatório inclui uma referência ao namespace do RDL que especifica a versão do esquema de definição de relatório usado para validar o arquivo .rdl.  
  
 Ao abrir um arquivo .rdl no Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se o relatório tiver sido criado para um namespace anterior, o Designer de Relatórios criará automaticamente um arquivo de backup e atualizará o relatório para o namespace atual. Esse é o único modo que você pode atualizar um arquivo de definição de relatório.  
  
 As propriedades da implantação que você define podem afetar em qual esquema o arquivo de definição de relatório é salvo. Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
 Você pode carregar um arquivo .rdl criado em uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e ele será atualizado automaticamente na primeira vez que for usado. O servidor de relatório armazena o arquivo de definição de relatório no formato original. O relatório será atualizado automaticamente na primeira vez que for exibido, mas o arquivo de definição de relatório armazenado permanecerá inalterado.  
  
> [!NOTE]  
>  Você não pode publicar nem carregar um relatório que tenha o namespace de definição de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em um servidor de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
 Para identificar o esquema RDL atual de um relatório, de um servidor de relatório ou do Designer de Relatórios, consulte [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> Relatórios publicados e instantâneos de relatório  
 Na primeira vez que for usado, o servidor de relatório tentará atualizar os relatórios publicados e os instantâneos de relatório existentes para o novo esquema de definição de relatório, sem exigir uma ação específica de sua parte. Quando um usuário exibe um relatório ou um instantâneo de relatório, ou quando o servidor de relatório processa uma assinatura, ocorre uma tentativa de atualização. A definição de relatório não é substituída, mas continua sendo armazenada no servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em seu esquema original. Se um relatório não puder ser atualizado, ele será executado no modo da compatibilidade com versões anteriores.  
  
##  <a name="bkmk_backcompat"></a> Modo de compatibilidade com versões anteriores  
 Um relatório atualizado com êxito é processado pelo processador de relatório [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Um relatório que não pode ser atualizado é processado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] processador no modo de compatibilidade com versões anteriores de relatório. Um relatório não pode ser processado pelos dois processadores de relatório. Na primeira vez que for usado, um relatório será atualizado com êxito ou marcado para compatibilidade com versões anteriores.  
  
 Só o processador de relatório [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] dá suporte a novos recursos. Se não for possível atualizar um relatório, você ainda poderá exibir o relatório renderizado, mas os recursos novos não estarão disponíveis. Para se beneficiar dos recursos novos, um relatório deverá ser atualizado com êxito.  
  
##  <a name="bkmk_subreports"></a> Atualizando um relatório com sub-relatórios  
 Quando um relatório contiver sub-relatórios, um de quatro possíveis estados poderá ocorrer durante a atualização:  
  
-   O relatório principal e todos os sub-relatórios podem ser atualizados com êxito. Eles são processados pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
-   O relatório principal e todos os sub-relatórios não podem ser atualizados. Eles são processados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] processador de relatório.  
  
-   O relatório principal pode ser atualizado, entretanto um ou mais sub-relatórios não podem ser atualizados. O relatório principal é processado pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mas o relatório renderizado mostra a mensagem "Erro: não foi possível processar o sub-relatório" no local onde o sub-relatório que não foi atualizado seria exibido.  
  
-   Não é possível atualizar o relatório principal, entretanto é possível atualizar um ou mais sub-relatórios. O relatório principal é processado pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mas o relatório renderizado mostra a mensagem "Erro: não foi possível processar o sub-relatório" no local onde o sub-relatório seria exibido.  
  
 Se você visualizar o erro "Erro: não foi possível processar o sub-relatório", deverá alterar a definição do relatório principal ou do sub-relatório de forma que os relatórios possam ser processados pela mesma versão do processador de relatórios.  
  
 Relatórios detalhados não têm esta limitação porque eles são processados como relatórios independentes.  
  
##  <a name="bkmk_CRIs"></a> Atualizando um relatório com itens de relatório personalizados  
 Os relatórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem conter CRIs (itens de relatórios personalizados) fornecidos pelos fornecedores de software de terceiros e instalados pelo administrador do sistema no computador de criação de relatório e no servidor de relatório. Os relatórios que contêm CRIs podem ser atualizados dos seguintes modos:  
  
-   Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de relatório é atualizado para um [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de relatório. Os relatórios publicados no servidor de relatório serão atualizados automaticamente na primeira vez que forem usados.  
  
-   Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatório é carregado para um [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de relatório. O relatório será atualizado automaticamente na primeira vez que for usado.  
  
-   Um relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é aberto no Designer de Relatórios no  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Uma cópia de backup do relatório original é criada. Ocorrerá um dos dois casos seguintes:  
  
    1.  Todos o CRIs no relatório não têm recurso sem-suporte. Os CRIs são convertidos em itens de relatório no novo esquema de definição de relatório, portanto, o relatório inteiro é atualizado. Se você salvar o arquivo, ele será salvo no namespace da RDL atual.  
  
    2.  Um ou mais CRIs no relatório têm recursos sem-suporte. Uma caixa de diálogo avisa o usuário se deve converter os CRIs ou deixá-los inalterados.  
  
     Para obter mais informações, consulte [Abrindo um relatório no Designer de Relatórios](#OpeningaReport) posteriormente neste tópico.  
  
 Para obter informações sobre como identificar o namespace de RDL atual de um servidor de relatório, do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou de um relatório, consulte [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md).  
  
### <a name="upgrading-reports-on-a-report-server"></a>Atualizando relatórios em um servidor de relatório  
 Na primeira vez em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatório é executado em um servidor de relatório que foi atualizado para um [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de relatório, o relatório é atualizado automaticamente para o namespace de definição de relatório atual suportado pelo servidor de relatório. O relatório poderia ter existido no servidor de relatório antes da atualização ou o relatório poderia ter sido carregado por meio do Gerenciador de relatórios ou publicado para o servidor de relatório no Designer de relatórios no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 A tabela seguinte lista a ação de atualização que é executada pelo servidor de relatório para tipos específicos de CRIs em um relatório.  
  
|Tipo de CRI|Ação de atualização do servidor de relatório|  
|--------------|----------------------------------|  
|CRIs de terceiros|Atualização não executada.<br /><br /> Processado pelo processador de relatório [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|CRI de Gráfico Dundas 2005 que não tem recursos sem-suporte|Atualizado para o esquema RDL mais recente. Todos os CRIs de Gráfico Dundas 2005 são convertidos em regiões de dados do gráfico compatíveis com o [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].<br /><br /> Processado pelo processador do relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|CRI do medidor 2005 Dundas que não tem recursos sem suporte|Atualizado para o esquema RDL mais recente. Todos os CRIs de medidor Dundas 2005 são convertidos em regiões de dados que são compatíveis com medidor [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]<br /><br /> Processado pelo processador do relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|CRI de Gráfico Dundas 2005 com recursos sem-suporte|Atualização não executada.<br /><br /> Processado pelo processador de relatório [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|CRI do medidor 2005 Dundas com recursos sem suporte|Atualização não executada.<br /><br /> Processado pelo processador de relatório [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###  <a name="OpeningaReport"></a> Abrindo um Relatório com CRIs no Designer de Relatórios  
 Quando você abre um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] relatório com CRIs no Designer de relatórios no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o relatório será atualizado para o novo esquema de definição de relatório. Dependendo dos CRIs contidos no relatório, uma das seguintes ações ocorrerá:  
  
-   CRIs de terceiros detectados. Se a versão do CRI que está instalada no computador de criação de relatórios não for compatível com o novo esquema rdl, a superfície do design mostrará uma caixa de texto com um X vermelho. Você deverá contatar o administrador do sistema para instalar novas versões do CRI de fornecedores de terceiros que sejam compatíveis com o novo esquema rdl.  
  
-   Os CRIs do gráfico ou medidor 2005 Dundas detectados e todas as instâncias contêm funcionalidade com suporte. Todos os CRIs de gráfico ou medidor 2005 Dundas são convertidos em itens de relatório de gráfico e medidor do Reporting Services que você visualiza na Caixa de Ferramentas. Eles são conhecidos como itens de relatório de gráfico e medidor nativos.  
  
-   Os CRIs de Gráfico ou Medidor 2005 Dundas são detectados e qualquer instância tem funcionalidade sem suporte. A funcionalidade sem-suporte é descrita depois desta seção. Você pode escolher se deve converter todos os CRIs em itens de relatório nativos.  
  
    -   Se você os converter, o relatório será atualizado para o novo esquema rdl, e os CRIs de gráfico e medidor 2005 Dundas serão convertidos em itens de relatório de gráfico e medidor nativos correspondentes, mas a funcionalidade sem suporte será removida. No relatório renderizado, você poderia consultar diferenças do modo de exibição do CRI.  
  
    -   Se você optar por não convertê-los, o relatório será atualizado para o novo esquema rdl, mas os CRIs serão tratados como CRIs de terceiros. Você deve trabalhar com o administrador do sistema e os fornecedores de terceiros para instalar novos CRIs que são compatíveis com o novo esquema de relatório. Se os novos CRIs não estiverem disponíveis, o relatório exibirá uma caixa de texto com um X vermelho no Designer de Relatórios.  
  
 Salvar um relatório depois de ele ser atualizado no ambiente de criação de relatórios é a única maneira de atualizar um relatório existente para o novo esquema de definição de relatório.  
  
### <a name="unsupported-dundas-2005-chart-custom-report-item-functionality"></a>Funcionalidade do item de relatório personalizado do gráfico 2005 Dundas sem-suporte  
 A funcionalidade sem-suporte para CRI do Gráfico 2005 Dundas inclui os seguintes recursos:  
  
-   Anotações.  
  
-   Itens personalizados de legenda.  
  
-   Atributos personalizados com os seguintes nomes:  
  
    -   CUSTOM_CODE_CS  
  
    -   CUSTOM_CODE_VB  
  
    -   CUSTOM_CODE_COMPILED_ASSEMBLY  
  
         Por exemplo, se o arquivo .rdl contiver a seção seguinte, você deverá removê-lo antes da atualização:  
  
        ```  
        <CustomProperty>  
         <Name>CUSTOM_CODE_CS</Name>  
         <Value>dXNpWERwegfdfgiobxxl3bmc… </Value>  
        </CustomProperty>  
        ```  
  
### <a name="unsupported-dundas-2005-gauge-custom-report-item-functionality"></a>Funcionalidade do item de relatório personalizado do medidor 2005 Dundas sem suporte  
 A funcionalidade sem suporte para CRI do medidor 2005 Dundas inclui os seguintes recursos:  
  
-   Indicadores numéricos.  
  
-   Indicadores estatais.  
  
-   Imagens personalizadas.  
  
###  <a name="bkmk_convertCRIdialog"></a> Caixa de diálogo Converter CRI  
 Este relatório contém CRIs (itens de relatório personalizados) com recursos sem suporte. CRIs são extensões para a linguagem RDL (Report Definition Language) que oferecem suporte a objetos personalizados que exibem dados em um relatório. Os CRIs incluem componentes em tempo de design e em tempo de execução oferecidos por fornecedores de software de terceiros.  
  
> [!NOTE]  
>  Optar por oferecer suporte a itens de relatório personalizados em um servidor de relatório é uma decisão tomada pelo administrador do sistema. Para exibir CRIs em um relatório, os componentes do CRI devem ser instalados no cliente de criação do relatório para visualizar um relatório e no servidor de relatório para exibir um relatório publicado ou carregado. Para obter mais informações, consulte [itens de relatório personalizados](../custom-report-items/custom-report-items.md) e a documentação do fornecedor do software de terceiros.  
  
 Alguns CRIs podem ser convertidos em itens de relatório no novo formato de definição do relatório. Para obter a lista de CRIs que podem ser convertidos, consulte [Upgrading Reports](upgrade-reports.md). Use a seguinte lista para decidir se você deve converter os CRIs nesse relatório:  
  
-   **Sim** Escolha **Sim** para converter todos os CRIs do relatório, quando possível. Recursos para os quais não há suporte nos CRIs não podem ser atualizados, sendo removidos do arquivo de definição do relatório. Para obter a lista de recursos sem suporte, consulte [Upgrading Reports](upgrade-reports.md). Ao exibir o relatório, você pode ver as diferenças na forma como o CRI é exibido no relatório.  
  
-   **Não** Escolha **Não** quando não quiser converter os CRIs do relatório. Esses CRIs não podem ser exibidos pelo processador de relatório na versão atual. Caso o administrador do sistema pretenda instalar uma nova versão da CRI do fornecedor de software de terceiros compatível com o novo formato de definição do relatório, escolha **Não**. Até que as novas versões estejam disponíveis, os CRIs são exibidos no relatório como uma caixa de texto vazia com um X vermelho.  
  
 Em ambos os casos, o relatório é atualizado para o novo formato de definição de relatório e uma cópia de backup do relatório original é salva como *\<Report Name>* `-` Backup.rdl. Caso salve o relatório na ferramenta de criação do relatório, você está salvando o relatório atualizado no novo formato de definição do relatório. Caso você publique o relatório, ele é salvo primeiro no computador e, em seguida, publicado no servidor de relatório. Você está publicando a versão atualizada do relatório no servidor de relatório.  
  
 Caso você não salve o relatório, o relatório original permanece inalterado. No entanto, não é possível editá-lo na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou em um ambiente de criação do relatório que use um formato mais novo de definição do relatório. Você pode continuar a executar a versão original do relatório carregando-o para um [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de relatório usando o Gerenciador de relatórios. Para obter mais informações, consulte [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  
 Para relatórios carregados, e não publicados em um servidor de relatório, o processador de relatórios determina se o relatório pode ser atualizado no primeiro uso. Os relatórios que não podem ser atualizados são processados no modo de compatibilidade com versões anteriores e continuam a ser exibidos como ocorria na versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Alterações recentes no SQL Server Reporting Services no SQL Server 2014](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [Alterações de comportamento do SQL Server Reporting Services no SQL Server 2014](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [Itens de relatório personalizados](../custom-report-items/custom-report-items.md)   
 [Atualizar um banco de dados do servidor de relatório](upgrade-a-report-server-database.md)  
  
  
