---
title: Definindo conjuntos nomeados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 47254fd3-525f-4c35-b93d-316607652517
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff1b386d0f85f1073b533921d690462c9ed25dc0
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69493891"
---
# <a name="defining-named-sets"></a>Definindo conjuntos nomeados
  Um conjunto nomeado é uma linguagem MDX (Multidimensional Expressions) que retorna um conjunto de membros de dimensão. Os conjuntos nomeados podem ser definidos e salvos como parte da definição de cubo; você também pode criar conjuntos nomeados em aplicativos cliente. Você cria conjuntos nomeados combinando dados de cubo, operadores aritméticos, números e funções. Os conjuntos nomeados podem ser usados por usuários em consultas MDX em aplicativos cliente e também podem ser usados para definir conjuntos em subcubos. Um subcubo é uma coleção de conjuntos de crossjoined que restringe o espaço do cubo para o subespaço definido para instruções subsequentes. Definir um espaço de cubo restrito é um conceito fundamental para o script MDX.  
  
 Os conjuntos nomeados simplificam as consultas MDX e fornecem aliases úteis para expressões complexas, normalmente usadas, definidas. Por exemplo, você pode definir um conjunto nomeado chamado grandes revendedores que contém o conjunto de membros na dimensão Revendedor que têm a maioria dos funcionários. Os usuários finais podem usar os grandes revendedores nomeados conjunto em consultas, ou você pode usar o conjunto nomeado para definir um conjunto em um subcubo. As definições de conjunto nomeado são armazenadas em cubos, mas seus valores existem apenas na memória. Para criar um conjunto nomeado, use o comando **novo conjunto nomeado** na guia **cálculos** do designer de cubo. Para obter mais informações, consulte [cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md), [criar conjuntos nomeados](multidimensional-models/create-named-sets.md).  
  
 Nas tarefas deste tópico, você definirá dois conjuntos nomeados: um conjunto nomeado de produtos principais e um conjunto nomeado de revendedores grandes.  
  
## <a name="defining-a-core-products-named-set"></a>Definindo um conjunto nomeado de produtos principais  
  
1.  Alterne para a guia **Cálculos** do Designer de Cubo para o cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique na guia **Exibição de Formulário** na barra de ferramentas.  
  
2.  Clique em **[taxa total de vendas para todos os produtos]** no painel **organizador de script** e clique em **novo conjunto nomeado** na barra de ferramentas da guia **cálculos** .  
  
     Ao definir um novo cálculo na guia **Cálculos** , lembre-se de que os cálculos são resolvidos na ordem em que eles aparecem no painel **Organizador de Script** . O foco definido dentro desse painel ao criar um novo cálculo determina a ordem de execução do cálculo; um novo cálculo é definido imediatamente após o cálculo no qual você definiu o foco.  
  
3.  Na caixa **nome** , altere o nome do novo conjunto nomeado para `[Core Products]`.  
  
     No painel **Organizador de Script** , observe o único ícone que diferencia a um conjunto nomeado de um comando de script ou um membro calculado.  
  
4.  Na guia **metadados** do painel **ferramentas de cálculo** , expanda **produto**, **categoria**, expanda `Members` e expanda **todos os produtos**.  
  
    > [!NOTE]  
    >  Se não for possível exibir nenhum metadado no painel **ferramentas de cálculo** , clique em **reconectar** na barra de ferramentas. Se isso não funcionar, talvez seja necessário processar o cubo ou iniciar a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
5.  Arraste **bicicletas** para a caixa **expressão** .  
  
     Agora você criou uma expressão de conjunto que retornará o conjunto de membros que estão na categoria de bicicleta na dimensão produto.  
  
## <a name="defining-a-large-resellers-named-set"></a>Definindo um conjunto nomeado chamado Grandes Revendedores  
  
1.  Clique com o botão direito do mouse em `[Core Products]` no painel **organizador de script** e clique em **novo conjunto nomeado**.  
  
2.  Na caixa **nome** , altere o nome desse conjunto nomeado para `[Large Resellers]`.  
  
3.  Na caixa **expressão** , digite `Exists()`.  
  
     Você usará a função Exists para retornar o conjunto de membros da hierarquia de atributo de nome do revendedor que faz interseção com o conjunto de membros na hierarquia de atributo número de funcionários que tem o maior número de funcionários.  
  
4.  Na guia **metadados** do painel **ferramentas de cálculo** , expanda a dimensão **revendedor** e, em seguida, expanda a hierarquia de atributo **nome do revendedor** .  
  
