---
title: "Assistente de mineração de dados (Analysis Services – mineração de dados) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], data mining
- OLAP [Analysis Services], mining models
- Data Mining Wizard
- relational mining models [Analysis Services]
ms.assetid: d5fea90f-5f38-4639-8851-7707f6606a12
caps.latest.revision: "57"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ffd9987c39cdffda3052ed075cb3abb137e4d1b2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-wizard-analysis-services---data-mining"></a>Assistente de Mineração de Dados (Analysis Services - Mineração de dados)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]O Assistente de mineração de dados no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] iniciado toda vez que você adicionar uma nova estrutura de mineração para um projeto de mineração de dados. O assistente ajuda a escolher uma fonte de dados e configurar uma exibição da fonte de dados que define os dados a serem usados para análise e, em seguida, ajuda a criar um modelo inicial.  
  
 Na fase final do assistente, você pode dividir seus dados opcionalmente em conjuntos de treinamento e teste, e habilitar recursos como detalhamento.  
  
## <a name="what-to-know-before-you-start"></a>O que você deve conhecer antes de iniciar  
 Veja agora o que você precisa saber antes de iniciar o assistente.  
  
-   Você criará a estrutura e os modelos de mineração de dados a partir de um banco de dados relacional ou a partir de um cubo existente em um banco de dados OLAP?  
  
-   Quais colunas contêm as chaves que identificam exclusivamente um registro de caso?  
  
-   Quais colunas ou atributos você deseja usar para previsão? Quais colunas ou atributos são bons para usar como entrada para análise?  
  
-   Qual algoritmo você deve usar? Todos os algoritmos fornecidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] têm características diferentes e produzem resultados diferentes. Felizmente, você não está limitado a um modelo para cada conjunto de dados. Portanto, fique à vontade para experimentar adicionando modelos diferentes.  
  
-   Você precisa ser capaz de testar seus modelos em um conjunto de dados unificado? Nesse caso, use a opção para separar alguns dados para teste. Você pode escolher um percentual e limitar um número especificado de linhas, se desejar.  
  
##  <a name="BKMK_Using_DM_Wizard"></a> Iniciando o Assistente de Mineração de Dados  
 Para usar o Assistente de Data Mining, você deverá ter aberto uma solução no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] que contém pelo menos um projeto de mineração de dados ou OLAP.  
  
-   Se sua solução estiver pronta para mineração de dados, basta clicar com o botão direito do mouse no nó **Estruturas de Mineração** no Gerenciador de Soluções e selecionar **Nova Estrutura de Mineração** para iniciar o assistente.  
  
-   Se sua solução não contiver nenhum projeto existente, você poderá adicionar um novo projeto de mineração de dados. No menu **Arquivo** , selecione **Novo**e **Projeto**. Verifique se você escolheu o modelo **Projeto Multidimensional e de Data Mining do Analysis Services**.  
  
-   Você também pode usar o Assistente de Importação do Analysis Services para obter metadados de uma solução de mineração de dados existente. No entanto, você não pode selecionar os objetos individuais para importar; o banco de dados inteiro é importado, incluindo cubos, exibições da fonte de dados etc. Observe também que a nova solução que é criada pela importação é configurada automaticamente para usar o banco de dados padrão local. Você pode precisar alterar isto para outra instância antes de poder processar ou procurar os objetos. E, se estiver importando de uma versão anterior do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], pode precisar atualizar as referências a provedores.  
  
 Em seguida, você criará a estrutura de mineração e um modelo de mineração de dados associado. Você também pode criar apenas a estrutura de mineração e adicionar modelos posteriormente, mas é geralmente mais fácil criar um modelo de teste primeiro.  
  
