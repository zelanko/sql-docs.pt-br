---
title: Estruturas de mineração (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- mining structures [Analysis Services], about mining structures
- mining structures [Analysis Services]
- data mining [Analysis Services], structure
- Analysis Services objects, data mining objects
- data mining [Analysis Services], models
- algorithms [data mining]
- data mining [Analysis Services], objects
- mining models [Analysis Services]
- mining models [Analysis Services], about data mining models
ms.assetid: 39748290-c32a-48e6-92a6-0c3a9223773a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cfc630ffc943a989348e350c3668452a2777298
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083375"
---
# <a name="mining-structures-analysis-services---data-mining"></a>Estruturas de mineração (Analysis Services – Mineração de dados)
  A estrutura de mineração define os dados a partir dos quais os modelos de mineração são criados. Ela especifica a exibição da fonte de dados, o número e tipo de colunas e uma partição opcional nos conjuntos de treinamento e teste. Uma única estrutura de mineração pode oferecer suporte a vários modelos de mineração que compartilham o mesmo domínio. O diagrama a seguir mostra a relação da estrutura de mineração de dados com a fonte de dados e com os modelos de mineração de dados que a compõe.  
  
 ![Processamento de dados: origem para estrutura para modelo](../media/dmcon-modelarch.gif "Processamento de dados: origem para estrutura para modelo")  
  
 A estrutura de mineração apresentada neste diagrama tem como base uma fonte de dados que contém diversas tabelas ou exibições unidas no campo CustomerID. Uma tabela contém informações sobre os clientes, como região geográfica, idade, renda e sexo, enquanto que a tabela aninhada relacionada contém diversas linhas com informações adicionais sobre cada cliente, como o tipo de produto adquirido. O diagrama mostra que vários modelos podem ser criados na mesma estrutura de mineração e que os modelos podem usar colunas diferentes da estrutura.  
  
 **Modelo 1** Usa CustomerID, renda, idade, região e filtra os dados na região.  
  
 **Modelo 2** Usa CustomerID, renda, idade, região e filtra os dados em idade.  
  
 **Modelo 3** Usa CustomerID, age, sexo e a tabela aninhada, sem filtro.  
  
 Como os modelos usam colunas diferentes para entrada e, além disso, dois modelos restringem ainda mais os dados que são usados no modelo com a aplicação de um filtro, os modelos podem ter resultados bem diferentes, mesmo que tenham como base os mesmos dados. Observe que a coluna CustomerID é obrigatória em todos os modelos, pois ela é a única coluna disponível que pode ser usada como chave do caso.  
  
 Esta seção explica a arquitetura básica de estruturas de mineração de dados: como você define uma estrutura de mineração, como você a popula com dados e como você a usa para criar modelos. Para obter mais informações sobre como gerenciar ou exportar estruturas de mineração de dados existentes, consulte [Gerenciamento de soluções de mineração de dados e objetos](management-of-data-mining-solutions-and-objects.md).  
  
## <a name="defining-a-mining-structure"></a>Definindo uma estrutura de mineração  
 A configuração de uma estrutura de mineração de dados inclui as seguintes etapas:  
  
-   Definir uma fonte de dados.  
  
-   Selecionar colunas de dados para incluir na estrutura (nem todas as colunas precisam ser adicionadas ao modelo) e definindo uma chave.  
  
-   Definir uma chave para a estrutura, incluindo a chave para a tabela aninhada, se aplicável.  
  
-   Especifique se os dados de origem devem estar separados em um conjunto de treinamento e um conjunto de teste. Esta etapa é opcional.  
  
-   Processe a estrutura.  
  
 Essas etapas estão descritas com mais detalhes nas seções a seguir.  
  
### <a name="data-sources-for-mining-structures"></a>Fontes de dados para estruturas de mineração  
 Quando você define uma estrutura de mineração, você usa colunas que estão disponíveis em uma exibição da fonte de dados existente. Uma exibição de fonte de dados é um objeto compartilhado que permite que você combine várias fontes de dados. As fontes de dados originais não são visíveis a aplicativos cliente e você pode usar as propriedades da exibição da fonte de dados para modificar tipos de dados, criar agregações, ou designar um alias para as colunas.  
  
 Se você criar vários modelos de mineração a partir da mesma estrutura de mineração, os modelos poderão usar colunas diferentes da estrutura. Por exemplo, você pode criar uma única estrutura e, em seguida, criar uma árvore de decisão separada e modelos clustering dele, com cada modelo usando colunas diferentes e prevendo atributos diferentes.  
  
 Além disso, cada modelo pode usar as colunas da estrutura de modos diferentes. Por exemplo, sua exibição da fonte de dados pode conter uma coluna de Receita que você pode guardar de modos diferentes para modelos diferentes.  
  
 A estrutura de mineração de dados armazena a definição da fonte de dados e as colunas nela na forma de *associações* para os dados de origem. Para obter mais informações sobre associações de fonte de dados, consulte [Fontes de dados e associações &#40;SSAS Multidimensional&#41;](../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md). No entanto, observe que você também pode criar uma estrutura de mineração de dados sem associá-la a uma fonte de dados específica usando a instrução DMX [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
### <a name="mining-structure-columns"></a>Colunas da estrutura de mineração  
 Os blocos de construção da estrutura de mineração são as colunas da estrutura de mineração, que descrevem os dados que a fonte de dados contém. Essas colunas contêm informações como tipo de dados, tipo de conteúdo e como os dados são distribuídos. A estrutura de mineração não contém informações sobre como as colunas são usadas para um modelo de mineração específico ou sobre o tipo de algoritmo usado para criar um modelo; essas informações são definidas no próprio modelo de mineração.  
  
 Uma estrutura de mineração também pode conter tabelas aninhadas. Uma tabela aninhada representa uma relação um para muitos entre a entidade de um caso e seus atributos relacionados. Por exemplo, se as informações que descrevem o cliente residirem em uma tabela, e as compras do cliente residirem em outra tabela, você poderá usar tabelas aninhadas para combinar as informações em um único caso. O identificador de cliente é a entidade, e as compras são os atributos relacionados. Para obter mais informações sobre quando usar tabelas aninhadas, consulte [Tabelas aninhadas &#40;Analysis Services – Mineração de dados&#41;](nested-tables-analysis-services-data-mining.md).  
  
 Para criar um modelo de mineração de dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você deve primeiro criar uma estrutura de mineração de dados. O Assistente de Mineração de Dados o guia pelo processo de criação de uma estrutura de mineração, seleção de dados e adição de um modelo de mineração.  
  
 Se você criar um modelo de mineração usando DMX (Data Mining Extensions), poderá especificar o modelo e as colunas nele, e o DMX criará automaticamente a estrutura de mineração necessária. Para obter mais informações, consulte [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx).  
  
 Para obter mais informações, consulte [Colunas da estrutura de mineração](mining-structure-columns.md).  
  
### <a name="dividing-the-data-into-training-and-testing-sets"></a>Dividindo os dados em conjuntos de treinamento e de teste  
 Quando você define os dados da estrutura de mineração, você também pode especificar que alguns deles devem ser usados para treinamento e outros para teste. Portanto, não é mais necessário separar seus dados antes de criar uma estrutura de mineração de dados. Em vez disso, enquanto você cria seu modelo, pode especificar que uma determinada porcentagem dos dados são para teste e que o restante deve ser usado para treinamento ou pode especificar que um determinado número de casos deve ser usado como conjunto de dados de teste. As informações sobre os conjuntos de dados de treinamento e teste são armazenadas em cache com a estrutura de mineração e, como resultado, o mesmo conjunto de teste pode ser usado com todos os modelos baseados nessa estrutura,  
  
 Para obter mais informações, consulte [Training and Testing Data Sets](training-and-testing-data-sets.md).  
  
### <a name="enabling-drillthrough"></a>Habilitando o detalhamento  
 Você pode adicionar colunas à estrutura de mineração mesmo que você não pretenda usá-la em um modelo de mineração específico. Isso será útil, por exemplo, se você desejar recuperar os endereços de email de clientes em um modelo de clustering, sem usar o endereço de email durante o processo de análise. Para ignorar uma coluna durante a fase de análise e previsão, você a adiciona à estrutura, mas não especifica um uso para a coluna, ou define o sinalizador de uso como Ignorar. Os dados sinalizados dessa maneira podem ainda ser usados em consultas se o detalhamento tiver sido habilitado no modelo de mineração e se você tiver as permissões apropriadas. Por exemplo, você pode examinar os clusters resultantes da análise de todos os clientes, e então usar uma consulta de detalhamento para obter os nomes e endereços de email de clientes em um cluster específico, mesmo que essas colunas de dados não tenham sido usadas para criar o modelo.  
  
 Para obter mais informações, consulte [Drillthrough Queries &#40;Data Mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="processing-mining-structures"></a>Processando estruturas de mineração  
 Uma estrutura de mineração é apenas um contêiner de metadados até ser processado. Quando você processa uma estrutura de mineração, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria um cache local que armazena estatísticas sobre os dados, informações sobre como qualquer atributo contínuo é discretizado e outras informações que serão usadas posteriormente pelos modelos de mineração. O próprio modelo de mineração não armazena estas informações de resumo, mas referencia as informações que foram armazenadas em cache quando a estrutura de mineração foi processada. No entanto, você não precisa reprocessar a estrutura cada vez que adiciona um novo modelo a uma estrutura existente; você poderá processar somente o modelo.  
  
 Você pode optar por descartar este cache depois de processar, se o cache for muito grande ou você desejar remover dados detalhados. Se não quiser que os dados sejam armazenados em cache, poderá alterar a propriedade `CacheMode` da estrutura de mineração como `ClearAfterProcessing`. Isso destruirá o cache depois que qualquer modelo for processado. A definição da propriedade `CacheMode` como `ClearAfterProcessing` desabilitará o detalhamento do modelo de mineração.  
  
 No entanto, depois de destruir o cache, você não será capaz de adicionar novos modelos à estrutura de mineração. Ao adicionar um novo modelo de mineração à estrutura, ou alterar as propriedades de modelos existentes, você precisará reprocessar a estrutura de mineração primeiro. Para obter mais informações, consulte [Requisitos e considerações sobre processamento &#40;Mineração de dados&#41;](processing-requirements-and-considerations-data-mining.md).  
  
### <a name="viewing-mining-structures"></a>Exibindo estruturas de mineração  
 Você não pode usar visualizadores para procurar dados em uma estrutura de mineração. No entanto, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], é possível usar a guia **Estrutura de Mineração** do Designer de Mineração de Dados para exibir as colunas de estrutura e suas definições. Para obter mais informações, consulte [Designer de Mineração de Dados](data-mining-designer.md).  
  
 Se quiser revisar os dados na estrutura de mineração, poderá criar consultas usando DMX (Data Mining Extensions). Por exemplo, a instrução `SELECT * FROM <structure>.CASES` retorna todos os dados da estrutura de mineração. Para recuperar essas informações, a estrutura de mineração deve ter sido processada e os resultados desse processamento devem ter sido armazenados em cache.  
  
 A instrução `SELECT * FROM <model>.CASES` retorna as mesmas colunas, mas apenas para os casos de um determinado modelo. Para obter mais informações, consulte [SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases) e [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx).  
  
## <a name="using-data-mining-models-with-mining-structures"></a>Usando modelos de mineração de dados com estruturas de mineração  
 Um modelo de mineração de dados aplica um algoritmo de modelo de mineração aos dados que são representados por uma estrutura de mineração. Um modelo de mineração é um objeto que pertence a uma estrutura de mineração específica e herda todos os valores de propriedades definidas pela estrutura de mineração. O modelo pode usar todas as colunas contidas na estrutura de mineração ou um subconjunto das colunas. Você pode adicionar várias cópias de uma coluna de estrutura a uma estrutura. Você também pode adicionar várias cópias de uma coluna de estrutura a um modelo e atribuir nomes diferentes ou *aliases*a cada coluna de estrutura do modelo. Para obter mais informações sobre colunas de estrutura de nome alternativo, consulte [Criar um alias para uma coluna de modelo](create-an-alias-for-a-model-column.md) e [Propriedades do modelo de mineração](mining-model-properties.md).  
  
 Para obter mais informações sobre a arquitetura dos modelos de mineração de dados, consulte [Modelos de mineração &#40;Analysis Services – Data Mining&#41;](mining-models-analysis-services-data-mining.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Use os links fornecidos aqui para saber mais sobre como definir, gerenciar e usar estruturas de mineração.  
  
|Tarefas|Links|  
|-----------|-----------|  
|Trabalhar com estruturas de mineração relacionais|[Criar uma nova estrutura de mineração relacional](create-a-new-relational-mining-structure.md)<br /><br /> [Adicionar uma tabela aninhada a uma estrutura de mineração](add-a-nested-table-to-a-mining-structure.md)|  
|Trabalhar com estruturas de mineração com base em cubos OLAP|[Criar uma nova estrutura de mineração OLAP](create-a-new-olap-mining-structure.md)<br /><br /> [Filtrar o cubo de origem para uma estrutura de mineração](../filter-the-source-cube-for-a-mining-structure.md)|  
|Trabalhar com colunas em uma estrutura de mineração|[Adicionar colunas a uma estrutura de mineração](add-columns-to-a-mining-structure.md)<br /><br /> [Remover colunas de uma estrutura de mineração](remove-columns-from-a-mining-structure.md)|  
|Alterar ou consultar dados e propriedades da estrutura de mineração|[Alterar as propriedades de uma estrutura de mineração](change-the-properties-of-a-mining-structure.md)|  
|Trabalhar com as fontes de dados subjacentes e atualizar dados de origem|[Editar a exibição da fonte de dados usada para a Estrutura de Mineração](edit-the-data-source-view-used-for-a-mining-structure.md)<br /><br /> [Processar uma estrutura de mineração](process-a-mining-structure.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Objetos de banco de dados &#40;Analysis Services-&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Modelos de mineração &#40;Analysis Services de mineração de dados&#41;](mining-models-analysis-services-data-mining.md)  
  
  
