---
title: Adicionar um hiperlink a uma URL (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 80fb8d9b4f416933e19931aeb29fdb33f533e9f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Adicionar um hiperlink a uma URL (Construtor de Relatórios e SSRS)
Saiba como adicionar ações de hiperlink a caixas de texto, imagens, gráficos e medidores nos relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  . Links podem ir para outros relatórios, indicadores em um relatório ou URLs estáticas ou dinâmicas. 

 Você pode adicionar uma ação de hiperlink a um item que tem uma propriedade **Action** , por exemplo, uma caixa de texto, imagem ou série calculada em um gráfico. Quando o usuário clicar nesse item de relatório, ocorrerá a ação definida.  
  
*   Você pode **adicionar um hiperlink que abrirá um navegador com uma URL** especificada. O hiperlink pode ser uma URL estática ou uma expressão avaliada como uma URL. Se você tiver um campo em um banco de dados que contenha URLs, a expressão poderá conter esse campo, resultando em uma lista dinâmica de hiperlinks no relatório. Verifique se os leitores do relatório têm acesso à URL fornecida.  
   
*  Você também pode **especificar URLs para criar detalhamentos** em relatórios em qualquer servidor de relatório ao qual você e os usuários tenham permissão para exibir usando solicitações de URL para o servidor de relatório. Por exemplo, você pode especificar um relatório e ocultar o mapa do documento para o usuário quando ele exibir o relatório pela primeira vez. Para obter mais informações, consulte [Acesso à URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) e [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).
 
 *  Além disso, você pode **adicionar um indicador a um local específico** no mesmo relatório. 
  
Tente adicionar hiperlinks com os dados de exemplo no [Tutorial: Formatar texto &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  Links associados a campos de conjuntos de dados podem ser vulneráveis à violação para fins mal-intencionados. Para obter mais informações, consulte [Proteger relatórios e recursos](../../reporting-services/security/secure-reports-and-resources.md).  
  
## <a name="to-add-a-hyperlink-and"></a>Para adicionar um hiperlink e...   
  
1.  No modo de exibição de Design de relatório, clique com o botão direito do mouse na caixa de texto, na imagem ou no gráfico a que você deseja adicionar um link e, em seguida, clique em **Propriedades**.  
  
2.  Na caixa de diálogo Propriedades, clique na guia **Ação** . Continue lendo para obter informações sobre as opções.  

## <a name="-add-drillthrough-to-another-report"></a>... adicionar detalhamento a outro relatório

1. Na guia **Ação** , selecione **Ir para o relatório**. 

2. Especifique o relatório de destino e os parâmetros que você deseja usar. Os nomes de parâmetro devem corresponder aos parâmetros definidos para o relatório de destino. 

3. Use os botões **Adicionar** e **Excluir** para adicionar ou remover parâmetros e as setas para cima e para baixo para ordenar a lista de parâmetros.

4.  Digite ou selecione um **Valor** a ser passado para o parâmetro nomeado no relatório de detalhamento. Clique no botão Expressão (fx) para editar a expressão.

5. Selecione **Omitir** para impedir que o parâmetro seja executado. Por padrão, esta caixa de seleção é desmarcada e não ativa. Para marcar a caixa de seleção, clique no botão Expressão (fx) e digite True ou crie uma expressão. A caixa de seleção é marcada quando você clica em **OK** na caixa de diálogo Expressão.
  
   Consulte [Adicionar uma ação de detalhamento em um relatório](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) para obter mais informações. 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>... adicionar um indicador

É possível criar link para indicadores em um local do relatório atual. Para criar um link para um indicador, primeiro é necessário definir a propriedade **Bookmark** de um item de relatório. Para definir a propriedade **Bookmark** , selecione um item de relatório e, no painel Propriedades, digite um valor ou uma expressão para a ID do indicador. Por exemplo, SalesChart ou 5TopSales.

1. Na guia **Ação** , selecione **Ir para o indicador**. 

2. Digite ou selecione a ID de indicador para a qual o relatório deverá pular. Clique no botão Expressão (fx) para alterar a expressão. 

   A ID de indicador pode ser uma ID estática ou uma expressão que seja avaliada por uma ID de indicador. A expressão pode incluir um campo que contenha uma ID de indicador.
   
   Consulte [Adicionar um indicador a um relatório](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) para obter mais informações.
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>... adicionar um hiperlink 
  
1. Na guia **Ação** , selecione **Ir para URL**. Aparecerá uma seção adicional na caixa de diálogo para essa opção.  
  
4.  Em **Selecionar URL**, digite ou selecione uma URL ou uma expressão avaliada como uma URL, ou clique na seta suspensa e no nome de um campo que contenha uma URL. 

    Para um item publicado em um servidor de relatórios configurado para o modo nativo, use um caminho completo ou relativo. Por exemplo, `http://<servername>/images/image1.jpg`. 
    
    Para um item publicado em um servidor de relatórios configurado para o modo integrado do SharePoint, use uma URL completamente qualificada. Por exemplo, `http://<SharePointservername>/<site>/Documents/images/image1.jpg`.
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>Depois de adicionar um hiperlink
  
1.  (Opcional) O texto não é formatado automaticamente como um link. Para textos, é recomendável alterar sua cor e seu efeito para indicar que ele é um link. Por exemplo, altere a cor para azul e o efeito para sublinhado na seção **Fonte** da guia Página Inicial da Faixa de Opções.  
  
7.  Para testar o link, clique em **Executar** para visualizar o relatório e, em seguida, no item de relatório no qual você definiu esse link.  
  
## <a name="see-also"></a>Consulte Também  
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Criar um mapa de documentos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
