---
title: Definindo uma relação referenciada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4a34ba52-e3b3-4e8a-8e55-73e0cd5a97bd
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f49d90e05c7d76129b5c2385ed1af05fc6e3731a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200376"
---
# <a name="defining-a-referenced-relationship"></a>Definindo uma relação referenciada
  Até este ponto no tutorial, cada dimensão de cubo que você definiu teve como base uma tabela que estava diretamente vinculada à tabela de fatos de um grupo de medidas por uma relação de chave primária para chave estrangeira. Nas tarefas deste tópico, você vinculará a dimensão **Geografia** à tabela de fatos para vendas do revendedor por meio da dimensão **Revendedor** , conhecida como *dimensão de referência*. Isso permite aos usuários dimensionar as vendas do revendedor por geografia. Para obter mais informações, consulte [Definir uma relação referenciada e as propriedades da relação referenciada](multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="dimensioning-reseller-sales-by-geography"></a>Dimensionando as vendas do revendedor por geografia  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Tutorial do Analysis Services** na pasta **Cubos** e clique em **Procurar**.  
  
2.  Remova todas as hierarquias do painel de dados e verifique se a medida **Vendas do Revendedor/Valor das Vendas** é exibida na área de dados do painel de dados. Adicione-a ao painel de dados caso ela ainda não esteja lá.  
  
3.  Na dimensão **Geografia** no painel de metadados, arraste a hierarquia definida pelo usuário **Geografias** até a área **Solte os Campos Linha Aqui** do painel de dados.  
  
     Observe que a medida **Vendas do Revendedor/Valor das Vendas** não foi dimensionada corretamente pelos membros do atributo **País/Região** na hierarquia **Regiões** . O valor de **Vendas do Revendedor/Valor das Vendas** é repetido para cada membro de atributo **País/Região** .  
  
     ![Dimensionadas medidas de vendas do revendedor](../../2014/tutorials/media/l5-referencedrelationship-1.gif "medida quantidade de vendas de revendedor dimensionadas")  
  
4.  Abra o Designer de Exibição da Fonte de Dados para a exibição da fonte de dados do **Adventure Works DW 2012**  
  
5.  No painel **Organizador de Diagramas** , exiba a relação entre a tabela **Geography** e a tabela **ResellerSales** .  
  
     Observe que não há nenhum vínculo direto entre essas tabelas. No entanto, existe um vínculo indireto entre elas pela tabela **Reseller** ou **SalesTerritory** .  
  
6.  Clique duas vezes na seta que representa a relação entre a tabela **Geography** e a tabela **Reseller** .  
  
     Na caixa de diálogo **Editar Relação** , observe que a coluna **GeographyKey** é a chave primária na tabela **Geography** e a chave estrangeira na tabela **Reseller** .  
  
7.  Clique em **Cancelar**, mude para o Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique na guia **Uso da Dimensão** .  
  
     Observe que, neste momento, a dimensão de cubo **Geography** não tem uma relação com os grupos de medidas **Vendas pela Internet** e **Vendas do Revendedor** .  
  
8.  Clique no botão Procurar (**…**) na célula **Nome Completo** , na interseção da dimensão **Customer** e do grupo de medidas **Vendas pela Internet** .  
  
     Na caixa de diálogo **Definir Relação** , observe que uma relação **Regular** está definida entre a tabela de dimensões **DimCustomer** e a tabela de grupos de medidas **FactInternetSales** com base na coluna **CustomerKey** de cada uma dessas tabelas. Todas as relações que você definiu dentro deste tutorial até este momento foram relações regulares.  
  
     A imagem a seguir mostra a caixa de diálogo **Definir Relação** com uma relação normal entre a tabela de dimensões **DimCustomer** e a tabela de grupos de medidas **FactInternetSales** .  
  
     ![Caixa de diálogo Definir relação](../../2014/tutorials/media/l5-referencedrelationship-4.gif "caixa de diálogo Definir relação")  
  
9. Clique em **Cancelar**.  
  
10. Clique no botão Procurar (**…**) na célula sem nome, na interseção da dimensão **Geografia** e do grupo de medidas **Vendas do Revendedor** .  
  
     Na caixa de diálogo **Definir Relação** , observe que não há relações definidas entre a dimensão de cubo Geografia e o grupo de medidas Vendas do Revendedor. Não é possível definir uma relação regular porque não há uma relação direta entre a tabela de dimensões da dimensão Geografia e a tabela de fatos do grupo de medidas Vendas do Revendedor.  
  
11. Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
     Uma relação referenciada é definida pela especificação de uma dimensão conectada diretamente à tabela de grupos de medidas, chamada *dimensão intermediária*, que pode ser usada pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para vincular a dimensão de referência à tabela de fatos. Em seguida, você especifica o atributo que vincula a dimensão de referência à dimensão intermediária.  
  
12. Na lista **Dimensão intermediária** , selecione **Revendedor**.  
  
     A tabela subjacente da dimensão Geografia é vinculada à tabela de fatos através da tabela subjacente da dimensão Revendedor.  
  
13. Na lista **Atributo de dimensão de referência** , selecione **Chave de Geografia**e tente selecionar **Chave de Geografia** na lista **Atributo de dimensão intermediária** .  
  
     Observe que **Chave de Geografia** não é exibido na lista **Atributo de dimensão intermediária** . Isso ocorre porque a coluna **GeographyKey** não está definida como um atributo na dimensão **Revendedor** .  
  
14. Clique em **Cancelar**.  
  
 Na próxima tarefa, você solucionará esse problema definindo um atributo que se baseia na coluna GeographyKey da dimensão Revendedor.  
  
## <a name="defining-the-intermediate-dimension-attribute-and-the-referenced-dimension-relationship"></a>Definindo o atributo de dimensão intermediária e a relação de dimensão referenciada  
  
1.  Abra o Designer de Dimensão na dimensão **Revendedor** e exiba as colunas da tabela **Revendedor** no painel **Exibição da Fonte de Dados** . Em seguida, exiba os atributos definidos na dimensão **Revendedor** no painel **Atributos** .  
  
     Observe que, embora a GeographyKey esteja definida como uma coluna na tabela Revendedor, nenhum atributo de dimensão está definido na dimensão Revendedor com base nessa coluna. A Geografia é definida como um atributo de dimensão na dimensão Geografia porque ela é a coluna principal que vincula a tabela subjacente daquela dimensão à tabela de fatos.  
  
2.  Para adicionar um atributo **Geografia Principal** à dimensão **Revendedor** , clique com o botão direito do mouse em **GeographyKey** no painel **Exibição da Fonte de Dados** e clique em **Novo Atributo da Coluna**.  
  
3.  No painel **Atributos** , selecione **Chave de Geografia**. Na janela Propriedades, defina a propriedade **AttributeHierarchyOptimizedState** como **NotOptimized**, a propriedade **AttributeHierarchyOrdered** como **False**e a propriedade **AttributeHierarchyVisible** como **False**.  
  
     O atributo Geografia Principal na dimensão Revendedor será usado apenas para vincular a dimensão Geografia à tabela de fatos Vendas do Revendedor. Como ele não será usado para pesquisa, não há valores ao definir essa hierarquia de atributo como visível. Além disso, ordenar e otimizar a hierarquia de atributo afetará negativamente o desempenho do processamento. Entretanto, o atributo deve estar habilitado para servir como vínculo entre as duas dimensões.  
  
4.  Mude para o Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , clique na guia **Uso da Dimensão** e clique no botão Procurar (**…**) na interseção do grupo de medidas **Vendas do Revendedor** e da dimensão de cubo **Geografia** .  
  
5.  Na lista **Selecionar tipo de relação** , selecione **Referenciada**.  
  
6.  Na lista **Dimensão intermediária** , selecione **Revendedor**.  
  
7.  Na lista **Atributo de dimensão de referência** , selecione **Geografia Principal**e selecione **Geografia Principal** na lista **Atributo de dimensão intermediária** .  
  
     Observe se a caixa de seleção **Materializar** está marcada. Esta é a configuração padrão para as dimensões MOLAP. A materialização do atributo de dimensão faz com que o valor do vínculo entre a tabela de fatos e a dimensão de referência de cada linha seja materializado, ou armazenado, na estrutura MOLAP da dimensão durante o processamento. Isso terá um efeito secundário no desempenho do processamento e nos requisitos de armazenamento, mas aumentará o desempenho da consulta (algumas vezes de maneira bastante significativa).  
  
8.  Clique em **OK**.  
  
     Observe que agora a dimensão de cubo **Geografia** está vinculada ao grupo de medidas **Vendas do Revendedor** . O ícone indica que a relação é uma relação de dimensão referenciada.  
  
9. Na lista **Dimensões** da guia **Uso da Dimensão** , clique com o botão direito do mouse em **Geografia**e clique em **Renomear**.  
  
10. Altere o nome desta dimensão de cubo para `Reseller Geography`.  
  
     Como agora essa dimensão de cubo está vinculada ao grupo de medidas **Vendas do Revendedor** , os usuários poderão definir seu uso explicitamente no cubo, evitando uma possível confusão do usuário.  
  
## <a name="successfully-dimensioning-reseller-sales-by-geography"></a>Dimensionamento bem-sucedido das vendas do revendedor por geografia  
  
1.  No menu **Compilar** , clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **Navegador** do Designer do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique no botão **Reconectar** .  
  
3.  No painel de metadados, expanda `Reseller Geography`, clique com botão direito **geografias**e, em seguida, clique em **adicionar à área de linha**.  
  
     Observe que agora a medida **Vendas do Revendedor/Valor das Vendas** foi dimensionada corretamente pelo atributo **País/Região** da hierarquia definida pelo usuário **Geografias** , como mostra a imagem a seguir.  
  
     ![Caixa de diálogo Definir relação](../../2014/tutorials/media/l5-referencedrelationship-5.gif "caixa de diálogo Definir relação")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Definindo uma relação de fatos](../analysis-services/lesson-5-2-defining-a-fact-relationship.md)  
  
## <a name="see-also"></a>Consulte também  
 [Relações de atributo](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)   
 [Definir uma relação referenciada e propriedades de relação referenciada](multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md)  
  
  
