---
title: Criar e gerenciar uma partição Local (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44b27801af70756913b293afd5e7613f3e026d82
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076302"
---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>Criar e gerenciar uma partição local (Analysis Services)
  Você pode criar mais partições para um grupo de medidas para melhorar o desempenho do processamento. Ter várias partições permite a você alocar dados de fatos em diversos arquivos de dados físicos correspondentes em servidores locais e remotos. No Analysis Services, as partições podem ser processadas de forma independente e em paralelo, permitindo maior controle sobre o processamento de cargas de trabalho no servidor.  
  
 As partições podem ser criadas no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] durante o design de modelo, ou após a implantação da solução usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o XMLA. É recomendável escolher apenas uma abordagem. Se você alternar entre ferramentas, talvez descubra que alterações feitas em um banco de dados implantado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são substituídas quando você subsequentemente reimplanta a solução do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
## <a name="before-you-start"></a>Antes de iniciar  
 Verifique se você tem a edição business intelligence ou enterprise. A edição Standard não oferece suporte a várias partições. Para verificar a edição, clique com o botão direito do mouse no nó de servidor no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e escolha **Relatórios** | **Geral**. Para obter mais informações sobre disponibilidade de recursos, consulte [recursos compatíveis com as edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Logo no início, é importante compreender que as partições devem compartilhar o mesmo design de agregação se você pretende mesclá-las posteriormente. As partições só poderão ser mescladas se tiverem designs de agregação e modos de armazenamento idênticos.  
  
> [!TIP]  
>  Explore os dados na DSV (exibição da fonte de dados) para compreender o intervalo e a profundidade dos dados que você está particionando. Por exemplo, se você estiver particionando por data, poderá classificar em uma coluna de data para determinar os limites superior e inferior de cada partição.  
  
## <a name="choose-an-approach"></a>Escolher uma abordagem  
 O aspecto mais importante ao criar partições é segmentar os dados para que não haja linhas duplicadas. Os dados devem ser armazenados em uma única partição para evitar contar duas vezes as mesmas linhas. Portanto, é comum particionar por DATA de forma que você possa definir limites claros entre cada partição.  
  
 Você pode usar qualquer técnica para distribuir os dados de fatos em várias partições. As técnicas a seguir podem ser usadas para segmentar os dados.  
  
|Técnica|Recomendações|  
|---------------|---------------------|  
|Use consultas SQL para segmentar dados de fatos|As partições podem se originar de consultas SQL. Durante o processamento, a consulta SQL deve recuperar os dados. A cláusula WHERE da consulta fornece o filtro que segmentar os dados para cada partição. O Analysis Services gera a consulta, mas você precisa preencher a cláusula WHERE para segmentar os dados corretamente.<br /><br /> A maior vantagem dessa abordagem é a facilidade em particionar dados de uma única tabela de origem. Se todos os dados de origem forem obtidos de uma grande tabela de fatos, você poderá criar consultas que filtrem esses dados em partições discretas, sem precisar criar estruturas de dados adicionais na DSV (exibição da fonte de dados).<br /><br /> Uma desvantagem é que o uso de consultas quebrará a associação entre a partição e a DSV. Caso você atualize a DSV mais tarde no projeto do Analysis Services, por exemplo, adicionando colunas à tabela de fatos, edite manualmente as consultas para cada partição para incluir a nova coluna. A segunda abordagem, discutida em seguida, não tem esta desvantagem.|  
|Use tabelas na DSV para segmentar dados de fatos|Você pode associar uma partição a uma tabela, consulta nomeada ou exibição na DSV. Como base de uma partição, as três são funcionalmente equivalentes. Uma tabela inteira, uma consulta nomeada ou uma exibição fornece todos os dados para uma única partição.<br /><br /> Usando uma tabela, exibição ou consulta nomeada, toda a lógica de seleção dos dados é colocada na DSV, que pode ser mais fácil de gerenciar e manter ao longo do tempo. Uma grande vantagem nessa abordagem é que as associações de tabela são preservadas. Se você atualizar a tabela de origem posteriormente, não precisará modificar as partições que a utilizam. Em segundo lugar, todas as tabelas, consultas nomeadas e exibições existem em um espaço de trabalho em comum, tornando as atualizações mais convenientes do que precisar abrir e editar cada consulta de partição separadamente.|  
  
## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>Opção 1: Filtrar uma tabela de fatos para várias partições  
 Para criar várias partições, comece alterando a propriedade **Source** da partição padrão. Por padrão, um grupo de medidas é criado usando uma única partição que está associada a uma única tabela da DSV. Antes de adicionar mais partições, primeiro modifique a partição original para conter apenas uma parte dos dados de fatos. Você pode continuar criando partições adicionais para armazenar o restante dos dados.  
  
 Construa seus filtros de modo que os dados não sejam duplicados entre as partições. O filtro de uma partição especifica quais dados da tabela de fatos são usados na partição. É importante que os filtros de todas as partições de um cubo extraiam conjuntos de dados mutuamente exclusivos da tabela de fatos. Os mesmos dados de fatos podem ser contados em dobro quando aparecem em várias partições.  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], em Gerenciador de Soluções, clique duas vezes no cubo para abri-lo no Designer de Cubo e, depois, clique na guia **Partições** .  
  
2.  Expanda o grupo de medidas para o qual você está adicionando partições. Por padrão, cada grupo de medidas tem uma partição, associada a uma tabela de fatos no DSV.  
  
