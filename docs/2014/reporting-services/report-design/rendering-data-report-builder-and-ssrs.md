---
title: Renderizando dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a458fdf9-fb2a-4fee-9fbd-b38f36e91753
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 681fffa274b9ec8bf9f4e5d76e909325d1611d6b
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964062"
---
# <a name="rendering-data-report-builder-and-ssrs"></a>Renderizando dados (Construtor de Relatórios e SSRS)
  Quando você usa os renderizadores de layout, como HTML, MHTML, Word, Excel, PDF ou Image, os dados e suas organizações permanecem inalterados. Ao exportar usando um formato de renderizador de dados, como CSV (Comma-Separated Value) ou XML, nenhum elemento de layout visual é renderizado. O CSV e o XML aplicam determinadas regras ao relatório e seu conteúdo ao renderizar o relatório. Essas regras determinam como os dados são renderizados nesses formatos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Você pode usar os renderizadores de dados para:  
  
-   Importar para um banco de dados. O CSV é um formato comum que pode ser facilmente importado por muitos aplicativos de banco de dados, inclusive o SQL Server e o Microsoft Access.  
  
-   Importar para o Excel. Use o renderizador de CSV para exportar seus dados para o Excel sem o layout visual. Depois que os dados estiverem no Excel, você poderá usar as ferramentas padrão do Excel, como gráficos, fórmulas e tabelas dinâmicas.  
  
-   Transformações XSLT. Um XSLT pode ser se aplicado à saída do renderizador de XML. Essa transformação do lado do servidor é uma técnica poderosa para transformar seus dados virtuais em qualquer formato.  
  
-   Troca de dados/EDI. Um processo externo pode solicitar uma renderização CSV ou XML de um relatório e consumir seus dados.  
  
 Os formatos de renderização de dados são controlados por um conjunto de propriedades diferente dos renderizadores de layout. A seguir está uma lista de conjuntos de propriedades no painel **Propriedades** que só se aplica aos renderizadores de dados:  
  
-   A propriedade DataElementOutput controla se um determinado item estará ou não presente nos dados quando forem exportados.  
  
-   A propriedade DataElementName controla o nome do elemento de dados. No CSV, isso controla o nome do cabeçalho de coluna CSV. Em XML, isso se transforma no nome do elemento XML ou atributo para o item.  
  
-   A propriedade DataElementStyle controla, em XML, se o item de relatório será ou não renderizado como um elemento ou um atributo.  
  
 A opção de exportação CSV salva os dados do relatório como arquivos de texto delimitado por vírgula, sem qualquer formatação. Por padrão, o arquivo usa uma vírgula (,) para delimitar campos e linhas, mas essa configuração pode ser definida usando as Configurações de Informações de Dispositivo. O arquivo resultante pode ser aberto em um programa de planilhas como o Office SharePoint Server ou usado como formato de importação por outros programas. O arquivo .csv é aberto em um editor de textos, como Bloco de notas. Caso seja acessado como URL, o arquivo .csv retorna um tipo MIME de **text/csv**. Os arquivos são MIME versão 1.0. Para obter mais informações sobre como renderizar seu relatório no tipo de arquivo CSV, consulte [Exportando para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
 O arquivo XML com opção de exportação dos dados de relatório salva um relatório como arquivo XML. O esquema XML para o relatório é específico ao relatório. As informações sobre o layout do relatório não são salvas pela opção de exportação XML. O XML gerado usando essa opção pode ser importado para um banco de dados, usado como mensagem de dados XML ou enviado para um aplicativo personalizado. Para obter mais informações sobre como renderizar seu relatório no tipo de arquivo XML, consulte [Exportando para XML &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/exporting-to-xml-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Configurações de informações de dispositivo do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=102515)  
  
  