5.  Arraste o nível **nome do revendedor** até o parêntese para a expressão de conjunto Exists.  
  
     Você usará a função members para retornar todos os membros deste conjunto. Para obter mais informações, [consulte &#40;Members Set&#41; &#40;&#41;MDX](/sql/mdx/members-set-mdx).  
  
6.  Após a expressão de conjunto parcial, digite um ponto e, em seguida, adicione a função members. Sua expressão deve ser parecida com a seguinte:  
  
    ```  
    Exists([Reseller].[Reseller Name].[Reseller Name].Members)  
    ```  
  
     Agora que você definiu o primeiro conjunto para a expressão de conjunto Exists, você está pronto para adicionar o segundo conjunto – o conjunto de membros da dimensão Revendedor que contém o maior número de funcionários.  
  
7.  Na guia **metadados** do painel **ferramentas de cálculo** , expanda o **número de funcionários** na dimensão Revendedor, expanda `Members` e, em seguida, expanda **todos os revendedores**.  
  
     Observe que os membros dessa hierarquia de atributo não são agrupados.  
  
8.  Abra o designer de dimensão para a dimensão **revendedor** e clique em **número de funcionários** no painel **atributos** .  
  
9. No janela Propriedades, altere a propriedade `DiscretizationMethod` para **automático**e, em seguida, altere a propriedade `DiscretizationBucketCount` para `5`. Para obter mais informações, consulte [Group Attribute &#40;Members discretização&#41;](multidimensional-models/attribute-properties-group-attribute-members.md).  
  
10. No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **implantar Analysis Services tutorial**.  
  
11. Quando a implantação for concluída com êxito, alterne para o designer de cubo para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e, em seguida, clique em **reconectar** na barra de ferramentas da guia **cálculos** .  
  
12. Na guia **metadados** do painel **ferramentas de cálculo** , expanda o **número de funcionários** na dimensão **revendedor** , expanda `Members` e, em seguida, expanda **todos os revendedores**.  
  
     Observe que os membros dessa hierarquia de atributo agora estão contidos em cinco grupos, numerados de 0 a 4. Para exibir o número de um grupo, pause o ponteiro sobre esse grupo para exibir um InfoTip. Para o intervalo `2 -17`, o InfoTip deve conter `[Reseller].[Number of Employees].&[0]`.  
  
     Os membros desta hierarquia de atributo são agrupados porque a propriedade DiscretizationBucketCount está definida como `5` e a propriedade DiscretizationMethod está definida como **Automatic**.  
  
13. Na caixa **expressão** , adicione uma vírgula na expressão de conjunto Exists após a função members e antes do parêntese de fechamento e, em seguida, arraste **83-100** do painel **metadados** e posicione-o após a vírgula.  
  
     Agora você concluiu a expressão de conjunto Exists que retornará o conjunto de membros que interseccionam com esses dois conjuntos especificados, o conjunto de todos os revendedores e o conjunto de revendedores que têm 83 a 100 funcionários, quando o conjunto nomeado grandes revendedores é colocado em um eixo.  
  
     A imagem a seguir mostra o painel **expressões de cálculo** para o `[Large Resellers]` conjunto nomeado.  
  
     ![Painel de expressões de cálculo para [grandes revendedores]](../../2014/tutorials/media/l6-named-set-02.gif "Painel de expressões de cálculo para [grandes revendedores]")  
  
14. Na barra de ferramentas da guia **cálculos** , clique em **exibição de script**e examine os dois conjuntos nomeados que você acabou de adicionar ao script de cálculo.  
  
15. Adicione uma nova linha no script de cálculo imediatamente antes do primeiro comando CREATE SET e, em seguida, adicione o seguinte texto ao script em sua própria linha:  
  
    ```  
    /* named sets */  
    ```  
  
     Agora você definiu dois conjuntos nomeados, que são visíveis no painel **organizador de script** . Agora você está pronto para implantar esses conjuntos nomeados e, em seguida, procurar essas medidas no cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial.  
  
## <a name="browsing-the-cube-by-using-the-new-named-sets"></a>Navegando no cubo usando os novos conjuntos nomeados  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **implantar Analysis Services tutorial**.  
  
2.  Quando a implantação for concluída com êxito, clique na guia **navegador** e, em seguida, clique em **reconectar**.  
  
3.  Limpe a grade no painel dados.  
  
4.  Adicione a medida **vendas do revendedor/valor das vendas** à área de dados.  
  
5.  Expanda a dimensão Produto e adicione Categoria e Subcategoria à área de linha, conforme mostrado na imagem a seguir.  
  
     ![Membros do atributo subcategoria](../../2014/tutorials/media/l6-named-set-03.gif "Membros do atributo subcategoria")  
  
6.  No painel **metadados** , na dimensão **produto** , arraste **produtos principais** para a área de filtro.  
  
     Observe que apenas o membro de **bicicleta** do atributo **Category** e os membros das subcategorias de **bicicletas** permanecem no cubo. Isso ocorre porque o conjunto nomeado de **produtos principais** é usado para definir um subcubo. Esse subcubo limita os membros do atributo **Category** na dimensão **Product** dentro do subcubo para os membros do **produto principal** chamado set, conforme mostrado na imagem a seguir.  
  
     ![Membros do conjunto nomeado do produto principal](../../2014/tutorials/media/l6-named-set-04.gif "Membros do conjunto nomeado do produto principal")  
  
7.  No painel de **metadados** , expanda **revendedor**, adicione **grandes revendedores** à área de filtro.  
  
     Observe que a medida valor das vendas do revendedor no painel dados exibe apenas valores de vendas para grandes revendedores de bicicletas. Observe também que o painel de filtro agora exibe os dois conjuntos nomeados que são usados para definir esse subcubo específico, conforme mostrado na imagem a seguir.  
  
     ![Painel de filtro contendo dois conjuntos nomeados](../../2014/tutorials/media/l6-named-set-05.gif "Painel de filtro contendo dois conjuntos nomeados")  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa na lição  
 [Lição 7: definindo KPIs indicadores &#40;chave de desempenho&#41;](lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>Consulte também  
 @No__t_1 de [cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md)  
 [Criar conjuntos nomeados](multidimensional-models/create-named-sets.md)  
  
  
