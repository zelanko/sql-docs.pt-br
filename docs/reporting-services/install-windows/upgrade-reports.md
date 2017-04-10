---
title: "Atualizar relat&#243;rios | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "relatórios [Reporting Services], atualizando"
  - "relatórios publicados [Reporting Services], atualizações"
  - "itens de relatório personalizados, atualizando"
  - "Reporting Services, atualizações"
  - "atualizando o Reporting Services"
  - "instantâneos [Reporting Services], atualizando"
  - "arquivos de definição de relatório [Reporting Services]"
  - "arquivos .rdl"
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
caps.latest.revision: 70
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 67
---
# Atualizar relat&#243;rios
  Os arquivos de definição de relatório (.rdl) são automaticamente atualizados da seguinte forma:  
  
-   Quando você abre um relatório no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a definição do relatório é atualizada para o esquema RDL com suporte no momento. Quando você especifica um servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] nas propriedades de projeto, a definição de relatório é salva em um esquema que é compatível com o servidor de destino.  
  
-   Quando você atualiza uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para uma instalação do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], os relatórios e instantâneos existentes que foram publicados em um servidor de relatório são compilados e atualizados automaticamente para o novo esquema na primeira vez que são processados. Se não for possível atualizar um relatório automaticamente, o relatório será processado usando o modo da compatibilidade com versões anteriores. A definição de relatório permanece no esquema original.  
  
 Os relatórios não são atualizados quando você carrega um arquivo de definição de relatório diretamente no servidor de relatório ou no site do SharePoint. A atualização de uma definição de relatório no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] é a única maneira de atualizar o arquivo .rdl.  
  
 Após a atualização de um relatório localmente ou no servidor de relatório, talvez você encontre erros, avisos e mensagens adicionais. Esse é o resultado das alterações no modelo de objeto de relatório interno e nos componentes de processamento, que fazem com que mensagens sejam exibidas quando forem detectados problemas subjacentes no relatório. Para obter mais informações, consulte [Reporting Services Backward Compatibility](../../reporting-services/reporting-services-backward-compatibility.md).  
  
 Para obter mais informações sobre os novos recursos do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], veja [Novidades no Reporting Services&#40;SSRS&#41;](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md).  
  
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
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> Arquivos de definição de relatório (.rdl) e Designer de Relatórios  
 Um arquivo de definição de relatório inclui uma referência ao namespace do RDL que especifica a versão do esquema de definição de relatório usado para validar o arquivo .rdl.  
  
 Ao abrir um arquivo .rdl no Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se o relatório tiver sido criado para um namespace anterior, o Designer de Relatórios criará automaticamente um arquivo de backup e atualizará o relatório para o namespace atual. Esse é o único modo que você pode atualizar um arquivo de definição de relatório.  
  
 As propriedades da implantação que você define podem afetar em qual esquema o arquivo de definição de relatório é salvo. Para obter mais informações, veja [Implantação e suporte de versão no SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
 Você pode carregar um arquivo .rdl criado em uma versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e ele será atualizado automaticamente na primeira vez que for usado. O servidor de relatório armazena o arquivo de definição de relatório no formato original. O relatório será atualizado automaticamente na primeira vez que for exibido, mas o arquivo de definição de relatório armazenado permanecerá inalterado.  
  
 Para identificar o esquema RDL atual de um relatório, um servidor de relatório ou do Designer de Relatórios, veja [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> Relatórios publicados e instantâneos de relatório  
 Na primeira vez que for usado, o servidor de relatório tentará atualizar os relatórios publicados e os instantâneos de relatório existentes para o novo esquema de definição de relatório, sem exigir uma ação específica de sua parte. Quando um usuário exibe um relatório ou um instantâneo de relatório, ou quando o servidor de relatório processa uma assinatura, ocorre uma tentativa de atualização. A definição de relatório não é substituída, mas continua sendo armazenada no servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em seu esquema original. Se um relatório não puder ser atualizado, ele será executado no modo da compatibilidade com versões anteriores.  
  
##  <a name="bkmk_backcompat"></a> Modo de compatibilidade com versões anteriores  
 Um relatório atualizado com êxito é processado pelo processador de relatório [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Um relatório que não pode ser atualizado é processado pelo processador de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo da compatibilidade com versões anteriores. Um relatório não pode ser processado pelos dois processadores de relatório. Na primeira vez que for usado, um relatório será atualizado com êxito ou marcado para compatibilidade com versões anteriores.  
  
 Só o processador de relatório [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] dá suporte a novos recursos. Se não for possível atualizar um relatório, você ainda poderá exibir o relatório renderizado, mas os recursos novos não estarão disponíveis. Para se beneficiar dos recursos novos, um relatório deverá ser atualizado com êxito.  
  
##  <a name="bkmk_subreports"></a> Atualizando um relatório com sub-relatórios  
 Quando um relatório contiver sub-relatórios, um de quatro possíveis estados poderá ocorrer durante a atualização:  
  
-   O relatório principal e todos os sub-relatórios podem ser atualizados com êxito. Eles são processados pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
-   O relatório principal e todos os sub-relatórios não podem ser atualizados. Eles são processados pelo processador de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   O relatório principal pode ser atualizado, entretanto um ou mais sub-relatórios não podem ser atualizados. O relatório principal é processado pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mas o relatório renderizado mostra a mensagem "Erro: não foi possível processar o sub-relatório" no local onde o sub-relatório que não foi atualizado seria exibido.  
  
-   Não é possível atualizar o relatório principal, entretanto é possível atualizar um ou mais sub-relatórios. O relatório principal é processado pelo processador de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mas o relatório renderizado mostra a mensagem "Erro: não foi possível processar o sub-relatório" no local onde o sub-relatório seria exibido.  
  
 Se você visualizar o erro "Erro: não foi possível processar o sub-relatório", deverá alterar a definição do relatório principal ou do sub-relatório de forma que os relatórios possam ser processados pela mesma versão do processador de relatórios.  
  
 Relatórios detalhados não têm esta limitação porque eles são processados como relatórios independentes.  
  
##  <a name="bkmk_CRIs"></a> Atualizando um relatório com itens de relatório personalizados  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem conter CRIs (itens de relatórios personalizados) fornecidos por fornecedores de software de terceiros e instalados pelo administrador do sistema no computador de criação de relatório e no servidor de relatório. Os relatórios que contêm CRIs podem ser atualizados dos seguintes modos:  
  
-   Um servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é atualizado para um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Os relatórios publicados no servidor de relatório serão atualizados automaticamente na primeira vez que forem usados.  
  
-   Um relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é carregado em um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. O relatório será atualizado automaticamente na primeira vez que for usado.  
  
-   Um relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é aberto no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Uma cópia de backup do relatório original é criada. Ocorrerá um dos dois casos seguintes:  
  
    1.  Todos o CRIs no relatório não têm recurso sem-suporte. Os CRIs são convertidos em itens de relatório no novo esquema de definição de relatório, portanto, o relatório inteiro é atualizado. Se você salvar o arquivo, ele será salvo no namespace da RDL atual.  
  
    2.  Um ou mais CRIs no relatório têm recursos sem-suporte. Uma caixa de diálogo avisa o usuário se deve converter os CRIs ou deixá-los inalterados.  
  
     Para obter mais informações, consulte [Abrindo um relatório no Designer de Relatórios](#OpeningaReport) posteriormente neste tópico.  
  
 Para obter informações sobre como identificar o namespace de RDL atual de um servidor de relatório, do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou de um relatório, veja [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
### Atualizando relatórios em um servidor de relatório  
 Na primeira vez que um relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é executado em um servidor de relatório que foi atualizado para um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , ele é atualizado automaticamente para o namespace de definição de relatório atual suportado pelo servidor de relatório. O relatório poderia ter existido no servidor de relatório antes da atualização ou ter sido carregado por meio do Gerenciador de Relatórios ou publicado para o servidor de relatório do Designer de Relatórios no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 A tabela seguinte lista a ação de atualização que é executada pelo servidor de relatório para tipos específicos de CRIs em um relatório.  
  
|Tipo de CRI|Ação de atualização do servidor de relatório|  
|--------------|----------------------------------|  
|CRIs de terceiros|Atualização não executada.<br /><br /> Processado pelo processador do relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
###  <a name="OpeningaReport"></a> Abrindo um Relatório com CRIs no Designer de Relatórios  
 Quando você abrir um relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com CRIs no Designer de Relatórios no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o relatório será atualizado para o novo esquema de definição de relatório. Dependendo dos CRIs contidos no relatório, uma das seguintes ações ocorrerá:  
  
-   CRIs de terceiros detectados. Se a versão do CRI que está instalada no computador de criação de relatórios não for compatível com o novo esquema rdl, a superfície do design mostrará uma caixa de texto com um X vermelho. Você deverá contatar o administrador do sistema para instalar novas versões do CRI de fornecedores de terceiros que sejam compatíveis com o novo esquema rdl.  
  
 Salvar um relatório depois de ele ser atualizado no ambiente de criação de relatórios é a única maneira de atualizar um relatório existente para o novo esquema de definição de relatório.  
  
###  <a name="bkmk_convertCRIdialog"></a> Caixa de diálogo Converter CRI  
 Este relatório contém CRIs (itens de relatório personalizados) com recursos sem suporte. CRIs são extensões para a linguagem RDL (Report Definition Language) que oferecem suporte a objetos personalizados que exibem dados em um relatório. Os CRIs incluem componentes em tempo de design e em tempo de execução oferecidos por fornecedores de software de terceiros.  
  
> [!NOTE]  
>  Optar por oferecer suporte a itens de relatório personalizados em um servidor de relatório é uma decisão tomada pelo administrador do sistema. Para exibir CRIs em um relatório, os componentes do CRI devem ser instalados no cliente de criação do relatório para visualizar um relatório e no servidor de relatório para exibir um relatório publicado ou carregado. Para obter mais informações, veja [Itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-items.md) e a documentação do fornecedor de software de terceiros.  
  
 Alguns CRIs podem ser convertidos em itens de relatório no novo formato de definição do relatório. Use a seguinte lista para decidir se você deve converter os CRIs nesse relatório:  
  
-   **Sim** Escolha **Sim** para converter todos os CRIs do relatório, quando possível. Recursos para os quais não há suporte nos CRIs não podem ser atualizados, sendo removidos do arquivo de definição do relatório. Ao exibir o relatório, você pode ver as diferenças na forma como o CRI é exibido no relatório.  
  
-   **Não** Escolha **Não** quando não quiser converter os CRIs do relatório. Esses CRIs não podem ser exibidos pelo processador de relatório na versão atual. Caso o administrador do sistema pretenda instalar uma nova versão da CRI do fornecedor de software de terceiros compatível com o novo formato de definição do relatório, escolha **Não**. Até que as novas versões estejam disponíveis, os CRIs são exibidos no relatório como uma caixa de texto vazia com um X vermelho.  
  
 Em ambos os casos, o relatório é atualizado para o novo formato de definição de relatório e uma cópia de backup do relatório original é salva como *\<Report Name>* `-` Backup.rdl. Caso salve o relatório na ferramenta de criação do relatório, você está salvando o relatório atualizado no novo formato de definição do relatório. Caso você publique o relatório, ele é salvo primeiro no computador e, em seguida, publicado no servidor de relatório. Você está publicando a versão atualizada do relatório no servidor de relatório.  
  
 Caso você não salve o relatório, o relatório original permanece inalterado. No entanto, não é possível editá-lo na versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou em um ambiente de criação do relatório que use um formato mais novo de definição do relatório. Você pode continuar executando a versão original do relatório, carregando-o em um servidor de relatório do [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] usando o Gerenciador de Relatórios. Para obter mais informações, veja [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
 Para relatórios carregados, e não publicados em um servidor de relatório, o processador de relatórios determina se o relatório pode ser atualizado no primeiro uso. Os relatórios que não podem ser atualizados são processados no modo de compatibilidade com versões anteriores e continuam a ser exibidos como ocorria na versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## Consulte também  
 [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [Alterações recentes no SQL Server Reporting Services do SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [Alterações de comportamento do SQL Server Reporting Services in SQL Server 2016](../../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2016](../Topic/Discontinued%20Functionality%20to%20SQL%20Server%20Reporting%20Services%20in%20SQL%20Server%202016.md)   
 [Itens de Relatório Personalizados](../../reporting-services/custom-report-items/custom-report-items.md)   
 [Atualizar um banco de dados do servidor de relatório](../../reporting-services/install-windows/upgrade-a-report-server-database.md)  
  
  