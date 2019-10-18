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
ms.openlocfilehash: 6dc768188f25640a3685c8526bfceb3874154f40
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "69890831"
---
# <a name="automatically-grouping-attribute-members"></a>Agrupando membros de atributo automaticamente
  Ao procurar um cubo, normalmente você dimensiona os membros de uma hierarquia de atributo pelos membros de outra hierarquia de atributo. Por exemplo, você pode agrupar as vendas do cliente por cidade, por produto adquirido ou por sexo. No entanto, com determinados tipos de atributos, é útil ter [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] criar automaticamente agrupamentos de membros de atributo com base na distribuição dos membros dentro de uma hierarquia de atributo. Por exemplo, você pode ter [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] criar grupos de valores de renda anuais para os clientes. Quando você fizer isso, os usuários que navegam na hierarquia de atributo verão os nomes e valores dos grupos em vez dos próprios membros. Isso limita o número de níveis que são apresentados aos usuários, o que pode ser mais útil para análise.  
  
 A propriedade **DiscretizationMethod** determina se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria agrupamentos e determina o tipo de agrupamento que é executado. Por padrão, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não executa agrupamentos. Ao habilitar agrupamentos automáticos, você pode permitir que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determine automaticamente o melhor método de agrupamento com base na estrutura do atributo ou pode escolher um dos algoritmos de agrupamento na lista a seguir para especificar o método de agrupamento:  
  
 **EqualAreas**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria intervalos de grupo para que a população total de membros de dimensão seja distribuída igualmente entre os grupos.  
  
 **Clusters**  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cria grupos executando clustering unidimensional nos valores de entrada usando o método de clustering K-means com distribuições gaussianas. Essa opção só é válida para colunas numéricas.  
  
 Depois de especificar um método de agrupamento, você deve especificar o número de grupos, usando a propriedade **DiscretizationBucketCount** . Para obter mais informações, consulte [Agrupar membros &#40;de&#41; atributo discretização](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
 Nas tarefas deste tópico, você habilitará diferentes tipos de agrupamentos para o seguinte: os valores de renda anual na dimensão **cliente** ; o número de horas de licença de doença do funcionário na dimensão **funcionários** ; e o número de horas de férias do funcionário na dimensão **funcionários** . Em seguida, você processará e procurará o cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial para exibir o efeito dos grupos de membros. Por fim, você modificará as propriedades do grupo de membros para ver o efeito da alteração no tipo de agrupamento.  
  
## <a name="grouping-attribute-hierarchy-members-in-the-customer-dimension"></a>Agrupando membros de hierarquia de atributo na dimensão cliente  
  
1.  Em Gerenciador de Soluções, clique duas vezes em **cliente** na pasta **dimensões** para abrir o designer de dimensão para a dimensão cliente.  
  
2.  No painel **exibição da fonte de dados** , clique com o botão direito do mouse na tabela **cliente** e clique em **explorar dados**.  
  
     Observe o intervalo de valores para a coluna **YearlyIncome** . Esses valores se tornam os membros da hierarquia de atributo **renda anual** , a menos que você habilite o agrupamento de membros.  
  
3.  Feche a guia **Explorar Tabela Cliente** .  
  
4.  No painel **atributos** , selecione **renda anual**.  
  
5.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para **Automatic** e altere o valor da propriedade **DiscretizationBucketCount** para `5`.  
  
     A imagem a seguir mostra as propriedades modificadas para **renda anual**.  
  
     ![Propriedades modificadas para renda anual](../../2014/tutorials/media/l4-discretizationmethod-1.gif "Propriedades modificadas para renda anual")  
  
## <a name="grouping-attribute-hierarchy-members-in-the-employee-dimension"></a>Agrupando membros de hierarquia de atributo na dimensão funcionário  
  
1.  Alterne para o designer de dimensão da dimensão funcionário.  
  
2.  No painel **exibição da fonte de dados** , clique com o botão direito do mouse na tabela **funcionário** e clique em **explorar dados**.  
  
     Observe os valores para a coluna **SickLeaveHours** e a coluna **VacationHours** .  
  
3.  Feche a guia **explorar tabela de funcionários** .  
  
4.  No painel **atributos** , selecione **horas de licença médica**.  
  
5.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para **clusters** e altere o valor da propriedade **DiscretizationBucketCount** para `5`.  
  
6.  No painel **atributos** , selecione **horas de férias**.  
  
7.  No janela Propriedades, altere o valor da propriedade **DiscretizationMethod** para **áreas iguais** e altere o valor da propriedade **DiscretizationBucketCount** para `5`.  
  
## <a name="browsing-the-modified-attribute-hierarchies"></a>Navegando pelas hierarquias de atributo modificadas  
  
1.  No menu **Compilar** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique em **implantar Analysis Services tutorial**.  
  
2.  Quando a implantação for concluída com êxito, mude para o designer de cubo para o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubo de tutorial e, em seguida, clique em **reconectar** na guia **navegador** .  
  
3.  Clique no ícone do Excel e clique em **Habilitar**.  
  
4.  Arraste a medida **vendas pela Internet/valor das vendas** até a área valores da lista de campos da tabela dinâmica.  
  
5.  Na lista de campos, expanda a dimensão **produto** e arraste a hierarquia de usuário **linhas de modelo de produto** para a área rótulos de **linha** da lista de campos.  
  
6.  Expanda a dimensão **cliente** na lista de campos, expanda a pasta de exibição **demográfica** e arraste a hierarquia de atributo **renda anual** para a área **Rótulos de coluna** .  
  
     Os membros da hierarquia de atributo **renda anual** agora são agrupados em seis buckets, incluindo um Bucket de vendas para clientes cuja renda anual é desconhecida. Nem todos os buckets são exibidos.  
  
7.  Remova a hierarquia de atributo **renda anual** da área colunas e remova a medida **vendas pela Internet/valor das vendas** da área **valores** .  
  
8.  Adicione a medida **vendas do revendedor/valor das vendas** à área de dados.  
  
9. Na lista de campos, expanda a dimensão **Funcionário** , expanda **Organização**e, em seguida, arraste **Horas de Dispensa Médica** para **Rótulos de Coluna**.  
  
     Observe que todas as vendas são feitas por funcionários dentro de um dos dois grupos. Observe também que os funcionários com 32-42 de licenças de licença de doença fizeram muito mais vendas do que funcionários com 20-31 de horas de licença de doença.  
  
     A imagem a seguir mostra as vendas dimensionadas por horas de licença de doença do funcionário.  
  
     ![Vendas dimensionadas por horas de licença de doença do funcionário](../../2014/tutorials/media/l4-discretizationmethod-2.gif "Vendas dimensionadas por horas de licença de doença do funcionário")  
  
10. Remova a hierarquia de atributo **horas de licença médica** da área coluna do painel **dados** .  
  
11. Adicione **horas de férias** à área de coluna do painel **dados** .  
  
     Observe que dois grupos aparecem, com base no método de agrupamento áreas iguais. Três outros grupos estão ocultos porque não contêm valores de dados.  
  
## <a name="modifying-grouping-properties-and-reviewing-the-effect-of-the-changes"></a>Modificando Propriedades de agrupamento e revisando o efeito das alterações  
  
1.  Alterne para o designer de dimensão da dimensão **funcionário** e, em seguida, selecione **horas de férias** no painel **atributos** .  
  
2.  No janela Propriedades, altere o valor da propriedade **DiscretizationBucketCount** para **10.**  
  
3.  No menu **Compilar** do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **implantar Analysis Services tutorial**.  
  
4.  Quando a implantação for concluída com êxito, volte para o designer de cubo para o cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutorial.  
  
5.  Clique em **reconectar** na guia **navegador** , clique no ícone do Excel e, em seguida, reconstrua a tabela dinâmica para que você possa exibir o efeito da alteração para o método de agrupamento:  
  
    1.  Arraste vendas do revendedor/valor das vendas para valores  
  
    2.  Arraste as horas de férias (na pasta de organização funcionários) para colunas  
  
    3.  Arrastar linhas de modelo de produto para linhas  
  
     Observe que, agora, há três grupos de membros do atributo **Horas de Férias** que contêm valores de vendas para produtos. (Os outros sete grupos contêm membros sem dados de vendas.)  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa na lição  
 [Ocultando e desabilitando hierarquias de atributo](lesson-4-4-hiding-and-disabling-attribute-hierarchies.md)  
  
## <a name="see-also"></a>Consulte também  
 [Agrupar Membros &#40;de atributo discretização&#41;](multidimensional-models/attribute-properties-group-attribute-members.md)  
  
  
