---
title: Criar uma estrutura de mineração OLAP | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b5ad8add984db3c83cfc6b3af99f430035f56d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-olap-mining-structure"></a>Criar uma estrutura de mineração OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Há muitas vantagens na criação de um modelo de mineração de dados baseado em um cubo OLAP ou em outro repositório de dados multidimensional. Uma solução de OLAP já contém grandes volumes de dados que estão bem-organizados, limpos e corretamente formatados; contudo, a complexidade dos dados é tamanha que é pouco provável que usuários localizem padrões significativos pela exploração ad hoc. A mineração de dados permite descobrir novas correlações e apresenta ideias acionáveis.  
  
 Este tópico descreve como criar uma estrutura de mineração OLAP, com base em uma dimensão e em medidas relacionadas em uma solução multidimensional existente.  
  
 [Requisitos](#bkmk_Reqs)  
  
 [Visão geral do processo de mineração de dados OLAP](#bkmk_Overview)  
  
 [Cenários para usar a mineração de dados em soluções OLAP](#bkmk_OLAP_Scenarios)  
  
 [Filtros](#bkmk_Filters)  
  
 [Usando tabelas aninhadas](#bkmk_Nested)  
  
 [Dimensões de mineração de dados](#bkmk_DMDimension)  
  
##  <a name="bkmk_Reqs"></a> Requisitos para a estrutura e modelos de mineração OLAP  
 Se você está criando um modelo de mineração OLAP, sua fonte de dados já existe, no banco de dados usado para criar o cubo. Você não pode se conectar a um cubo remoto e criar objetos de mineração de dados; os objetos de cubo devem estar disponíveis na mesma solução que o banco de dados como a estrutura de mineração que você criará.  
  
 Se você não tiver os arquivos de projeto originais, ou não quiser alterá-los, poderá usar a opção no Visual Studio, **Importar do Servidor (Multidimensional ou Mineração de dados)**, para obter uma cópia dos metadados e dos objetos de solução. Você pode modificar o destino de implantação, editar fontes de dados e trabalhar com os objetos de cubo sem afetar os objetos existentes.  
  
 Para obter mais informações, consulte [Importar um projeto de mineração de dados usando o Assistente de Importação do Analysis Services](../../analysis-services/data-mining/import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
##  <a name="bkmk_Overview"></a> Visão geral do processo de mineração de dados OLAP  
 Inicie o Assistente de Mineração de Dados, clicando com o botão direito do mouse no nó **Estruturas de Mineração** , no Gerenciador de Soluções, e selecionando  **Nova Estrutura de Mineração**. O assistente orienta-o pelas seguintes etapas para criar a estrutura de um novo modelo e estrutura:  
  
1.  **Selecionar o Método de Definição**: aqui você seleciona um tipo de fonte de dados e escolhe **De cubo existente**.  
  
    > [!NOTE]  
    >  O cubo OLAP usado como uma origem deve existir no mesmo banco de dados que a estrutura de mineração, conforme descrito acima. Além disso, você não pode usar um cubo criado pelo suplemento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel como uma fonte para mineração de dados.  
  
2.  **Criar a Estrutura de Mineração de Dados**: determina se você criará somente uma estrutura ou uma estrutura com um modelo de mineração.  
  
     Você também deve escolher um algoritmo apropriado para analisar seus dados. Para obter orientação sobre qual algoritmo é melhor para determinadas tarefas, consulte HYPERLINK "ms-help://SQL111033/as_1devconc/html/ed1fc83b-b98c-437e-bf53-4ff001b92d64.htm" Algoritmos de mineração de dados (Analysis Services - Data Mining).  
  
3.  **Selecionar a Dimensão do Cubo de Origem**: Esta etapa equivale a selecionar uma fonte de dados. Você precisa escolher a única dimensão que contém os dados mais importantes usados para treinar seu modelo. Você pode adicionar dados de outras dimensões posteriormente ou filtrar a dimensão.  
  
4.  **Selecionar a Chave do Caso**: na dimensão recém-selecionada, escolha um atributo (coluna) para servir como o identificador exclusivo de seus dados de caso.  
  
     Normalmente, uma coluna será pré-selecionada para você, mas será possível alterar a coluna se houver várias chaves.  
  
5.  **Selecionando Colunas de Nível de Caso**: Aqui você escolhe os atributos da dimensão selecionada e as medidas relacionadas, que são relevantes para sua análise. Esta etapa equivale a selecionar colunas de uma tabela.  
  
     O assistente inclui automaticamente para sua análise e seleção quaisquer medidas criadas usando atributos da dimensão selecionada.  
  
     Por exemplo, se seu cubo contiver uma medida que calcula o custo de frete com base na localização geográfica do cliente, e você escolher a dimensão Cliente como a fonte de dados principal para modelagem, a medida será proposta como um candidato a ser adicionado ao modelo. Tenha cuidado ao adicionar muitas medidas que já estejam diretamente baseadas em atributos, pois já existe uma relação implícita entre as colunas, conforme definido na fórmula de medida, e a força desta correlação (esperada) pode obscurecer outras relações porventura descobertas.  
  
6.  **Especificar Uso de Colunas do Modelo de Mineração**: Para cada atributo ou medida adicionada à estrutura, especifique se o atributo deve ser usado para previsão ou como entrada. Se você não selecionar uma destas opções, os dados serão processados, mas não serão usados para análise; porém, eles estarão disponíveis como dados em segundo plano caso você habilite o detalhamento posteriormente.  
  
7.  **Adicionar tabelas aninhadas**: Clique para adicionar tabelas relacionadas. Na caixa de diálogo **Selecionar uma Dimensão de Grupo de Medidas** , você pode escolher uma única dimensão entre as dimensões relacionadas à dimensão atual.  
  
     Em seguida, use a caixa de diálogo **Selecionar uma Chave de Tabela Aninhada** para definir como a nova dimensão é relacionada à dimensão que contém os dados de caso.  
  
     Use a caixa de diálogo **Selecionar Colunas de Tabela Aninhada** para escolher os atributos e as medidas da nova dimensão a ser usada na análise. Você também precisa especificar se o atributo aninhado será usado para previsão.  
  
     Depois de adicionar todos os atributos aninhados necessários, retorne à página, **Especificar Uso de Colunas do Modelo de Mineração**e clique em **Avançar**.  
  
8.  **Especificar Conteúdo e Tipo de Dados das Colunas**: A esta altura, você adicionou todos os dados que serão usados para análise e deve especificar o *tipo de dados* e o *tipo de conteúdo* para cada atributo.  
  
     Em um modelo OLAP, você não tem a opção de detectar tipos de dados automaticamente, porque o tipo de dados já está definido pela solução multidimensional e não pode ser alterado. As chaves também são identificadas automaticamente. Para obter mais informações, consulte [Tipos de dados &#40;Mineração de dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
     O *tipo de conteúdo* que você escolhe para cada coluna que usa no modelo informa como o algoritmo deve processar os dados. Para obter mais informações, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
9. **Dividindo o cubo de origem**: Aqui você pode definir filtros em um cubo para selecionar um subconjunto de dados e treinar modelos mais direcionados.  
  
     Você filtra um cubo escolhendo a dimensão de filtragem, selecionando o nível da hierarquia que contém os critérios a serem usados e digitando uma condição a ser usada como o filtro.  
  
10. **Criar Conjunto de Testes**: nesta página, você pode informar ao assistente quantos dados devem ser separados para uso ao testar o modelo. Se seus dados oferecerão suporte a vários modelos, convém criar um conjunto de dados de controle, de forma que todos os modelos possam ser testados nos mesmos dados.  
  
     Para obter mais informações, consulte [Teste e validação &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
11. **Concluindo o Assistente**: nessa página, dê um nome para a nova estrutura de mineração e para o modelo de mineração associado, e salve a estrutura e o modelo.  
  
     Nesta página, você também pode definir as seguintes opções:  
  
    -   **Permitir detalhamento**  
  
    -   **Criar dimensão do modelo de mineração**  
  
    -   **Criar cubo usando a dimensão do modelo de mineração**  
  
     Para saber mais sobre estas opções, consulte a seção posteriormente neste tópico, [Noções básicas de dimensões e detalhamento de mineração de dados](#bkmk_DMDimension).  
  
 Neste ponto, a estrutura de mineração e seu modelo são apenas metadados; você precisará processar ambos para obter resultados.  
  
##  <a name="bkmk_OLAP_Scenarios"></a> Cenários para uso de mineração de dados com dados OLAP  
 Os cubos OLAP geralmente contêm tantos membros e tantas dimensões que pode ser difícil saber por onde começar a mineração de dados. Para ajudar a identificar os padrões que os cubos contêm, geralmente você identifica uma única dimensão de interesse e, em seguida, começa a explorar os padrões relacionados à dimensão. A tabela a seguir lista várias tarefas de mineração de dados OLAP comuns, descreve os cenários de amostra nos quais você pode aplicar cada tarefa e identifica o algoritmo de mineração de dados a ser usado para cada tarefa.  
  
|Tarefa|Cenário de exemplo|Algoritmo|  
|----------|---------------------|---------------|  
|Agrupar membros em clusters|Segmente uma dimensão de cliente com base nas propriedades do membro do cliente, os produtos que os clientes compram e a quantidade de dinheiro que eles gastam.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Algoritmo de Cluster|  
|Localizar membros interessantes ou anormais|Identifique lojas interessantes ou anormais em uma dimensão de loja com base em vendas, lucros, local da loja e tamanho da loja.|Algoritmo de Árvores de Decisão da [!INCLUDE[msCoName](../../includes/msconame-md.md)]|  
|Localizar células interessantes ou anormais|Identifique as vendas por loja que contradizem as tendências típicas com o tempo.|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Algoritmo de série temporal|  
|Localize correlações|Identifique fatores relacionados ao tempo de inatividade do servidor, inclusive região, tipo de computador, SO ou data de compra.|Algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naïve Bayes|  
  
##  <a name="bkmk_Filters"></a>Dividindo um cubo versus. Filtrando modelos  
 Fatiar o cubo enquanto cria um modelo é como criar um filtro em um modelo de mineração relacional. Em um modelo relacional, o filtro na fonte de dados é definido como uma cláusula WHERE em uma instrução SQL; em um cubo, você usa o editor para criar instruções de filtro que usam MDX.  
  
 Por exemplo, um cubo pode conter informações sobre compras de produtos no mundo, mas, para sua campanha de marketing, você deseja criar um modelo baseado na análise de consumidoras com mais de 30 anos que morem no Reino Unido.  
  
 Neste cenário, você criaria dois filtros:  
  
-   Para o primeiro filtro, você escolherá a dimensão Geografia, escolherá a hierarquia para Região e usaria a lista **Expressão de Filtro** para escolher “Reino Unido” nos possíveis valores.  
  
-   Para o segundo filtro, você escolherá a dimensão Cliente, selecionará o atributo Gênero e selecionará “Feminino” na lista de valores de atributo.  
  
 Após a criação da estrutura de mineração, você pode modificar a definição dos dados de cubo e os critérios de filtro. Para obter mais informações, consulte [filtros para modelos de mineração](~/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 As guias **Estrutura de Mineração** e **Modelo de Mineração** fornecem uma opção para adicionar um filtro a uma estrutura de mineração existente, clicando em **Definir uma Fatia do Cubo**. A caixa de diálogo **Fatiar Cubo** ajuda-o a criar uma expressão de filtro MDX válida, escolhendo um valor nas listas suspensas.  
  
> [!WARNING]  
>  Observe que a interface por criar e procurar cubos foi alterada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Procurar dados e metadados no Cubo](../../analysis-services/multidimensional-models/browse-data-and-metadata-in-cube.md).  
  
 Você pode adicionar quantos filtros forem necessários no cubo para retornar os dados necessários ao modelo de mineração. Você também pode definir fatias em fatias de cubo individuais. Por exemplo, se a sua estrutura contiver duas tabelas aninhadas baseadas em produtos, você poderá fatiar uma tabela em março de 2004 e a outra tabela em abril de 2004. O modelo resultante poderá então ser usado para prever compras realizadas em abril com base nas compras que foram realizadas em março.  
  
##  <a name="bkmk_Nested"></a> Usando tabelas aninhadas em um modelo de mineração OLAP  
 Quando você usar o Assistente de Mineração de Dados para criar um modelo baseado em dados de cubo, poderá adicionar tabelas aninhadas especificando os nomes de dimensões relacionadas e, depois, escolhendo os atributos ou medidas a serem adicionadas ao modelo  
  
 Por exemplo, caso a dimensão principal usada para dados de caso seja Cliente, você pode adicionar a dimensão Produtos como uma dimensão relacionada, porque você espera que um cliente tenha solicitado vários produtos ao longo do tempo, e o cubo já vincula cada cliente aos diversos produtos por meio das tabelas de fatos de pedidos.  
  
 Você adiciona tabelas aninhadas à página **Especificar Uso de Colunas do Modelo de Mineração** do assistente, clicando em **Adicionar Tabelas Aninhadas**. Uma caixa de diálogo é aberta e orienta-o no processo de escolher uma dimensão relacionada, bem como na escolha de medidas. As dimensões de caso e aninhadas devem ser relacionadas por uma chave estrangeira, e medidas devem usar um dos atributos já incluídos nas tabelas de caso ou aninhadas. Infelizmente, estas restrições não contribuem muito para estreitar o escopo; assim, tenha cuidado ao selecionar apenas os atributos que são úteis para a modelagem.  
  
 Para cada atributo ou medida adicionada à tabela aninhada, especifique se o atributo aninhado será usado para previsão ou não, selecionando **Previsível** ou **Entrada** na caixa de diálogo **Selecionar Colunas de Tabela Aninhada** . Se você não selecionar uma destas opções, os dados serão adicionados à estrutura de mineração, mas não serão usados para análise.  
  
 Para cada atributo e medida, especifique também se o atributo é discreto, discretizado ou contínuo. O assistente selecionará previamente um padrão com base no tipo de dados do atributo, mas você pode precisar alterá-los, dependendo dos requisitos de algoritmo. Se você escolher um tipo de conteúdo que não seja compatível com o algoritmo escolhido (por exemplo, se usar um tipo numérico contínuo com um modelo Naïve Bayes), não obterá uma mensagem de erro até que tente processar o modelo.  
  
 Quando você terminar de configurar estas opções, o assistente adicionará a tabela aninhada à tabela de casos. O nome padrão para a tabela aninhada é o nome da dimensão aninhada, mas você pode alterar o nome da tabela aninhada e de suas colunas. Você pode repetir este processo para adicionar várias tabelas aninhadas à estrutura de mineração.  
  
 A capacidade de usar dados de tabela aninhada como essa é um recurso de mineração de dados do SQL Server especialmente avançado e, em um cubo, as possibilidades de usar subconjuntos de dados relacionados são praticamente ilimitadas.  
  
##  <a name="bkmk_DMDimension"></a> Noções básicas de dimensões e detalhamento de mineração de dados  
 A opção, **Permitir detalhamento**, permite executar consultas nos dados de cubo subjacentes ao procurar o modelo. Os dados não estão contidos na nova dimensão de mineração de dados, mas o banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode usar as associações de dados para recuperar as informações do cubo de origem.  
  
 A opção, **Criar dimensão de modelo de mineração**, permite gerar uma nova dimensão no cubo existente que contém os padrões descobertos pelo algoritmo. A hierarquia na nova dimensão é determinada em grande parte pelo tipo de modelo. Por exemplo, a representação de um modelo de clustering é simples, com o nó (Todos) na parte superior da hierarquia e cada cluster no próximo nível. Em contraste, a dimensão que é criada para um modelo de árvore de decisão pode ter uma hierarquia profunda, representando a ramificação da árvore.  
  
 A opção, **Criar cubo usando a dimensão do modelo de mineração**, permite exportar a nova dimensão de mineração de dados para um novo cubo. Quaisquer objetos requeridos para detalhamento na dimensão de mineração de dados serão incluídos automaticamente.  
  
> [!WARNING]  
>  Apenas estes tipos de modelo oferecem suporte à criação de dimensões de mineração de dados: modelos baseados no algoritmo Microsoft Clustering, no algoritmo Árvores de Decisão da Microsoft ou no algoritmo Associação da Microsoft.  
  
## <a name="see-also"></a>Consulte também  
 [Algoritmos de mineração de dados e &#40; Analysis Services – Data Mining e &#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Colunas de estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md)   
 [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md)   
 [Propriedades do modelo de mineração](../../analysis-services/data-mining/mining-model-properties.md)   
 [Propriedades de estrutura de mineração e colunas de estrutura](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)  
  
  
