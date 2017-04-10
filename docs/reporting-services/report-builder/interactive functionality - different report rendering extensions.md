---
title: "Funcionalidade interativa para extens&#245;es de renderiza&#231;&#227;o de relat&#243;rio diferentes (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Funcionalidade interativa para extens&#245;es de renderiza&#231;&#227;o de relat&#243;rio diferentes (Construtor de Relat&#243;rios e SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece recursos para interagir com um relatório paginado no tempo de execução. Nem todos os formatos de renderização de relatório dão suporte a uma gama completa de recursos interativos. Use a tabela a seguir para entender como cada recurso interativo funciona em formatos específicos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Recursos interativos em formatos de saída diferentes  
 Os relatórios paginados que são renderizados para XML, CSV ou formatos de imagem não dão suporte aos recursos interativos.  
  
 Os relatórios que você pode exibir portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], no Web Parts do SharePoint ou em um navegador são renderizados em HTML. O HTML e os Formulários do Windows são os únicos formatos de saída de relatório que dão suporte total a todos os recursos interativos. Os formatos alternativos do HTML (como o MHTML) dão suporte a vários recursos interativos. Se existirem exceções para o MHTML, elas serão indicadas na tabela a seguir.  
  
### Mapas do documento  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|O mapa interativo do documento oferece um painel de navegação dos links hierárquicos que são utilizados para navegar para seções diferentes do relatório.|  
|PDF|O PDF renderiza o mapa do documento como painel de Indicações. Todos os itens no mapa do documento são listados um após o outro no painel. Inclui uma hierarquia de links. Se um intervalo de página for especificado, só essas indicações que estão renderizadas existem na hierarquia.|  
|Excel|O Excel renderiza um mapa do documento como a primeira planilha na pasta. Inclui uma hierarquia de links. Quando no link no mapa do documento é clicado, a célula de destino na respectiva planilha é aberta.|  
|Word|O Word renderiza o mapa do documento como rótulos do Sumário.|  
|Outra (por exemplo, TIFF, XML e CSV)|Não disponível em MHTML, XML, CSV ou Imagem.|  
  
### Links de detalhamento para outros relatórios  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Os usuários clicam nos valores de dados no relatório para exibir os dados relacionados em outro relatório.|  
|PDF|Links de detalhamento não estão disponíveis em PDF. Considere o uso de hiperlinks para relatórios em PDF vinculados a outras páginas.|  
|Excel|Os links de detalhamento são renderizados em Excel.<br /><br /> O link se torna um hiperlink que aponta ao relatório referenciado pelo link de detalhamento. Clicando no vínculo abre um relatório em uma janela do navegador.|  
|Word|Os links de detalhamento são renderizados em Word.<br /><br /> O link se torna um hiperlink que aponta ao relatório referenciado pelo link de detalhamento. Clicando no vínculo abre um relatório em uma janela do navegador.|  
|Outro|Não disponível em XML, CSV ou Imagem.|  
  
### Alterne os itens dentro de um relatório  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Os usuários clicam nos ícones de expansão e recolhimento para exibir as seções de um relatório.|  
|PDF|O servidor de relatórios exporta o estado atual de exibição ou ocultação do relatório para o PDF. A alternância interativa não tem suporte|  
|Excel|Os links de detalhamento que podem ser alternados são renderizados como estruturas recolhíveis no Excel. Você pode expandir e pode recolher as seções do relatório no Excel. Para obter mais informações sobre as limitações impostas pelo Excel, consulte [Exportar para Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).|  
|Word|O servidor de relatórios exporta o estado atual de exibição ou ocultação do relatório para o PDF. A alternância interativa não tem suporte|  
|Outro|Não disponível em MHTML, XML, ou CSV. Ao exportar para um formato Imagem, o servidor de relatórios exporta o estado de exibição ou ocultação do relatório para o PDF. Não há suporte para a alternância interativa.|  
  
### Classificação interativa  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Para relatórios tabulares, os usuários clicam nas setas de classificação na coluna para alterar o modo como os dados estão classificados.|  
|PDF|Não disponível em PDF.|  
|Excel|Não disponível em Excel.|  
|Word|Não disponível em Word.|  
|Outro|Não disponível em MHTML, XML, CSV ou Imagem.|  
  
### Hiperlinks para conteúdo de Web externo ou imagens  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Os usuários clicam em links para abrir páginas da Web externas em uma nova janela do navegador.|  
|PDF|Os hiperlinks são renderizados pela extensão de renderização do PDF. Quando um usuário clicar em um hiperlink, as páginas vinculadas são abertas no navegador.|  
|Excel|Os hiperlinks são renderizados em Excel.|  
|Word|Os hiperlinks são renderizados em Word.|  
|Outro|Hiperlinks não estão disponíveis em MHTML, XML, CSV ou Imagem.<br /><br /> Para MHTML e Imagem, as imagens externas são renderizadas como quadro estático.|  
  
### Indicação ou âncora  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Os usuários clicam em links para navegar para outra seção do mesmo relatório.|  
|PDF|Não disponível em PDF.|  
|Excel|As indicações são renderizadas em Excel.<br /><br /> A indicação se torna um hiperlink apontando para o nome do item do relatório.|  
|Word|Indicações são renderizadas em Word.<br /><br /> Uma indicação se torna um hiperlink que aponta para o item de relatório indicado. Apenas 40 caracteres do nome de uma indicação ou âncora são convertidos quando o relatório é exportado o que pode levar à duplicidade dos nomes da indicação ou da âncora. Os espaços são convertidos em sublinhados (_).|  
|Outro|Não disponível em XML, CSV ou Imagem.|  
  
### Parâmetros solicitados obtidos em tempo de execução  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Uma área de entrada de parâmetro aparece no topo do relatório. Esta área faz parte do Visualizador de HTML usado para exibir relatórios em um navegador.|  
|PDF|O servidor de relatórios exporta o relatório para PDF usando os valores dos parâmetros atualmente em vigor para o relatório.|  
|Excel|O servidor de relatórios exporta o relatório para Excel usando os valores dos parâmetros atualmente em vigor para o relatório.|  
|Word|O servidor de relatórios exporta o relatório para Word usando os valores dos parâmetros atualmente em vigor para o relatório.|  
|Outro|O servidor de relatório exporta o relatório para outros formatos usando os valores dos parâmetros atualmente em vigor para o relatório.|  
  
### Filtros aplicados em tempo de execução  
  
|Opção de exportação|Informações de suporte|  
|-------------------|-------------------------|  
|Visualização/Visualizador de Relatórios, HTML|Os dados filtrados são exibidos ao usuário em tempo de execução.|  
|PDF|O servidor de relatórios exporta o relatório para o PDF usando dados filtrados no relatório atual.|  
|Excel|O servidor de relatórios exporta o relatório para o Excel usando dados filtrados no relatório atual.|  
|Word|O servidor de relatórios exporta o relatório para o Word usando dados filtrados no relatório atual.|  
|Outro|O servidor de relatórios exporta o relatório para outros formatos usando dados filtrados no relatório atual.|  
  
## Consulte também  
 [Exportar relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Matrices%20\(Report%20Builder%20and%20SSRS\).md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  