###  <a name="BKMK_Relational"></a>Relacional versus Modelos de mineração OLAP  
 A próxima opção importante que você tem é se deseja usar uma fonte de dados relacional ou basear seu modelo em dados multidimensionais (OLAP).  
  
 O Assistente de Mineração de Dados é ramificado em dois caminhos nesse momento, dependendo se sua fonte de dados é relacional ou em um cubo. Todo o restante exceto o processo de seleção de dados é o mesmo — a escolha do algoritmo, a capacidade para adicionar um conjunto de dados de controle, etc — mas selecionar dados de cubo é um pouco mais complexo que usar dados relacionais. (Você também obterá algumas opções adicionais no final se criar um modelo baseado em um cubo.)  
  
 Consulte os tópicos a seguir para obter um passo a passo de cada opção com mais detalhes:  
  
 [Criar uma estrutura de mineração relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 Orienta você pelas decisões feitas ao criar um modelo de mineração de dados relacional.  
  
 [Criar uma estrutura de mineração OLAP](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 Descreve as opções adicionais e as seleções a serem feitas ao escolher dados de um cubo OLAP.  
  
> [!NOTE]  
>  Você não precisa ter um cubo ou um banco de dados OLAP para fazer mineração de dados. A menos que seus dados já estejam armazenados em um cubo ou você queira explorar dimensões OLAP ou resultados de cálculos ou agregações OLAP, recomendamos que você use uma fonte de dados ou tabela relacional para mineração de dados.  
  
### <a name="choosing-an-algorithm"></a>Escolhendo um algoritmo  
 Em seguida, você deve decidir sobre qual algoritmo deve ser usado ao processar seus dados. Esta decisão pode ser difícil de tomar. Cada algoritmo fornecido no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem recursos diferentes e gera resultados diferentes, de modo que você pode experimentar vários modelos diferentes antes de determinar qual é o mais apropriado para seus dados e seu problema comercial. Consulte o tópico a seguir para obter uma explicação das tarefas para as quais cada algoritmo é mais apropriado:  
  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 Novamente, é possível criar vários modelos usando algoritmos diferentes ou modificar parâmetros para que os algoritmos criem modelos diferentes. Você não está bloqueado em sua escolha de algoritmo, e é prática recomendada criar vários modelos diferentes nos mesmos dados.  
  
### <a name="define-the-data-used-for-modeling"></a>Definir os dados usados para modelagem  
 Além de escolher os dados de uma origem, você deverá especificar qual tabela na exibição da fonte de dados contém os *dados de caso*. A tabela de casos será usada para treinar o modelo de mineração de dados e, dessa forma, deve conter as entidades que você quer analisar: por exemplo, clientes e as respectivas informações demográficas. Cada caso deve ser exclusivo e identificado por uma *chave do caso*.  
  
 Além de especificar a tabela de casos, você pode incluir *tabelas aninhadas* em seus dados. Uma tabela aninhada normalmente contém informações adicionais sobre as entidades da tabela de casos, como as transações conduzidas pelo cliente ou os atributos que têm um relacionamento muitos para um com a entidade. Por exemplo, uma tabela aninhada unida à tabela de casos de **Clientes** pode incluir uma lista de produtos adquiridos por cada cliente. Em um modelo que analisa o tráfego para um site, a tabela aninhada pode incluir as sequências de páginas que o usuário visitou. Para obter mais informações, consulte [Tabelas aninhadas &#40;Analysis Services – Mineração de dados&#41;](../../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
### <a name="additional-features"></a>Recursos Adicionais  
 Para ajudá-lo a escolher os dados certos, e configurar as fontes de dados corretamente, o Assistente de Mineração de Dados fornece estes recursos adicionais:  
  
-   **Automático – detecção de tipos de dados**: o assistente examinará a exclusividade e a distribuição de valores de coluna, recomendará o melhor tipo de dados e sugerirá um tipo de uso para obter os dados. Você pode substituir estas sugestões selecionando valores de uma lista.  
  
-   **Sugestões para variáveis**: você pode clicar em uma caixa de diálogo e iniciar um analisador que calcula as correlações nas colunas incluídas no modelo e determina se alguma coluna é uma previsão provável do atributo de resultado, considerando a configuração do modelo até então. Você pode substituir estas sugestões digitando valores diferentes.  
  
-   **Seleção de recursos**: a maioria dos algoritmos detectará automaticamente as colunas que são boas previsões e as usará preferencialmente. Nas colunas que contêm muitos valores, a *seleção de recursos* será aplicada para reduzir a cardinalidade dos dados e melhorar as chances de localizar um padrão significativo. Você pode afetar o comportamento da seleção de recursos usando parâmetros modelo.  
  
-   **Divisão automática do cubo**: se seu modelo de mineração for baseado em uma fonte de dados OLAP, a capacidade de segmentar o modelo usando atributos de cubo será fornecida automaticamente. Isto é útil para criar modelos com base em subconjuntos de dados de cubo.  
  
### <a name="completing-the-wizard"></a>Concluindo o assistente  
 A última etapa no assistente é nomear a estrutura de mineração e o modelo de mineração associado. Dependendo do tipo de modelo que você criou, também poderá ter as opções importantes a seguir:  
  
-   Se você selecionar **Permitir drillthrough**, a capacidade de *drillthrough* estará habilitada no modelo. Com o detalhamento, os usuários que têm permissões apropriadas podem explorar os dados de origem que são usados para criar o modelo.  
  
-   Se você estiver criando um modelo OLAP, poderá selecionar as opções **Criar um novo cubo de mineração de dados**ou **Criar uma dimensão de mineração de dados**. Ambas as opções facilitam a procura do modelo concluído e a análise dos dados subjacentes.  
  
 Após concluir o Assistente de Mineração de Dados, utilize o Designer de Mineração de Dados para modificar a estrutura de mineração e os modelos para exibir a precisão do modelo, as características da estrutura e dos modelos ou fazer previsões utilizando os modelos.  
  
 [Voltar ao Início](#BKMK_Using_DM_Wizard)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Para saber mais sobre as decisões que você precisa tomar ao criar um modelo de mineração de dados, consulte os links a seguir:  
  
 [Algoritmos de mineração de dados &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
 [Tipos de conteúdo &#40;Data Mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)  
  
 [Tipos de dados &#40;Mineração de dados&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
 [Seleção de recursos &#40;Mineração de dados&#41;](../../analysis-services/data-mining/feature-selection-data-mining.md)  
  
 [Valores ausentes &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)  
  
 [Detalhamento em modelos de mineração](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas de mineração de dados](../../analysis-services/data-mining/data-mining-tools.md)   
 [Soluções de mineração de dados](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
