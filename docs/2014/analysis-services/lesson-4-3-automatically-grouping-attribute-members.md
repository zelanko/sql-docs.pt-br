---
title: Agrupando automaticamente membros de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9fb2cda3-a122-4a4c-82e0-3454865eef04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 568cb46a17ac29cabe45b79212400fd020be84c3
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888408"
---
# <a name="automatically-grouping-attribute-members"></a>Agrupando membros de atributo automaticamente
  Ao navegar em um cubo, você normalmente dimensiona os membros de uma hierarquia de atributo pelos membros de outra hierarquia de atributo. Por exemplo, você pode agrupar as vendas de cliente por cidade, produto comprado ou sexo. Porém, com determinados tipos de atributo, é útil usar o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para criar automaticamente agrupamentos de membros de atributo com base na distribuição dos membros dentro de uma hierarquia de atributo. Por exemplo, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode criar grupos de valores de renda anual para clientes. Ao fazer isso, os usuários que navegarem pela hierarquia de atributo verão o nome e os valores dos grupos em vez dos próprios membros. Isso limita o número de níveis que são apresentados aos usuários, o que pode ser mais útil para a análise.  
  
 A propriedade **DiscretizationMethod** determina se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria agrupamentos e determina o tipo de agrupamento feito. Por padrão, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não faz nenhum agrupamento. Ao habilitar agrupamentos automáticos, você pode permitir que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determine automaticamente o melhor método de agrupamento com base na estrutura do atributo ou ainda escolher um dos algoritmos de agrupamento da lista a seguir para especificar o método de agrupamento:  
  
 **EqualAreas**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria intervalos de grupo de forma que a população total de membros da dimensão seja distribuída igualmente pelos grupos.  
  
 **Clusters**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria grupos executando clustering unidimensional nos valores de entrada usando o método de clustering K-means com distribuições gaussianas. Essa opção só é válida para colunas numéricas.  
  
 Depois de especificar um método de agrupamento, você deve especificar o número de grupos usando a propriedade **DiscretizationBucketCount** . Para obter mais informações, consulte [Agrupar membros de atributo &#40;Discretização&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
 Nas tarefas deste tópico, você habilitará tipos diferentes de agrupamentos para valores de renda anual na dimensão **Cliente** ; número de horas de dispensa médica dos funcionários na dimensão **Funcionários** ; e o número de horas de férias dos funcionários na dimensão **Funcionários** . Depois, você processará e navegará no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para exibir o efeito dos grupos de membros. Finalmente, você modificará as propriedades do grupo de membros para ver o efeito da alteração no tipo de agrupamento.  
  
## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>Agrupando membros da hierarquia de atributo na dimensão Cliente  
  
1.  No Gerenciador de Soluções, clique duas vezes em **Cliente** na pasta **Dimensões** para abrir o Designer de Dimensão da dimensão Customer.  
  
2.  No painel **Exibição da Fonte de Dados** , clique com o botão direito do mouse na tabela **Cliente** e clique em **Explorar Dados**.  
  
     Observe o intervalo de valores da coluna **YearlyIncome** . Esses valores se tornam os membros da hierarquia de atributo **Renda Anual** , a menos que você habilite o agrupamento de membros.  
  
3.  Feche a guia **Explorar Tabela Cliente** .  
  
4.  No painel **Atributos** , selecione **Renda Anual**.  
  
5.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para **Automatic** e altere o valor para a propriedade **DiscretizationBucketCount** para `5`.  
  
     A imagem a seguir mostra as propriedades modificadas para **Renda Anual**.  
  
     ![Propriedades modificadas para renda anual](../../2014/tutorials/media/l4-discretizationmethod-1.gif "Propriedades modificadas para renda anual")  
  
## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>Agrupando membros da hierarquia de atributo na dimensão Funcionário  
  
1.  Alterne para o Designer de Dimensão da dimensão Funcionário.  
  
2.  No painel **Exibição da Fonte de Dados** , clique com o botão direito do mouse na tabela **Funcionário** e clique em **Explorar Dados**.  
  
     Observe os valores das colunas **SickLeaveHours** e **VacationHours** .  
  
3.  Feche a guia **Explorar Tabela Funcionário** .  
  
4.  No painel **Atributos** , selecione **Horas de Dispensa Médica**.  
  
5.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para clusters e altere o valor para a propriedade **DiscretizationBucketCount** para `5`.  
  
6.  No painel **Atributos** , selecione **Horas de Férias**.  
  
7.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para **áreas iguais** e altere o valor para a propriedade **DiscretizationBucketCount** para `5`.  
  
## <a name="browsing-the-modified-attribute-hierarchies"></a>Navegando nas hierarquias de atributo modificadas  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
2.  Quando a implantação finalizar com êxito, alterne para o Designer de Cubo do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e, em seguida, clique em **Reconectar** na guia **Navegador** .  
  
3.  Clique no ícone do Excel e clique em **Habilitar**.  
  
4.  Arraste a medida **Vendas pela Internet/Valor das Vendas** até a área Valores da Lista de Campos da Tabela Dinâmica.  
  
5.  Na lista de campos, expanda a dimensão **Produto** e arraste a hierarquia de usuário **Linhas de Modelo do Produto** para a área **Rótulos de Linhas** da lista de campos.  
  
6.  Expanda a dimensão **Cliente** na lista de campos, expanda a pasta de exibição **Demográfico** e, em seguida, arraste a hierarquia de atributo **Renda Anual** para a área **Rótulos de Coluna** .  
  
     Agora, os membros da hierarquia de atributo **Renda Anual** estão agrupados em seis buckets, incluindo um bucket de vendas para clientes cuja renda anual é desconhecida. Nem todos os buckets são exibidos.  
  
7.  Remova a hierarquia de atributo **Renda Anual** da área de colunas e a medida **Vendas pela Internet/Valor das Vendas** da área **Valores** .  
  
8.  Adicione a medida **Vendas do Revendedor/Valor das Vendas** à área de dados.  
  
9. Na lista de campos, expanda a dimensão **Funcionário** , expanda **Organização**e, em seguida, arraste **Horas de Dispensa Médica** para **Rótulos de Coluna**.  
  
     Observe que todas as vendas são feitas por funcionários dentro de um dos dois grupos. Observe também que os funcionários com 32 a 42 horas de dispensa médica fizeram um número significativamente maior de compras que os funcionários com 20 a 31 horas de dispensa médica.  
  
     A imagem a seguir mostra as vendas dimensionadas pelas horas de dispensa médica dos funcionários:  
  
     ![Vendas dimensionadas por horas de licença de doença do funcionário](../../2014/tutorials/media/l4-discretizationmethod-2.gif "Vendas dimensionadas por horas de licença de doença do funcionário")  
  
10. Remova a hierarquia **Horas de Dispensa Médica** da área de coluna do painel **Dados** .  
  
11. Adicione **Horas de Férias** à área de coluna do painel **Dados** .  
  
     Observe que dois grupos são exibidos com base no método de agrupamento de áreas iguais. Os outros três outros grupos são ocultados, pois não contêm nenhum valor de dados.  
  
## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>Modificando as propriedades de agrupamento e revisando o efeito das alterações  
  
1.  Alterne para o Designer de Dimensão da dimensão **Funcionário** e depois selecione **Horas de Férias** no painel **Atributos** .  
  
2.  Na janela Propriedades, altere o valor da propriedade **DiscretizationBucketCount** para **10.**  
  
3.  No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **Implantar Tutorial do Analysis Services**.  
  
4.  Quando a implantação for finalizada com êxito, volte para o Designer de Cubo do cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
5.  Clique em **Reconectar** na guia **Navegador** , clique no ícone do Excel e, em seguida, reconstrua a Tabela Dinâmica para que você possa exibir o efeito da alteração do método de agrupamento:  
  
    1.  Arraste Vendas do Revendedor-Valor das Vendas para Valores  
  
    2.  Arraste Horas de Férias (na pasta Organização de Funcionários) para Colunas  
  
    3.  Arraste Linhas de Modelo de Produtos para Linhas  
  
     Observe que, agora, há três grupos de membros do atributo **Horas de Férias** que contêm valores de vendas para produtos. (Os outros sete grupos contêm membros sem dados de vendas.)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Ocultando e desabilitando as hierarquias de atributo](https://docs.microsoft.com/analysis-services/lesson-4-4-hiding-and-disabling-attribute-hierarchies)  
  
## <a name="see-also"></a>Consulte também  
 [Agrupar membros de atributo &#40;Discretização&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
  
