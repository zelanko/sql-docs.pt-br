---
title: Criar uma estrutura de mineração relacional | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a808cfe9e5cd48ba689eac0bc4cb63123c4ef13a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543851"
---
# <a name="create-a-relational-mining-structure"></a>Criar uma estrutura de mineração relacional
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A maioria dos modelos de mineração de dados são baseados em fontes de dados relacionais. As vantagens de criar um modelo de mineração de dados relacional são que você pode montar dados ad hoc, além de treinar e atualizar um modelo sem a complexidade de criar um cubo.  
  
 Uma estrutura de mineração relacional pode tirar dados de origens distintas. Os dados brutos podem ser armazenados em tabelas, arquivos ou sistemas de banco de dados relacional, contanto que os dados possam ser definidos como parte da exibição da fonte de dados. Por exemplo, você deve usar uma estrutura de mineração relacional se seus dados estiverem no Excel, um data warehouse de SQL Server ou um banco de dados de relatório de SQL Server, ou em origens externas que são acessadas pelos provedores OLE DB ou ODBC.  
  
 Este tópico fornece uma visão geral de como usar o Assistente de Mineração de Dados para criar uma estrutura de mineração relacional.  
  
 [Requisitos](#BKMK_Relational_Structure)  
  
 [Processo para criar uma estrutura de mineração relacional](#BKMK_Relational_Structure)  
  
 [Como escolher fontes de dados](#BKMK_ChooseRelData)  
  
 [Como especificar tipo de conteúdo e tipo de dados](#bkmk_ContentDataType)  
  
 [Por que e como criar um conjunto de dados de controle](#bkmk_Holdout)  
  
 [Por que e como habilitar detalhamento](#BKMK_DrillThru)  
  
## <a name="requirements"></a>Requisitos  
 Primeiro, você deve ter uma fonte de dados existente. Você pode usar o designer de Fonte de Dados para configurar uma fonte de dados, se já não houver uma. Para obter mais informações, veja [Criar uma fonte de dados &#40;SSAS – Multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
 Em seguida, use o Assistente de Exibição da Fonte de Dados para montar dados exigidos em uma única exibição da fonte de dados. Para obter mais informações sobre como você pode selecionar, transformar, filtrar ou gerenciar dados com exibições da fonte de dados, consulte [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
##  <a name="BKMK_Relational_Structure"></a> Visão geral do processo  
 Inicie o Assistente de Mineração de Dados, clicando com o botão direito do mouse no nó **Estruturas de Mineração** no Gerenciador de Soluções e selecionando **Adicionar Nova Estrutura de Mineração**. O assistente o conduz pelas seguintes etapas para criar a estrutura para um novo modelo de mineração relacional:  
  
1.  **Selecione o método de definição**: Aqui você seleciona os dados de um tipo de fonte e, em seguida, escolha **do data warehouse relacional do banco de dados ou**.  
  
2.  **Criar a estrutura de mineração de dados**: Determine se você criará somente uma estrutura ou uma estrutura com um modelo de mineração.  
  
     Você também escolhe um algoritmo apropriado para seu modelo inicial. Para obter orientação sobre o melhor algoritmo para determinadas tarefas, consulte [Algoritmos de Mineração de Dados &#40;Analysis Services – Mineração de Dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
3.  **Selecionar exibição da fonte de dados**: Escolha um modo de exibição de fontes de dados para usar no seu modelo de treinamento. A exibição da fonte de dados também pode conter dados usados para teste ou dados não relacionados. Você consegue escolher quais dados são usados de fato na estrutura e no modelo. Você também pode aplicar filtros aos dados posteriormente.  
  
4.  **Especificar tipos de tabela**: Selecione a tabela que contém os casos usados para análise. Para alguns conjuntos de dados, principalmente os que são usados para criar modelos de cesta de compras, você também pode incluir uma tabela relacionada, para usar como uma tabela aninhada.  
  
     Para cada tabela, você deve especificar a chave, de forma que o algoritmo saiba identificar um registro exclusivo e registros relacionados se você tiver adicionado uma tabela aninhada.  
  
     Para obter mais informações, consulte [Colunas da estrutura de mineração](../../analysis-services/data-mining/mining-structure-columns.md).  
  
5.  **Especificar os dados de treinamento**: Nessa página, escolha como o *tabela de casos*, que é a tabela que contém os dados mais importantes para análise.  
  
     Para alguns conjuntos de dados, principalmente os que são usados para criar modelos de cesta de compras, você também pode incluir uma tabela relacionada. Os valores nessa tabela aninhada serão tratados como valores múltiplos que estão relacionados a uma única linha (ou caso) na tabela principal.  
  
6.  **Especificar o conteúdo de colunas e tipos de dados**: Para cada coluna que você usa na estrutura, você deve escolher uma *tipo de dados* e uma *tipo de conteúdo*.  
  
     O assistente automaticamente detectará possíveis tipos de dados, mas você não precisa usar o tipo de dados recomendado pelo assistente. Por exemplo, mesmo se seus dados contiverem números, eles podem ser representativos de dados categóricos. As colunas que você especificar como chaves são automaticamente atribuídas o tipo de dados correto para aquele tipo de modelo específico. Para obter mais informações, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md) e [Tipos de dados &#40;Mineração de Dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md).  
  
     O *tipo de conteúdo* que você escolhe para cada coluna que usa no modelo informa como o algoritmo deve processar os dados.  
  
     Por exemplo, você pode decidir discretizar números, em vez de usar valores contínuos. Você também pode pedir ao algoritmo para detectar o melhor tipo de conteúdo automaticamente para a coluna. Para obter mais informações, consulte [Tipos de conteúdo &#40;Mineração de dados&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
7.  **Criar conjunto de testes**: Nessa página, você pode informar o Assistente para a quantidade de dados deve ser definido reservados para uso ao testar o modelo. Se seus dados oferecerão suporte a vários modelos, convém criar um conjunto de dados de controle, de forma que todos os modelos possam ser testados nos mesmos dados.  
  
     Para obter mais informações, consulte [Teste e validação &#40;Mineração de dados&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
8.  **Concluindo o assistente**: Nessa página, dê um nome para a nova estrutura de mineração e o modelo de mineração associado e salve a estrutura e modelo.  
  
     Você também pode definir algumas opções importantes, dependendo do tipo de modelo. Por exemplo, você pode habilitar o detalhamento na estrutura.  
  
     Neste ponto, a estrutura de mineração e seu modelo são apenas metadados; você precisará processar ambos para obter resultados.  
  
##  <a name="BKMK_ChooseRelData"></a> Como escolher dados relacionais  
 As estruturas de mineração relacionais podem se basear em quaisquer dados disponíveis por meio de uma fonte de dados OLE DB. Se os dados de origem estiverem contidos em diversas tabelas, você poderá usar uma exibição de fonte de dados para montar as tabelas e as colunas desejadas em um único lugar.  
  
 Se as tabelas incluírem relações um-para-muitos-por exemplo, você tem vários registros de compra para cada cliente que você deseja analisar-você pode adicionar tabelas e, em seguida, usar uma tabela como tabela de casos, vinculação de dados no lado muitos da relação como uma tabela aninhada.  
  
 Os dados em uma estrutura de mineração são derivados do que existir na exibição da fonte de dados. Você pode modificar os dados como precisar dentro da exibição da fonte de dados, adicionando relações ou colunas derivadas que podem não estar presentes nos dados relacionais subjacentes. Você também pode criar cálculos nomeados ou agregações dentro da exibição da fonte de dados. Estes recursos são muito úteis se você não tiver controle sobre a organização de dados na fonte de dados, ou se você quiser experimentar com agregações diferentes de dados para seus modelos de mineração de dados.  
  
 Você não tem que usar todos os dados que estão disponíveis; você pode escolher quais colunas deseja incluir na estrutura de mineração. Todos os modelos que são baseados nessa estrutura podem usar essas colunas ou você pode sinalizar determinadas colunas como **Ignorar** para um modelo específico. É possível habilitar usuários de um modelo de mineração de dados para efetuar uma busca detalhada nos resultados do modelo de mineração para exibir colunas adicionais na estrutura de mineração que não foram incluídas no próprio modelo de mineração.  
  
##  <a name="bkmk_ContentDataType"></a> Como especificar tipo de conteúdo e tipo de dados  
 O tipo de dados é quase o mesmo que os especificados no SQL Server ou outras interfaces de aplicativo: datas e horas, números de tamanhos diferentes, valores Boolianos, texto e outros dados discretos.  
  
 Porém, os tipos de conteúdo são importantes para a mineração de dados e afetam o resultado da análise. O tipo de conteúdo informa ao algoritmo o que ele deve fazer com os dados: os números devem ser tratados em uma escala contínua ou guardados? Quantos valores potenciais estão lá? Cada valor é distinto? Se o valor for uma chave, que tipo de chave é que ele --indica um valor de data/hora, uma sequência ou algum outro tipo de chave?  
  
 Observe que a escolha do tipo de dados pode limitar sua escolha de tipos de conteúdo. Por exemplo, você não pode discretizar valores que não são numéricos. Se você não puder ver o tipo de conteúdo que deseja, clique em **Voltar** para retornar à página de tipo de dados e tente um tipo de dados diferente.  
  
 Você não precisa se preocupar muito sobre obter o tipo de conteúdo errado. É muito fácil criar um novo modelo e alterar o tipo de conteúdo dentro do modelo, contanto que o novo tipo de conteúdo tenha suporte pelo conjunto de tipo de dados na estrutura de mineração. Também é muito comum criar vários modelos usando tipos de conteúdo diferentes, como uma experiência ou para atender a requisitos de um algoritmo diferente.  
  
 Por exemplo, se seus dados contiverem uma coluna de renda, você poderá criar dois modelos diferentes ao usar o algoritmo de Árvores de Decisão da Microsoft e configurar a coluna alternadamente como números contínuos ou intervalos discretos. Porém, se você adicionou um modelo usando o algoritmo Naïve Bayes da Microsoft, você pode ser forçado a alterar somente a coluna para valores discretos, porque esse algoritmo não dá suporte a números contínuos.  
  
##  <a name="bkmk_Holdout"></a> Por que e como dividir dados em conjuntos de treinamento e teste  
 No final do assistente, você deve decidir se deseja dividir seus dados em conjuntos de treinamento e teste. A habilidade de provisionar uma parte dos dados escolhida aleatoriamente para teste é muito conveniente, porque garante que um conjunto de dados consistente de teste esteja disponível para uso com todos os modelos de mineração associados à nova estrutura de mineração.  
  
> [!WARNING]  
>  Observe que essa opção não está disponível para todos os tipos de modelo. Por exemplo, se você criar um modelo de previsão, você não conseguirá usar o controle, porque o algoritmo de série temporal não requer que haja nenhum intervalo nos dados. Para obter uma lista dos tipos de modelo que oferecem suporte a conjuntos de dados de controle, consulte [Conjuntos de dados de teste e treinamento](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
 Para criar este conjunto de dados de controle, você especifica o percentual dos dados que deseja usar para teste. Todos os dados restantes serão usados para treinamento. Opcionalmente, você pode definir um número máximo de casos para usar para teste ou definir um valor de semente para usar no início do processo de seleção aleatório.  
  
 A definição do conjunto de teste de controle é armazenada junto com a estrutura de mineração, de modo que sempre que você cria um novo modelo baseado na estrutura, o conjunto de dados de teste estará disponível para avaliar a precisão do modelo. Se você excluir o cache da estrutura de mineração, as informações sobre quais casos foram usados para treinamento e quais foram usados para teste também serão excluídas.  
  
##  <a name="BKMK_DrillThru"></a> Por que e como habilitar detalhamento  
 Quase no final do assistente, você tem a opção de habilitar *detalhamento*. É fácil perder esta opção, mas é importante. O detalhamento permite que você exiba dados de origem na estrutura de mineração, consultando o modelo de mineração.  
  
 Por que isso é útil? Suponha que você esteja exibindo os resultados de um modelo de clustering e queira ver os clientes que foram colocados em um cluster específico. Usando detalhamento, você pode exibir detalhes como informações de contato.  
  
> [!WARNING]  
>  Para usar o detalhamento, você deve habilitá-lo quando você cria a estrutura de mineração. Você pode habilitar o detalhamento em modelos posteriormente, definindo uma propriedade no modelo, mas as estruturas de mineração exigem que esta opção seja definida no início. Para obter mais informações, consulte [Consultas de detalhamento &#40;Mineração de dados&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
## <a name="see-also"></a>Consulte também  
 [Designer de Mineração de Dados](../../analysis-services/data-mining/data-mining-designer.md)   
 [Assistente de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)   
 [Propriedades do modelo de mineração](../../analysis-services/data-mining/mining-model-properties.md)   
 [Propriedades para estruturas de mineração e colunas de estrutura](../../analysis-services/data-mining/properties-for-mining-structure-and-structure-columns.md)   
 [Tarefas e instruções da estrutura de mineração](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
