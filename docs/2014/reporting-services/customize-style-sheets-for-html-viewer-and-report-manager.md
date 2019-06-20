---
title: Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de relatórios | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 7c7745d69e234f81c2a331d214789e93e9fd4014
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568259"
---
# <a name="customize-style-sheets-for-html-viewer-and-report-manager"></a>Personalizar folhas de estilo para o Visualizador de HTML e o Gerenciador de Relatórios
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece o estilo em cascata padrão arquivos de folha (. CSS) que definem estilos para o **relatório** barra de ferramentas no Visualizador de HTML e o Gerenciador de relatórios. Se você for um desenvolvedor Web ou possuir conhecimento especializado na criação de folhas de estilo em cascata, poderá modificar os tamanhos padrão por seu próprio risco para alterar cores, fontes e layout da barra de ferramentas do Gerenciador de Relatórios. Nem as folhas de estilo padrão nem as instruções para modificar as folhas de estilo são documentadas nesta versão.  
  
 Modificar as folhas de estilo incorretamente pode resultar em erros ao abrir relatórios. Se você não souber modificar folhas de estilo, deve usar as folhas de estilo padrão. Se escolher por personalizar as folhas de estilo, certifique-se de criar um backup para todos os arquivos .css padrão antes de efetuar qualquer modificação.  
  
 Modificar folhas de estilo não tem nenhum efeito na aparência de relatórios publicados e executados em um servidor de relatório pelo usuário. No [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], relatórios não fazem referência a folhas de estilo. Relatórios ad hoc gerados automaticamente pelo servidor de relatório usam informações de estilo armazenadas como recurso inserido nos arquivos de programa do servidor de relatório. Relatórios criados pelo usuário no Designer de Relatórios usam as fontes, cores e layout especificados na definição de relatório. Estilo são criados em correspondência com o restante do layout.  
  
> [!NOTE]  
>  Se desejar usar estilos de relatório predefinidos, use o Assistente de Relatório para criar um relatório. O Assistente de Relatório fornece uma variedade de temas que podem ser usados para criar relatórios estilizados com diferentes combinações de cores e fontes. Os modelos de estilo que definem os temas de um relatório podem ser modificados.  
  
## <a name="reporting-services-style-sheets"></a>Folhas de estilo do Reporting Services  
 A tabela a seguir descreve os arquivos de folha de estilo (.css) usados em uma instalação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|Folha de estilo|Descrição|  
|-----------------|-----------------|  
|Htmlviewer.css|Fornece uma folha de estilo de exemplo que pode ser usada como modelo para criar estilos personalizados para a barra de ferramentas do **relatório** no Visualizador de HTML.<br /><br /> Os estilos padrão usados pelo Visualizador de HTML são compilados no servidor de relatório. O arquivo Htmlviewer.css fornece um exemplo dos estilos usados pelo visualizador.|  
|ReportingServices.css|Define estilos para o Gerenciador de Relatórios.|  
  
## <a name="configuring-reporting-services-to-use-a-custom-style-sheet"></a>Configurando o Reporting Services para usar uma folha de estilo personalizada  
 É necessário que a folha de estilo seja um arquivo de folha de estilo em cascata (.css) localizado na pasta Estilos. Por padrão, a pasta estilos está localizada em \< *unidade*>: \Program Files\Microsoft SQL Server\MSSQL. *n*\Reporting Services\ReportServer\Styles.  
  
 Para usar uma folha de estilo personalizada em tempo de execução para o Visualizador de HTML, é possível escolher entre as seguintes abordagens:  
  
-   Adicione o <`HTMLViewerStyleSheet`> Definir como o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] arquivo de configuração.  
  
-   Especificar a folha de estilo em uma URL de relatório.  
  
### <a name="modifying-the-rsreportserverconfig-file"></a>Modificar o arquivo RSReportServer.config  
 É possível modificar o arquivo RSReportServer.config para especificar uma folha de estilo personalizada para o Visualizador de HTML. O <`HTMLViewerStyleSheet`> configuração não está incluída no arquivo por padrão. Você deve digitá-lo no <`Configuration`> seleção de rsreportserver. config arquivo e, em seguida, especifique a folha de estilos que você deseja usar. Não inclua a extensão de arquivo .css quando especificar a folha de estilo.  
  
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
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Visualizador de HTML e a barra de ferramentas de relatório](html-viewer-and-the-report-toolbar.md)   
 [Arquivo de configuração RSReportServer](report-server/rsreportserver-config-configuration-file.md)  
  
  
