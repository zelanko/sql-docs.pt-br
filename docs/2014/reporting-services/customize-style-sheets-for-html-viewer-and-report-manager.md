---
title: Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- style sheets [Reporting Services]
ms.assetid: df805cff-b1de-4062-b2ac-423f37390fbd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7903489a3fc34900ed8f717cc5a292f9af686af0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076976"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece o estilo em cascata padrão arquivos de folha (. CSS) que definem estilos para o **relatório** barra de ferramentas no Visualizador de HTML e o Gerenciador de relatórios. Se você for um desenvolvedor Web ou possuir conhecimento especializado na criação de folhas de estilo em cascata, poderá modificar os tamanhos padrão por seu próprio risco para alterar cores, fontes e layout da barra de ferramentas do Gerenciador de Relatórios. Nem as folhas de estilo padrão nem as instruções para modificar as folhas de estilo são documentadas nesta versão.  
  
 Modificar as folhas de estilo incorretamente pode resultar em erros ao abrir relatórios. Se você não souber modificar folhas de estilo, deve usar as folhas de estilo padrão. Se escolher por personalizar as folhas de estilo, certifique-se de criar um backup para todos os arquivos .css padrão antes de efetuar qualquer modificação.  
  
 Modificar folhas de estilo não tem nenhum efeito na aparência de relatórios publicados e executados em um servidor de relatório pelo usuário. No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], relatórios não fazem referência a folhas de estilo. Relatórios ad hoc gerados automaticamente pelo servidor de relatório usam informações de estilo armazenadas como recurso inserido nos arquivos de programa do servidor de relatório. Relatórios criados pelo usuário no Designer de Relatórios usam as fontes, cores e layout especificados na definição de relatório. Estilo são criados em correspondência com o restante do layout.  
  
> [!NOTE]  
>  Se desejar usar estilos de relatório predefinidos, use o Assistente de Relatório para criar um relatório. O Assistente de Relatório fornece uma variedade de temas que podem ser usados para criar relatórios estilizados com diferentes combinações de cores e fontes. Os modelos de estilo que definem os temas de um relatório podem ser modificados.  
  
## <a name="reporting-services-style-sheets"></a>Folhas de estilo do Reporting Services  
 A tabela a seguir descreve os arquivos (. CSS) de folha de estilo que são usados em um [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalação.  
  
|Folha de estilo|Description|  
|-----------------|-----------------|  
|Htmlviewer.css|Fornece uma folha de estilo de exemplo que pode ser usada como modelo para criar estilos personalizados para a barra de ferramentas do **relatório** no Visualizador de HTML.<br /><br /> Os estilos padrão usados pelo Visualizador de HTML são compilados no servidor de relatório. O arquivo Htmlviewer.css fornece um exemplo dos estilos usados pelo visualizador.|  
|ReportingServices.css|Define estilos para o Gerenciador de Relatórios.|  
  
> [!NOTE]  
>  As folhas de estilo a seguir são usadas para documentação on-line do Gerenciador de Relatórios e nunca devem ser modificadas: Sql.css e Mailto.css. Outras folhas de estilo definem estilos para relatórios e para o Gerenciador de Relatórios que abrem em Web parts do SharePoint. Algumas dessas folhas de estilo são Rswebparts.css, Sp_full.css e Sp_small.css. Não é recomendado modificar as folhas de estilo do SharePoint. Para obter mais informações sobre como as Web parts são usadas, consulte [exibir e explorar nativo modo relatórios usando Web Parts do SharePoint &#40;SSRS&#41;](reports/view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs.md).  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>Configurando o Reporting Services para usar uma folha de estilo personalizada  
 É necessário que a folha de estilo seja um arquivo de folha de estilo em cascata (.css) localizado na pasta Estilos. Por padrão, a pasta estilos está localizada em \< *unidade*>: \Program Files\Microsoft SQL Server\MSSQL. *n*\Reporting Services\ReportServer\Styles.  
  
 Para usar uma folha de estilo personalizada em tempo de execução para o Visualizador de HTML, é possível escolher entre as seguintes abordagens:  
  
-   Adicionar a configuração <`HTMLViewerStyleSheet`> ao arquivo de configuração do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Especificar a folha de estilo em uma URL de relatório.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>Modificar o arquivo RSReportServer.config  
 É possível modificar o arquivo RSReportServer.config para especificar uma folha de estilo personalizada para o Visualizador de HTML. Por padrão, a configuração <`HTMLViewerStyleSheet`> não é incluída no arquivo. É necessário digitá-lo na seleção <`Configuration`> do arquivo RSReportServer.config e depois especificar a folha de estilo desejada. Não inclua a extensão de arquivo .css quando especificar a folha de estilo.  
  
 O exemplo a seguir ilustra de como especificar a folha de estilo:  
  
```  
<Configuration>  
...  
          <HTMLViewerStyleSheet>MyStyleSheet</HTMLViewerStyleSheet>  
...  
</Configuration>  
```  
  
### <a name="specifying-a-style-sheet-on-a-report-url"></a>Especificando uma folha de estilo em uma URL de relatório  
 É possível usar o parâmetro de acesso a URL `rc:StyleSheet` para especificar uma folha de estilo personalizada na URL do relatório. Para obter mais informações sobre como especificar parâmetros de acesso de URL, consulte [URL Access Parameter Reference](url-access-parameter-reference.md).  
  
 O exemplo a seguir ilustra como adicionar estilos personalizados:  
  
```  
http://localhost/reportserver?/AdventureWorksSampleReports/Product+Line+Sales&rs:Command=Render&rc:Stylesheet=MyStyleSheet  
```  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visualizador de HTML e a barra de ferramentas de relatório](html-viewer-and-the-report-toolbar.md)   
 [Arquivo de configuração RSReportServer](report-server/rsreportserver-config-configuration-file.md)  
  
  
