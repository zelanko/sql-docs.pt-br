---
title: Visualizador de HTML e a barra de ferramentas de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTML Viewer [Reporting Services]
- report toolbar [Reporting Services]
ms.assetid: cd86b319-babd-45af-a6a4-f659fdcc40c3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b8043bb8f95ea67dbc3dceedc9cfd0154b033d51
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109048"
---
# <a name="html-viewer-and-the-report-toolbar"></a>Visualizador de HTML e a barra de ferramentas de relatório
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] fornece um Visualizador de HTML usado para exibir relatórios sob demanda à medida que são solicitados no servidor de relatório. O Visualizador de HTML fornece uma estrutura para exibir relatórios em HTML. Ele inclui uma barra de ferramentas de relatório, uma seção de parâmetros, uma seção de credenciais e um mapa do documento. A barra de ferramentas de relatório no Visualizador de HTML inclui recursos que você pode usar para trabalhar com seu relatório, incluindo opções de exportação para que seja possível exibir seu relatório em formatos diferentes de HTML. A seção de parâmetros e o mapa do documento aparecem somente quando você abre relatórios configurados para usar parâmetros e um controle do mapa do documento.  
  
> [!NOTE]  
>  Embora não seja possível modificar a barra de ferramentas de relatório, você pode configurar os parâmetros em uma URL de relatório para ocultá-la em um relatório. Para obter mais informações sobre como ocultar barra de ferramentas de relatório, consulte [Referência de parâmetro de acesso à URL](url-access-parameter-reference.md).  
  
