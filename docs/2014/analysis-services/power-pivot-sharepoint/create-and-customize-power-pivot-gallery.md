---
title: Criar e personalizar a galeria do PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b5cd35e0-3d8f-4784-9172-93d60c730321
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 305ae31522a54a776c989f4b8f4b0c4ceabe6658
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "70874402"
---
# <a name="create-and-customize-powerpivot-gallery"></a>Criar e personalizar uma galeria do PowerPivot
  A Galeria PowerPivot é um tipo especial de biblioteca de documentos do SharePoint que fornece visualização avançada e gerenciamento de documentos para pastas de trabalho do Excel publicadas e Reporting Services relatórios que contêm dados PowerPivot.  
  
##  <a name="bkmk_top"></a>Neste tópico  
  
-   [Pré-requisitos](#prereq)  
  
-   [Sobre](#overview)  
  
-   [Criar a Galeria PowerPivot](#createlib)  
  
-   [Personalizar uma biblioteca da Galeria PowerPivot](#customize)  
  
-   [Desabilitar ou ocultar o botão de atualização](#bkmk_hide_refresh_button)  
  
-   [Alternar para exibição de teatro ou exibição de galeria](#switch)  
  
##  <a name="prereq"></a>Pré-requisitos  
  
-   Você deve ter o Silverlight. O Silverlight pode ser baixado e instalado por meio de Microsoft Update. Se você exibir um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] biblioteca da Galeria usando um navegador que não tenha o Silverlight, clique no link na página para instalá-lo. Você deve fechar e reabrir o navegador depois de instalá-lo.  
  
    > [!NOTE]  
    >  A Galeria de Power Pivot requer o Microsoft Silverlight.  O navegador Microsoft Edge não oferece suporte ao Silverlight.   
    > Para exibir o conteúdo da biblioteca no Microsoft Edge, clique na guia **biblioteca** na Galeria Power pivot e altere a exibição da biblioteca de documentos para **todos os documentos**.    
    > Para alterar o modo de exibição padrão, clique na guia **biblioteca** e, em seguida, clique em modificar modo de exibição. Clique em "tornar este o modo de exibição padrão" e, em seguida, clique em OK para salvar o modo de exibição padrão.  
    >  Para obter mais informações sobre o que o Microsoft Edge dá suporte, consulte o blog do Windows, [um intervalo do passado, parte 2: dizendo adeus ao ActiveX, VBScript...](http://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/)  
  
-   Você deve ser um proprietário do site para criar uma biblioteca.  
  
-   Você deve ter permissões de colaboração ou acima para publicar ou carregar um arquivo.  
  
-   a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não pode estar em um site restrito. O site pai que contém a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ser adicionado ao site confiável ou à zona da intranet local.  
  
-   A solução de aplicativo Web [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ter sido implantada para seu aplicativo e o recurso de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ter sido ativado para o conjunto de sites. Para obter mais informações, consulte [implantar soluções PowerPivot no SharePoint](deploy-power-pivot-solutions-to-sharepoint.md) e[ativar a integração de recursos do PowerPivot para coleções de sites na administração central](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
-   Para exibir ou criar um relatório Reporting Services com base em uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], a pasta de trabalho e o relatório devem estar na mesma galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]. O relatório deve usar uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contenha dados inseridos ou a pasta de trabalho deve conter no máximo uma fonte de dados externa que seja uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
##  <a name="overview"></a>Sobre  
 a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é um modelo de biblioteca que está disponível quando você instala o [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] em um servidor do SharePoint. A Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] combina uma visualização precisa do conteúdo do arquivo com fatos sobre a origem do documento. Você pode ver imediatamente quem criou o documento e quando ele foi modificado pela última vez. Para criar imagens de visualização, a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa um serviço de instantâneo que pode ler [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pastas de trabalho e Reporting Services relatórios que contêm dados PowerPivot. Se você publicar um arquivo que o serviço de instantâneo não possa ler, nenhuma imagem de visualização estará disponível para esse arquivo.  
  
 As imagens de visualização são baseadas em como a pasta de trabalho é renderizada pelos serviços do Excel. A representação na Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ser idêntica ao que você vê ao exibir uma pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um navegador. No entanto, a visualização tem uma área de superfície limitada. Partes de uma pasta de trabalho ou relatório podem ser cortados para se ajustarem ao espaço disponível. Talvez seja necessário abrir uma pasta de trabalho ou relatório para exibir o documento em sua totalidade.  
  
 A atualização de dados de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pasta de trabalho de fontes de dados externas tem suporte total na Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], mas requer configuração adicional. Um administrador de farm ou de serviço deve adicionar a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como um local confiável dos serviços do Excel. Para obter mais informações, consulte [criar um local confiável para sites do PowerPivot na administração central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
##  <a name="createlib"></a>Criar a Galeria PowerPivot  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Galeria é criada quando você instala [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] usando a opção de instalação do novo servidor. Se você adicionou [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] a um farm existente ou se quiser uma biblioteca adicional, poderá criar um novo para seu aplicativo ou site.  
  
1.  1.  **SharePoint 2010**: clique em **ações do site** no canto superior esquerdo da home page do seu site.  
  
    2.  Clique em **mais opções**.  
  
    3.  Em Bibliotecas, clique em **Galeria PowerPivot**.  
  
    1.  **Sharepoint 2013**: clique no ícone de configurações ![configurações do SharePoint](../media/as-sharepoint2013-settings-gear.gif "Configurações do SharePoint"). Clique em **Conteúdo do Site**  
  
    2.  Clique em **Adicionar um aplicativo**.  
  
    3.  Clique em **Galeria PowerPivot**.  
  
2.  Digite um nome para a biblioteca. Certifique-se de incluir informações descritivas que ajudem os usuários a identificar essa biblioteca como visualização avançada para pastas de trabalho PowerPivot e relatórios de Reporting Services.  
  
3.  Clique em **criar**.  
  
4.  Peça a um administrador de farm ou de serviço para adicionar a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como um local confiável para os serviços do Excel. Essa etapa será necessária para evitar erros se um usuário configurar uma pasta de trabalho para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] atualização de dados. Para obter mais informações sobre essa tarefa, consulte [criar um local confiável para sites do PowerPivot na administração central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
 Um link para a biblioteca da Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aparecerá no painel início rápido de navegação do site atual.  
  
 Você pode criar mais bibliotecas da Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se estiver impondo permissões diferentes para diferentes conjuntos de sites ou sites individuais.  
  
##  <a name="customize"></a>Personalizar uma biblioteca da Galeria PowerPivot  
 a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é uma biblioteca de documentos do SharePoint. Portanto, você pode usar ferramentas de biblioteca padrão no SharePoint para alterar as configurações da biblioteca ou trabalhar com documentos individuais na biblioteca. Cada biblioteca que você cria pode ser personalizada independentemente para usar uma exibição ou configurações de biblioteca diferentes.  
  
 A ordem de classificação e os filtros podem ser modificados para alterar onde as pastas de trabalho aparecem na lista. Por padrão, os documentos são listados na ordem em que foram adicionados, onde o último documento publicado aparece na parte inferior da lista. Depois que um documento é publicado, ele retém seu lugar na lista. Atualizar e republicar o documento atualiza-o no local na lista.  
  
 Você não pode habilitar ou desabilitar a visualização para documentos específicos. O serviço de instantâneo irá gerar imagens de visualização para todas as pastas de trabalho PowerPivot e para Reporting Services relatórios baseados em pastas de trabalho PowerPivot que são armazenadas na mesma biblioteca. Essas imagens podem ser exibidas por todos os usuários que têm permissões de exibição no documento.  
  
 Você não pode estender [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] galeria para fornecer visualização para outros tipos de documento. A visualização só tem suporte para pastas de trabalho do Excel 2010 ou SQL Server 2008 R2 Reporting Services relatórios que contenham dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
 Você não pode alterar as configurações que controlam as informações de origem do documento. Os fatos que aparecem sobre documentos individuais, como quem adicionou ou modificou a pasta de trabalho, são determinados por um conjunto fixo de colunas que não podem ser modificadas.  
  
#### <a name="change-sort-order-add-filters-or-limit-the-number-of-documents"></a>Alterar a ordem de classificação, adicionar filtros ou limitar o número de documentos  
 a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sempre mostra os valores ' última modificação ' e ' criado por '. Não é possível desabilitar essas colunas. Não é possível habilitar outras colunas para a biblioteca. Use as instruções a seguir para alterar a ordem de classificação, adicionar um filtro ou limitar o número de documentos visíveis.  
  
1.  Em um site do SharePoint, abra a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
2.  Na faixa de faixas, clique em **biblioteca**.  
  
3.  **SharePoint 2010:** Em exibições personalizadas, clique em **modificar esta exibição**.  
  
     **SharePoint 2013:** Em **gerenciar exibições**, clique em **Modificar modo de exibição**.  
  
4.  Em classificar, especifique os critérios que serão usados para determinar como as pastas de trabalho aparecem na lista. Por padrão, os documentos são listados na ordem em que foram adicionados.  
  
5.  Em filtro, especifique os critérios que serão usados para mostrar ou Ocultar pastas de trabalho com base em valores condicionais definidos em colunas. Por exemplo, talvez você queira ocultar todas as pastas de trabalho criadas antes de uma determinada data.  
  
6.  Em limite de itens, especifique as opções que são úteis para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] bibliotecas da galeria que contêm um número muito grande de documentos. Você pode limitar o número real de itens que aparecem na lista ou exibir itens em lotes.  
  
7.  Clique em **OK** para salvar as alterações.  
  
####  <a name="bkmk_hide_refresh_button"></a>Desabilitar ou ocultar o botão de atualização  
 Não é possível ocultar o botão **gerenciar atualização de dados** . No entanto, o botão será desabilitado se o usuário não tiver permissões suficientes.  
  
 ![as_powerpivot_refresh_manage_reresh](../media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh")  
  
 Os proprietários ou autores da pasta de trabalho devem ter permissão de **colaboração** para agendar a atualização de dados em uma pasta de trabalho. Os usuários com permissões do Contribute podem abrir e editar a página de configuração de atualização de dados da pasta de trabalho para especificar as credenciais e as informações de agendamento usadas para atualizar os dados.  
  
 Portanto, os usuários que só têm níveis de permissão de **exibição** ou **leitura** não poderão acessar o botão atualizar. O botão Atualizar está visível, mas desabilitado. Para obter mais informações, consulte [permissões de usuário e níveis de permissão no SharePoint 2013](https://technet.microsoft.com/library/cc721640.aspx).  
  
##  <a name="switch"></a>Alternar para exibição de teatro ou exibição de galeria  
 A visualização varia dependendo de como você configura a exibição da biblioteca. No modo de exibição de galeria, você pode passar o ponteiro do mouse sobre planilhas individuais na pasta de trabalho para colocar uma planilha em foco na área de visualização.  
  
 ![GMNI_ReportGallery](../media/gmni-reportgallery.gif "GMNI_ReportGallery")  
  
 A tabela a seguir descreve os diferentes layouts para apresentar esboços em miniatura de cada página visualizada:  
  
|Exibição|Description|  
|----------|-----------------|  
|Exibição da galeria (padrão)|Galeria é a exibição padrão para uma Galeria [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . A visualização é exibida à esquerda. Miniaturas menores de cada planilha aparecem ao lado dela em uma ordem sequencial da esquerda para a direita.|  
|Todos os documentos|Este é o layout padrão para bibliotecas de documentos. Você pode escolher essa exibição para gerenciar documentos individuais ou exibir o conteúdo da biblioteca em um formato de lista.<br /><br /> Use esta exibição para editar propriedades, excluir ou mover documentos individuais.<br /><br /> Se você tiver habilitado o controle de versão, deverá usar essa exibição para verificar os documentos dentro ou fora da biblioteca.|  
|Exibição de teatro e exibição de carrossel|Essas são exibições especializadas que funcionam melhor se você estiver mostrando um pequeno número de documentos relacionados. A rotação completa de miniaturas inclui todas as páginas de todos os documentos na biblioteca. Se você tiver um grande número de documentos, essas exibições poderão ser impraticável para os usuários que desejam localizar ou abrir uma pasta de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] específica.<br /><br /> Exibição de teatro: a área de visualização está centralizada. Miniaturas menores de cada planilha aparecem na parte inferior da página, em ambos os lados.<br /><br /> Exibição de carrossel: a área de visualização está centralizada. As miniaturas que precedem e seguem imediatamente a miniatura atual são adjacentes à área de visualização.|  
  
### <a name="switch-to-a-different-view"></a>Alternar para uma exibição diferente  
  
1.  Em um site do SharePoint, abra a Galeria de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
2.  Na faixa de faixas, clique em **biblioteca**.  
  
3.  Em gerenciar exibições, na exibição atual, selecione a exibição que você deseja usar na lista. As exibições predefinidos incluem Galeria, teatro e carrossel. Como alternativa, você pode escolher todos os documentos se desejar mover, excluir ou gerenciar documentos na biblioteca.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de uma instalação do PowerPivot para SharePoint](../../sql-server/install/troubleshoot-a-powerpivot-for-sharepoint-installation.md)    
 [Usar a Galeria PowerPivot](use-power-pivot-gallery.md)    
 [Criar um local confiável para sites do PowerPivot na Administração Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)    
 [Excluir Galeria PowerPivot](delete-power-pivot-gallery.md)  
  
  
