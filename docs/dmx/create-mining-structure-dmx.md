---
title: CRIAR ESTRUTURA DE MINERAÇÃO (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b27f9e1c5927392b4ea221dcb6b7468a42ff9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892820"
---
# <a name="create-mining-structure-dmx"></a>CRIAR UMA ESTRUTURA DE MINERAÇÃO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cria uma nova estrutura de mineração em um banco de dados e define, opcionalmente, as partições de treinamento e de teste. Depois de criar a estrutura de mineração, você pode usar a instrução [ALTER MINING structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) para adicionar modelos à estrutura de mineração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>Argumentos  
 *estruturá*  
 Um nome exclusivo para a estrutura.  
  
 *lista de definições de coluna*  
 Uma lista de definições de coluna separadas por vírgulas.  
  
 *controle de MaxPercent*  
 Um número inteiro entre 1 e 100 que indica a porcentagem de dados separados para teste.  
  
 *controle de MaxCases*  
 Um número inteiro que indica o número de máximo de casos usados para teste.  
  
 Se o valor especificado para o máximo de casos for maior que o número de casos de entrada, todos os casos de entrada serão usados para teste e um aviso será emitido.  
  
> [!NOTE]  
>  Se a porcentagem e o número máximo de casos forem especificados, o menor dos dois limites será usado.  
  
 *semente de controle*  
 Um número inteiro usado como a semente para iniciar o particionamento de dados.  
  
 Se definido como 0, o hash da ID da estrutura de mineração será usada como a semente.  
  
> [!NOTE]  
>  Você deve especificar uma semente se precisar garantir que uma partição pode ser reproduzida.  
  
 Padrão: REPETÍVEL(0)  
  
## <a name="remarks"></a>Comentários  
 Uma estrutura de mineração é definida especificando uma lista de colunas, especificando, opcionalmente, as relações de hierarquia entre as colunas e particionamento, opcionalmente, a estrutura de mineração em conjuntos de dados de treinamento e de teste.  
  
 A palavra-chave opcional SESSION indica que a estrutura é temporária e você pode usá-la somente durante a sessão atual. Quando a sessão terminar, a estrutura e os modelos baseados nela serão excluídos. Para criar estruturas e modelos de mineração temporários, você deve primeiro definir a propriedade de banco de dados, AllowSessionMiningModels. Para obter mais informações, consulte [Propriedades de Data Mining](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties).  
  
## <a name="column-definition-list"></a>Lista de definições de coluna  
 Uma estrutura de mineração é definida incluindo as seguintes informações para cada coluna na lista de definições da coluna:  
  
-   Nome (obrigatório)  
  
-   Tipo de dados (obrigatório)  
  
-   Distribuição  
  
-   Lista de sinalizadores de modelagem  
  
-   Tipo de conteúdo (obrigatório)  
  
-   Relação com uma coluna de atributo (obrigatório, apenas se aplicável), indicada pela cláusula RELATED TO (RELACIONADO A)  
  
 Use a seguinte sintaxe para obter a lista de definições de coluna para definir uma única coluna:  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 Use a seguinte sintaxe para obter a lista de definições de coluna para definir uma coluna de tabela aninhada:  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 Para obter uma lista dos tipos de dados, dos tipos de conteúdo, de distribuições de coluna e de sinalizadores de modelagem que podem ser usados para definir uma coluna de estrutura, consulte os seguintes tópicos:  
  
-   [Tipos de dados &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-types-data-mining)  
  
-   [Tipos de conteúdo &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)  
  
-   [Distribuições de colunas &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [Sinalizadores de modelagem &#40;Mineração de dados&#41;](https://docs.microsoft.com/analysis-services/data-mining/modeling-flags-data-mining)  
  
 Você pode definir vários valores de sinalizadores de modelagem para uma coluna. No entanto, é possível ter apenas um tipo de conteúdo e um tipo de dados para uma coluna.  
  
### <a name="column-relationships"></a>Relações de coluna  
 É possível adicionar uma cláusula a qualquer instrução de definição de coluna para descrever a relação entre duas colunas. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]dá suporte ao uso da seguinte \<cláusula de> de relação de coluna.  
  
 **RELACIONADO A**  
 Indica uma hierarquia de valor. O destino de uma coluna RELATED TO pode ser a coluna de chave em uma tabela aninhada, uma coluna com um valor discreto na linha de caso ou outra coluna com uma cláusula RELATED TO, que indica uma hierarquia mais profunda.  
  
## <a name="holdout-parameters"></a>Parâmetros de validação  
 Ao especificar parâmetros de validação, você cria uma partição dos dados da estrutura. A quantidade especificada para validação é reservada para teste e os dados restantes são usados para treinamento. Por padrão, se você criar uma estrutura de mineração usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], uma partição de validação será criada contendo 30 por cento dos dados de teste e 70 por cento dos dados de treinamento. Para obter mais informações, consulte [Training and Testing Data Sets](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets).  
  
 Se você criar uma estrutura de mineração usando DMX (Data Mining Extensions), deverá especificar manualmente a criação de uma partição de validação.  
  
> [!NOTE]  
>  A instrução **ALTER MINING STRUCTURE** não dá suporte a controle.  
  
 É possível especificar até três parâmetros de validação. Se você especificar um número máximo de casos de validação e uma porcentagem de validação, uma porcentagem de casos são reservados até o limite máximo de casos ser atingido. Você especifica a porcentagem de controle como um inteiro seguido pela palavra-chave **percent** e especifica o número máximo de casos como um inteiro seguido pela palavra-chave **cases** . É possível combinar as condições em qualquer ordem, como mostra os exemplos a seguir:  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 A semente de validação controla o ponto de início do processo que atribui casos aleatoriamente aos conjuntos de dados de treinamento ou de teste. Ao definir uma semente de validação, é possível assegurar que a partição pode ser repetida. Se você não especificar uma semente de validação, o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará o nome da estrutura de mineração para criar uma semente. Se você renomear a estrutura, o valor de semente mudará. O parâmetro da semente de validação pode ser usado com ambos os outros parâmetros de avaliação.  
  
> [!NOTE]  
>  Como as informações de partição são armazenadas em cache com os dados de treinamento, para usar o controle, você deve garantir que a propriedade **CacheMode** da estrutura de mineração esteja definida como **KeepTrainingData**. Esta é a configuração padrão no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para novas estruturas de mineração. Alterar a propriedade **CacheMode** para **ClearTrainingCases** em uma estrutura de mineração existente que contém uma partição de controle não afetará nenhum modelo de mineração que tenha sido processado. No entanto <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> , se não estiver definido como **KeepTrainingData**, os parâmetros de validação não terão nenhum efeito. Isto significa que todos os dados de origem serão usados para treinamento e nenhum conjunto de testes estará disponível. A definição da partição é armazenada em cache com a estrutura; se você limpar o cache dos casos de treinamento, também limpará o cache dos dados de teste e a definição do conjunto de validação.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos seguintes demonstram como criar uma estrutura de mineração com validação usando DMX.  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>Exemplo 1: Adicionando uma estrutura sem conjunto de treinamentos  
 O seguinte exemplo cria uma estrutura de mineração chamada `New Mailing` sem criar nenhum modelo de mineração associado e sem usar a validação. Para saber como adicionar um modelo de mineração à estrutura, consulte [ALTER MINING structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>Exemplo 2: Especificando a porcentagem e semente de validação  
 A cláusula a seguir pode ser adicionada após a lista de definições de coluna para definir um conjunto de dados que pode ser usado para testar todos os modelos de mineração associados à estrutura de mineração. A instrução criará um conjunto de teste com 25% do total de casos de entrada, sem um limite no número máximo de casos. 5000 é usado como a semente para criação da partição. Quando você especifica uma semente, os mesmos casos são escolhidos para o conjunto de teste cada vez que a estrutura de mineração é processada, desde que os dados subjacentes não sejam alterados.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>Exemplo 3: Especificando a porcentagem e máximo de casos de validação  
 A seguinte cláusula criará um conjunto de testes que contém 25 por cento dos casos de entrada totais ou 2000 casos, qualquer que seja o menor. Como 0 é especificado como a semente, o nome da estrutura de mineração é usada para criar a semente que é usada para começar o exemplo de casos de entrada.  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#40;&#41; instruções de definição de dados DMX de extensões de mineração de dados](../dmx/dmx-statements-data-definition.md)   
 [&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)   
 [Referência de instruções de DMX &#40extensões de Mineração de Dados&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
