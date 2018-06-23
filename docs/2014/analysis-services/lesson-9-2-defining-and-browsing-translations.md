---
title: Definindo e procurando traduções | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e60be99-3768-499c-a22c-a4ec37e61887
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 8dcee3e98c81f02c0a2fe54d54fc7eaa91a6a752
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007383"
---
# <a name="defining-and-browsing-translations"></a>Definindo e procurando traduções
  Uma tradução é uma representação dos nomes de objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em uma linguagem específica. Os objetos incluem grupos de medidas, medidas, dimensões, atributos, hierarquias, KPIs, ações e membros calculados. As traduções oferecem suporte de servidor a aplicativos cliente que podem oferecer suporte para vários idiomas. Como cliente, basta passar o identificador de localidade (LCID) para a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], que usa o LCID para determinar qual conjunto de traduções deverá ser usado quando ele fornecer metadados para os objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Se um objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não tiver uma tradução para o idioma ou para um objeto específico, o idioma padrão será usado para retornar o metadados do objeto ao cliente. Por exemplo, se um usuário empresarial na França acessar um cubo a partir de uma estação de trabalho que tenha uma configuração local francesa, esse usuário poderá visualizar as legendas de membro e os valores de propriedade de membro na França, caso haja uma tradução francesa. Entretanto, se um usuário empresarial na Alemanha acessar o mesmo cubo a partir de uma estação de trabalho que tenha uma configuração local alemã, esse usuário poderá visualizar os nomes de membro e os valores de propriedade de membro em alemão. Para obter mais informações, consulte [traduções da dimensão](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md), [traduções de cubo](multidimensional-models-olap-logical-cube-objects/cube-translations.md), [traduções &#40;Analysis Services&#41;](translations-analysis-services.md).  
  
 Nas tarefas deste tópico, você define as traduções de metadados para um conjunto limitado de objetos de dimensões na dimensão Data e objetos de cubo no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Em seguida, será possível navegar pelas dimensões e objetos de cubo para examinar as traduções de metadados.  
  
## <a name="specifying-translations-for-the-date-dimension-metadata"></a>Especificando traduções para os metadados de dimensão Data  
  
1.  Abra o Designer de Dimensão na dimensão **Data** e clique na guia **Traduções** .  
  
     Os metadados no idioma padrão de cada objeto de dimensão aparecem. O idioma padrão no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é o inglês.  
  
2.  Na barra de ferramentas da guia **Traduções** , clique no botão **Nova Tradução** .  
  
     Uma lista de idiomas é exibida na caixa de diálogo **Selecionar Idioma** .  
  
3.  Clique em **Espanhol (Espanha)** e em **OK**.  
  
     Uma nova coluna será exibida na qual você poderá definir traduções espanholas para os objetos do metadados que deseja traduzir. Neste tutorial, traduziremos apenas alguns objetos para ilustrar o processo.  
  
4.  Na barra de ferramentas da guia **Traduções** , clique no botão **Nova Tradução** , clique em **Francês (França)** na caixa de diálogo **Selecionar Idioma** e clique em **OK**.  
  
     Outra coluna de idioma será exibida e nela você poderá definir as traduções francesas.  
  
5.  Na linha para o **legenda** de objeto para o **data** dimensão, digite `Fecha` no **Espanhol (Espanha)** coluna de tradução e `Temps` no  **Francês (França)** coluna de tradução.  
  
6.  Na linha para o **legenda** de objeto para o **nome do mês** atributo, digite `Mes del Año` no **Espanhol (Espanha)** coluna de tradução e `Mois d'Année` no **Francês (França)** coluna de tradução.  
  
     Observe que, quando você insere essas traduções, um sinal de reticências (**…**) é exibido. Ao clicar nas reticências, você pode especificar uma coluna na tabela subjacente que fornece as traduções para cada membro da hierarquia do atributo.  
  
7.  Clique nas reticências (**…**) para obter a tradução no idioma **Espanhol (Espanha)** do atributo **Nome do Mês** .  
  
     A caixa de diálogo **Tradução de Dados de Atributo** é exibida.  
  
8.  Na lista **Colunas de tradução** , selecione **SpanishMonthName**, conforme mostrado na imagem a seguir.  
  
     ![Caixa de diálogo de conversão de dados do atributo](../../2014/tutorials/media/l9-translations-4.gif "caixa de diálogo tradução de dados de atributo")  
  
9. Clique em **OK**e clique nas reticências (**…**) para obter a tradução no idioma **Francês (França)** do atributo **Nome do Mês** .  
  
10. Na lista **Colunas de tradução** , selecione **FrenchMonthName**e clique em **OK**.  
  
     As etapas neste procedimento ilustram o processo de definição das traduções de metadados para objetos de dimensão e membros.  
  
## <a name="specifying-translations-for-the-analysis-services-tutorial-cube-metadata"></a>Especificando traduções para o metadados de cubo do Tutorial do Analysis Services  
  
1.  Alterne para o Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e mude para a guia **Traduções** .  
  
     O metadados no idioma padrão de cada objeto de cubo é exibido, como mostra a imagem a seguir. O idioma padrão no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é o inglês.  
  
     ![Na guia traduções do idioma padrão](../../2014/tutorials/media/l9-translations-5.gif "na guia traduções do idioma padrão")  
  
2.  Na barra de ferramentas da guia **Traduções** , clique no botão **Nova Tradução** .  
  
     Uma lista de idiomas é exibida na caixa de diálogo **Selecionar Idioma**.  
  
3.  Selecione **Espanhol (Espanha)** e clique em **OK**.  
  
     Uma nova coluna será exibida na qual você poderá definir traduções espanholas para os objetos do metadados que deseja traduzir. Neste tutorial, traduziremos apenas alguns objetos para ilustrar o processo.  
  
4.  Na barra de ferramentas da guia **Traduções** , clique no botão **Nova Tradução** , selecione **Francês (França)** na caixa de diálogo **Selecionar Idioma** e clique em **OK**.  
  
     Outra coluna de idioma será exibida e nela você poderá definir as traduções francesas.  
  
5.  Na linha para o **legenda** de objeto para o **data** dimensão, digite `Fecha` no **Espanhol (Espanha)** coluna de tradução e `Temps` no  **Francês (França)** coluna de tradução.  
  
6.  Na linha para o **legenda** de objeto para o **vendas pela Internet** grupo de medidas, digite `Ventas del lnternet` no **Espanhol (Espanha)** coluna de tradução e `Ventes D'Internet` no o **francês (França)** coluna de tradução.  
  
7.  Na linha para o **legenda** objeto para a medida quantidade de vendas pela Internet, tipo `Cantidad de las Ventas del Internet` no **Espanhol (Espanha)** coluna de tradução e `Quantité de Ventes d'Internet` no **francês ( França)** coluna de tradução.  
  
     As etapas neste procedimento ilustram o processo de definição das traduções de metadados para objetos de cubo.  
  
## <a name="browsing-the-cube-by-using-translations"></a>Navegando pelo cubo usando as traduções  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, mude para a guia **Navegador** e clique em **Reconectar**.  
  
3.  Remova todas as hierarquias e medidas do painel **Dados** e selecione Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] na lista **Perspectivas** .  
  