3.  Na coluna Origem, clique no botão Procurar (. .) para abrir a caixa de diálogo Origem da Partição.  
  
     ![Coluna de origem no painel de partição](../media/ssas-partitionsource.png "coluna de origem no painel de partição")  
  
4.  No Tipo de Associação, selecione **Associação de Consulta**. A consulta SQL que seleciona os dados aparece automaticamente.  
  
5.  No final da cláusula WHERE, adicione um filtro que segmente dados para essa partição.  
  
     Exemplos de sintaxe da cláusula WHERE incluem `WHERE OrderDateKey >= '20060101'` ou `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`. Para obter outros exemplos, consulte [WHERE &#40;Transact-SQL&#41;](/sql/t-sql/queries/where-transact-sql).  
  
     Observe que os seguintes filtros são mutuamente exclusivos em cada conjunto:  
  
    |||  
    |-|-|  
    |Conjunto 1:|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|  
    |Conjunto 2:|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|  
    |Conjunto 3:|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|  
  
6.  Clique em **Verificar** para verificar se há erros de sintaxe e, depois, em **OK**.  
  
7.  Repita as etapas anteriores para criar as partições restantes, alterando a cláusula WHERE a cada vez para selecionar a próxima fatia de dados.  
  
8.  Implante a solução ou processe a partição para carregar os dados. Verifique se todas as partições foram processadas.  
  
9. Navegue no cubo para verificar se os dados corretos foram retornados.  
  
 Quando você tiver um grupo de medidas que use vários grupos de medidas, poderá criar mais partições no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Em um grupo de medidas, clique com o botão direito do mouse na pasta Partições e selecione **Novas Partições** para iniciar o assistente.  
  
> [!NOTE]  
>  Em vez de filtrar dados em uma partição, é possível usar a mesma consulta para criar uma consulta nomeada na DSV e, em seguida, basear a partição na consulta nomeada.  
  
## <a name="option-2-use-tables-views-or-named-queries"></a>Opção 2: Usar tabelas, exibições ou consultas nomeadas  
 Se a DSV já organiza fatos em tabelas individuais (por exemplo, por ano ou trimestre), você pode criar partições baseadas em uma tabela individual, onde cada partição tem sua própria tabela de fonte de dados. É essencialmente dessa forma que grupos de medidas são particionados por padrão, mas, no caso de várias partições, você quebra a partição original em várias partições, e mapeia cada nova partição para a tabela de fonte de dados que fornece os dados.  
  
 As exibições e consultas nomeadas são equivalentes funcionais de tabelas, pois os três objetos são definidos na DSV e associados a uma partição usando a opção Associação de Tabela na caixa de diálogo Origem da Partição. Você pode criar uma exibição ou consulta nomeada para gerar o segmento de dados necessário a cada partição. Para obter mais informações, consulte [Definir consultas nomeadas em uma exibição da fonte de dados &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md).  
  
> [!IMPORTANT]  
>  Ao criar consultas nomeadas mutuamente exclusivas para partições em uma DSV, verifique se os dados combinados das partições incluem todos os dados de um grupo de medidas a serem incluídas no cubo. Não deixe uma partição padrão se basear na tabela inteira do grupo de medidas, pois as partições baseadas em consultas sobrepõem a consulta baseada na tabela inteira.  
  
1.  Crie uma ou mais consultas nomeadas para usar como a origem da partição. Para obter mais informações, consulte [Definir consultas nomeadas em uma exibição da fonte de dados &#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md).  
  
     A consulta nomeada deve se basear na tabela de fatos associada ao grupo de medidas. Por exemplo, se você estiver particionando o grupo de medidas FactInternetSales, as consultas nomeadas na DSV deverão especificar a tabela FactInternetSales na instrução FROM.  
  
2.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], em Gerenciador de Soluções, clique duas vezes no cubo para abri-lo no Designer de Cubo e, depois, clique na guia **Partições** .  
  
3.  Expanda o grupo de medidas para o qual você está adicionando partições.  
  
4.  Clique em **Nova Partição** para iniciar o Assistente para Partições. Se você criou as consultas nomeadas usando a tabela de fatos associada ao grupo de medidas, verá cada uma das consultas nomeadas criadas na etapa anterior.  
  
5.  Em Especificar Informações sobre a Origem, escolha uma das consultas nomeadas criadas em uma etapa anterior. Se você não encontrar consultas nomeadas, volte para a DSV e verifique a instrução FROM.  
  
6.  Clique em **Avançar** para aceitar os valores padrão de cada página subsequente.  
  
7.  Na última página, Concluindo o Assistente, atribua um nome descritivo à partição.  
  
8.  Clique em **Concluir**.  
  
9. Repita as etapas anteriores para criar as partições restantes, cada vez escolhendo uma consulta nomeada diferente para selecionar a próxima fatia de dados.  
  
10. Implante a solução ou processe a partição para carregar os dados. Verifique se todas as partições foram processadas.  
  
11. Navegue no cubo para verificar se os dados corretos foram retornados.  
  
## <a name="next-step"></a>Próxima etapa  
 Ao criar consultas mutuamente exclusivas para partições, verifique se os dados combinados da partição incluem todos os dados que deseja incluir no cubo.  
  
 Como etapa final, em geral você deseja remover a partição padrão que se baseava na própria tabela (caso ela ainda exista); caso contrário, a consulta baseada na tabela completa será sobreposta pelas partições baseadas na consulta.  
  
## <a name="see-also"></a>Consulte também  
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Partições remotas](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Mesclar partições no Analysis Services &#40;SSAS – Multidimensional&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