## <a name="report-toolbar"></a>Barra de ferramentas de relatório  
 A barra de ferramentas de relatório fornece as funcionalidades de navegação na página, zoom, atualização, pesquisa, exportação, impressão e feed de dados para relatórios renderizados na extensão de renderização HTML.  
  
 A funcionalidade de impressão é opcional. Quando disponível, um ícone Impressora é exibido na barra de ferramentas de relatório. No primeiro uso, quando você clicar no ícone Impressora, um controle ActiveX será baixado e deverá ser instalado. Quando o controle estiver instalado e você clicar no ícone Impressora, a caixa de diálogo Imprimir será aberta para a seleção das impressoras configuradas para seu computador. A disponibilidade de impressão é determinada pelas configurações do servidor e navegador. Para obter mais informações, consulte [Imprimir relatórios em um navegador com o controle de impressão &#40;Construtor de Relatórios e SSRS&#41;](report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md) e [Habilitar e desabilitar a impressão do lado do cliente para o Reporting Services](report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
 A barra de ferramentas de relatório é semelhante à ilustração a seguir. A barra de ferramentas de relatório exibida pode ser diferente da ilustração com base nos recursos do relatório ou nas opções de renderização disponíveis.  
  
 ![Barra de ferramentas do relatório](media/htmlviewer-toolbar.gif "Barra de ferramentas do relatório")  
  
 A tabela a seguir descreve recursos geralmente usados da barra de ferramentas de relatório. Cada recurso é identificado pelo controle que você usa para acessá-lo.  
  
|Use este ícone ou controle||Para|  
|------------------------------|-|--------|  
|![Controles de navegação de página](media/htmlviewer-pagenav.gif "Controles de navegação de página")|**Controles de navegação de página**|Abrir a primeira ou a última página de um relatório, percorrer o relatório página por página e abrir uma página específica no relatório. Para exibir uma página específica, digite o número da página e pressione ENTER.|  
|![Controles de exibição de página](media/htmlviewer-pagesize.gif "Controles de exibição de página")|**Controles de exibição de página**|Aumentar ou reduzir o tamanho da página do relatório. Além das alterações com base em percentual, você pode selecionar **Largura da Página** para ajustar o comprimento horizontal de uma página de relatório na janela do navegador ou **Página Inteira** para ajustar o comprimento vertical de um relatório na janela do navegador. Uma opção **Zoom** tem suporte no [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 5.5 e versões posteriores.|  
|![Campo de pesquisa](media/htmlviewer-search.gif "Campo de pesquisa")|**Campo de pesquisa**|Procure o conteúdo no relatório digitando uma palavra ou frase que deseja localizar (o comprimento máximo do valor é 256 caracteres). A pesquisa diferencia maiúsculas e minúsculas e começa na página ou seção selecionada no momento. Somente conteúdo visível é incluído em uma operação de pesquisa. Para procurar ocorrências subsequentes do mesmo valor, clique em **Próximo**.|  
|![Formatos de exportação](media/htmlviewer-export.GIF "Formatos de exportação")|**Formatos de exportação**|Abra uma nova janela de navegador e renderize o relatório no formato selecionado. Os formatos disponíveis são determinados pelas extensões de renderização instaladas no servidor de relatório. TIFF é recomendado para imprimir. Clique em **Exportar** para exibir o relatório no formato selecionado.|  
|![Ícone do mapa do documento](media/htmlviewer-docmap.GIF "Ícone do mapa do documento")|**Ícone do mapa do documento**|Mostrar ou ocultar o painel de mapa do documento em um relatório que inclui um mapa do documento. Um mapa do documento é um controle de navegação de relatório semelhante ao painel de navegação em um site da Web. Você pode clicar em itens no mapa do documento navegar até um grupo específico, uma página ou um sub-relatório.|  
|![Ícone de impressora](media/printer-icon.gif "Ícone de impressora")|**Ícone de impressora**|Abrir uma caixa de diálogo de impressão para que você possa especificar opções de impressão e imprimir um relatório. No primeiro uso, ao clicar nesse ícone você deverá baixar o controle de impressão.|  
||**Mostrar e ocultar ícones**|Mostrar ou ocultar campos de valor de parâmetro e o botão **Exibir Relatório** em um relatório que inclui parâmetros.|  
|![Botão Atualizar do navegador na barra de ferramentas de relatório](media/htmlviewer-refresh.GIF "Botão Atualizar do navegador na barra de ferramentas de relatório")|**Ícone de atualização de relatório**|Atualizar o relatório. Os dados de relatórios dinâmicos serão atualizados. Os relatórios armazenados em cache serão recarregados de onde estão armazenados.|  
|![htmlviewer_datafeed](media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|**Ícone de feed de dados**|Feeds de dados gerados de relatórios.|  
  
### <a name="about-export-formats"></a>Sobre formatos de exportação  
 Na barra de ferramentas de relatório, você pode optar por exibir seu relatório em vários formatos. Os formatos disponíveis são determinados pelas extensões de renderização instaladas no servidor de relatório. Quando você seleciona outro formato, uma segunda janela do navegador é usada para exibir o relatório com um visualizador associado ao formato de exportação selecionado. Se um visualizador não estiver disponível para o formato selecionado, você poderá selecionar um formato diferente.  
  
 Os formatos de exportação a seguir são incluídos em uma instalação de servidor de relatório padrão. A lista de formatos de exportação disponíveis pode conter itens diferentes dos listados aqui.  
  
|Formato de exportação|Descrição|  
|-------------------|-----------------|  
|XML|Exiba um relatório em sintaxe XML. Relatórios exibidos em XML são abertos em uma nova janela do navegador.|  
|CSV|Exiba um relatório em um formato delimitado por vírgula. O relatório é aberto em um aplicativo associado ao tipo de arquivo CSV.|  
|Arquivo do Acrobat (PDF)|Exiba um relatório usando um visualizador de PDF cliente. Você deve ter um visualizador de PDF de terceiros (por exemplo, Adobe Acrobat Reader) para usar esse formato.|  
|Excel|Exiba o relatório no [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel.|  
|Arquivo da Web|Exiba o relatório em um formato HTML codificado em MIME que mantém as imagens e o conteúdo vinculado juntos no relatório.|  
|Arquivo TIFF|Exiba o relatório no visualizador TIFF padrão. Para alguns clientes do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows, esse é o Visualizador de Imagens e Fax do Windows. Selecione esse formato para exibir um relatório em layout orientado a página.|  
  
## <a name="parameters"></a>Parâmetros  
 Parâmetros são valores usados para selecionar determinados dados (especificamente, eles são usados para concluir uma consulta que seleciona os dados para o seu relatório ou para filtrar o conjunto de resultados). Parâmetros geralmente usados em relatórios incluem datas, nomes e IDs. Quando você especifica um valor para um parâmetro, o relatório contém somente os dados que correspondem ao valor; por exemplo, dados de funcionário com base em um parâmetro de ID de Funcionário. Parâmetros correspondem a campos no relatório. Depois de especificar um parâmetro, clique em **Exibir Relatório** para obter os dados.  
  
 O autor do relatório define os valores de parâmetro que são válidos para cada relatório. Um administrador de relatório também pode definir valores de parâmetro. Para descobrir quais valores de parâmetro são válidos para seu relatório, pergunte ao designer de relatórios ou ao administrador.  
  
## <a name="credentials"></a>Credenciais  
 Credenciais são valores de nome de usuário e senha que concedem acesso a uma fonte de dados. Depois de especificar suas credenciais, clique em **Exibir Relatório** para obter os dados. Se um relatório exigir que você faça logon, os dados que você está autorizado a visualizar podem diferir dos dados que outros usuários veem. Consequentemente, dois usuários podem executar o mesmo relatório e obter resultados diferentes. Além disso, alguns relatórios contêm áreas ocultas que são reveladas com base nas credenciais do logon do usuário ou seleções feitas no próprio relatório. Áreas ocultas no relatório são excluídas de operações de pesquisa, produzindo resultados de pesquisa diferentes quando todas as partes do relatório estão visíveis.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