4.  No painel de metadados, expanda **Medidas** e **Vendas pela Internet**.  
  
     Observe que a medida **Vendas pela Internet/Valor das Vendas** é exibida em inglês (Internet Sales-Sales Amount) neste grupo de medidas.  
  
5.  Na barra de ferramentas, selecione **Espanhol (Espanha)** na lista **Idioma** .  
  
     Observe que os itens no painel de metadados são preenchidos novamente. Após o preenchimento dos itens, observe que a medida Quantidade de Vendas pela Internet não aparece mais na pasta de exibição Vendas pela Internet. Em vez disso, ele aparece em espanhol em uma nova pasta de exibição denominada `Ventas del lnternet`, conforme mostrado na imagem a seguir.  
  
     ![Painel de metadados Repopulated](../../2014/tutorials/media/l9-translations-6.gif "Repopulated painel de metadados")  
  
6.  No painel de metadados, clique com botão direito `Cantidad de las Ventas del Internet` e, em seguida, selecione **adicionar à consulta**.  
  
7.  No painel de metadados, expanda `Fecha`, expanda **Calendar Date**, clique com botão direito **Calendar Date**e, em seguida, selecione **adicionar ao filtro**.  
  
8.  No painel **Filtro** , selecione **CY 2007** como a expressão de filtro.  
  
9. No painel de metadados, clique com o botão direito do mouse em **Mes del Ano** e selecione **Adicionar à Consulta**.  
  
     Observe que os nomes de mês são exibidos em espanhol, como mostra a imagem a seguir.  
  
     ![Nomes de meses em espanhol no painel de dados](../../2014/tutorials/media/l9-translations-7.gif "nomes de meses em espanhol no painel de dados")  
  
10. Na barra de ferramentas, selecione **Francês (França)** na lista **Idioma** .  
  
     Observe que agora os nomes de mês e de medida são exibidos em francês.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 10: definindo funções administrativas](../analysis-services/lesson-10-defining-administrative-roles.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conversões de dimensão](multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Traduções de cubo](multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Traduções &#40;do Analysis Services&#41;](translations-analysis-services.md)  
  
  