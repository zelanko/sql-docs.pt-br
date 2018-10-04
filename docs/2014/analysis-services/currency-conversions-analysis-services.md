---
title: Conversões de moeda (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple currency conversions
- monetary data [SQL Server]
- currency [Analysis Services]
- converting currency
- one-to-many currency conversions
- many-to-many currency conversions [Analysis Services]
- many-to-one currency conversions [Analysis Services]
ms.assetid: e03f491c-7df8-46a0-ade9-f2e55b68db85
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14ae3f58a8cfdef4dfde4d30e969e4386bd1dbc0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190835"
---
# <a name="currency-conversions-analysis-services"></a>Conversões de moeda (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  Somente multidimensional  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa uma combinação de recursos, orientada por scripts de linguagem Multidimensional Expressions (MDX), para dar suporte em conversão de moedas, em cubos, com suporte para várias moedas.  
  
## <a name="currency-conversion-terminology"></a>Terminologia de conversão de moedas  
 A seguinte terminologia é usada no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para descrever a funcionalidade de conversão de moedas:  
  
 Moeda corrente  
 A moeda em relação à qual as taxas de câmbio são inseridas no grupo de medidas de taxa.  
  
 Moeda local  
 A moeda usada para armazenar transações sobre quais as medidas a serem convertidas se baseiam.  
  
 A moeda local a ser identificada ou:  
  
-   Um identificador de moeda na tabela de fatos armazenado com a transação, como é geralmente o caso com aplicativos de serviços bancários, onde a própria transação identifica a moeda usada para a transação.  
  
-   Um identificador de moeda associado a um atributo em uma tabela de dimensões que está então associada a uma transação na tabela de fatos, como é geralmente o caso em aplicativos financeiros em que um local ou outro identificador, uma subsidiária, identifica a moeda usada por uma transação associada.  
  
 Moeda de relatório  
 A moeda na qual são convertidas transações da moeda corrente.  
  
> [!NOTE]  
>  Para conversões de moeda muitos para um, a moeda corrente e moeda de relatório são iguais.  
  
 Dimensão de moeda  
 Uma dimensão de banco de dados definida com as seguintes configurações:  
  
-   O `Type` propriedade da dimensão é definida como moeda.  
  
-   A propriedade `Type` de um atributo para a dimensão é definida como CurrencyName.  
  
    > [!IMPORTANT]  
    >  Os valores desse atributo devem ser usados em todas as colunas que contenham um identificador de moeda.  
  
 Grupo de medidas de taxa  
 Um grupo de medidas em um cubo, definido com as seguintes configurações:  
  
-   Existe uma relação de dimensão regular entre uma dimensão de moeda e o grupo de medidas de taxa.  
  
-   Existe uma relação de dimensão regular entre uma dimensão tempo e o grupo de medidas de taxa.  
  
-   Além disso, a propriedade `Type` é definida como ExchangeRate. Enquanto o Assistente de Business Intelligence usa as relações com as dimensões de tempo e moeda para identificar grupos de medidas de taxa de probabilidade, definindo o `Type` propriedade para ExchangeRate permite que aplicativos cliente identifiquem mais facilmente a medida de taxa grupos.  
  
-   Uma ou mais medidas, representando as taxas de câmbio contidas pelo grupo de medidas de taxa.  
  
 Dimensão de moeda de relatório  
 A dimensão, definida pelo Assistente de Business Intelligence depois que uma conversão de moeda é definida e que contém as moedas de relatório para essa conversão de moedas. A dimensão de moeda de relatório baseia-se em uma consulta nomeada e definida na exibição da fonte de dados, na qual a dimensão de moeda associada ao grupo de medidas de taxa tem base, a partir da tabela de dimensões principal da dimensão de moeda. A dimensão está definida com as seguintes configurações:  
  
-   O `Type` propriedade da dimensão é definida como moeda.  
  
-   O `Type` propriedade do atributo de chave para a dimensão é definida como CurrencyName.  
  
-   O `Type` propriedade de um atributo na dimensão é definida como CurrencyDestination e a coluna vinculada ao atributo contém os identificadores de moeda que representam as moedas de relatório para a conversão de moeda.  
  
## <a name="defining-currency-conversions"></a>Definindo conversões de moeda  
 Você pode usar o Assistente de Business Intelligence para definir a funcionalidade de conversão de moeda de um cubo ou pode definir manualmente as conversões de moeda usando scripts MDX.  
  
### <a name="prerequisites"></a>Prerequisites  
 Antes de você poder definir uma conversão de moedas em um cubo, usando o Assistente de Business Intelligence, será necessário definir, primeiro, pelo menos uma dimensão de moeda, uma dimensão temporal e, pelo menos, um grupo de medidas de taxa. A partir desses objetos, o Assistente de Business Intelligence pode recuperar os dados e os metadados usados para criar a dimensão de moeda de relatório e script MDX que são necessários para fornecer a funcionalidade de conversão de moedas.  
  
### <a name="decisions"></a>Decisões  
 Você precisa tomar as seguintes decisões, antes que o Assistente de Business Intelligence possa criar a dimensão de moeda de relatório e o script MDX que são necessários para fornecer a funcionalidade de conversão de moedas.  
  
-   Direção da taxa de câmbio  
  
-   Membros convertidos  
  
-   Tipo de conversão  
  
-   Moedas locais  
  
-   Moedas de relatório  
  
### <a name="exchange-rate-directions"></a>Direções da taxa de câmbio  
 O grupo de medidas de taxa contém medidas representando taxas de câmbio entre moedas locais e a moeda corrente (geralmente mencionada como moeda corporativa). A combinação de direção de taxa de câmbio e tipo de conversão determina a operação executada em medidas a serem convertidas por um script MDX gerado, usando o Assistente de Business Intelligence. A seguinte tabela descreve as operações executadas, dependendo da direção da taxa de câmbio e do tipo de conversão, com base nas opções de direção da taxa de câmbio e de direções de conversão, que são disponíveis no Assistente de Business Intelligence.  
  
|||||  
|-|-|-|-|  
|Direção da taxa de câmbio|**Muitos para um**|**Um para muitos**|**Muitos para muitos**|  
|**n moeda corrente em 1 moeda de amostra**|Multiplique a medida a ser convertida pela medida de taxa de câmbio para a moeda local para converter a medida em uma moeda corrente.|Divida a medida a ser convertida pela medida da taxa de câmbio da moeda de relatório para converter a medida em uma moeda de relatório.|Multiplique a medida a ser convertida pela medida de taxa de câmbio para a moeda local para converter a medida na moeda corrente, então, divida a medida convertida pela medida de taxa de câmbio para a moeda de relatório para converter a medida na moeda de relatório.|  
|**n moeda de amostra em 1 moeda corrente**|Divida a medida a ser convertida pela medida de taxa de cambo para a moeda local para converter a medida na moeda corrente.|Multiplique a medida a ser convertida pela medida de taxa de câmbio para a moeda de relatório para converter a medida na moeda de relatório.|Divida a medida a ser convertida pela medida de taxa de câmbio para a moeda local para converter a medida na moeda corrente, então, multiplique a medida convertida pela medida de taxa de câmbio para a moeda de relatório para converter a medida na moeda de relatório.|  
  
 Você escolhe a direção de taxa de câmbio na página **Definir opções de conversão de moeda** do Assistente de Business Intelligence. Para obter mais informações sobre a direção de conversão de configuração, consulte [Definir opções de conversão de moeda &#40;Assistente de Business Intelligence&#41;](set-currency-conversion-options-business-intelligence-wizard.md).  
  
### <a name="converted-members"></a>Membros convertidos  
 Você pode usar o Assistente de Business Intelligence para especificar quais medidas do grupo de medidas de taxa são usadas para converter valores para:  
  
-   Medidas em outros grupos de medidas.  
  
-   Membros de uma hierarquia de atributos para um atributo de conta em uma dimensão de banco de dados.  
  
-   Tipos de conta, usados por membros de uma hierarquia de atributo para um atributo de conta em uma dimensão de banco de dados.  
  
 O Assistente de Business Intelligence usa essas informações no script MDX geradas pelo assistente para determinar o escopo do cálculo de conversão de moedas. Para obter mais informações sobre como especificar membros para conversão de moedas, consulte [Selecionar membros &#40;Assistente de Business Intelligence&#41;](select-members-business-intelligence-wizard.md).  
  
### <a name="conversion-types"></a>Tipos de conversão  
 O Assistente de Business Intelligence oferece suporte para três tipos diferentes de conversão de moedas:  
  
-   **Um para muitos**  
  
     As transações são armazenadas na tabela de fatos na moeda corrente e, então, convertidas em uma ou mais moedas de relatório.  
  
     Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em USD. Esse tipo de conversão converte essas transações da moeda corrente nas moedas de relatório especificadas. Como resultado, essas transações podem ser armazenadas na moeda corrente especificada e exibidas na moeda corrente especificada, ou em qualquer uma das moedas de relatório especificadas na dimensão de moeda de relatório para a conversão de moeda.  
  
-   **Muitos para um**  
  
     As transações são armazenadas na tabela de fatos em moedas locais e, então, convertidas na moeda corrente. A moeda corrente funciona como a única moeda de relatório especificada na dimensão de moeda de relatório.  
  
     Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em EUR (euros), AUD (dólares australianos) e MXN (pesos mexicanos). Esse tipo de conversão converte essas transações das moedas locais especificadas para a moeda corrente. O resultado é que essas transações podem ser armazenadas nas moedas locais especificadas e exibidas na moeda corrente, que é especificada na dimensão de moeda de relatório definida para a conversão de moedas.  
  
-   **Muitos para muitos**  
  
     As transações são armazenadas na tabela de fatos em moedas locais. A funcionalidade de conversão de moedas converte essas transações na moeda corrente e, então, em uma ou mais moedas de relatório.  
  
     Por exemplo, a moeda corrente pode estar definida como USD (dólares dos EUA) e a tabela de fatos armazenar transações em EUR (euros), AUD (dólares australianos) e MXN (pesos mexicanos). Esse tipo de conversão converte essas transações das moedas locais especificadas na moeda corrente e, em seguida, as transações são convertidas novamente da moeda corrente na moeda de relatório especificada. Como resultado, essas transações podem ser armazenadas nas moedas locais especificadas e exibidas na moeda corrente especificada, ou em qualquer uma das moedas de relatório especificadas na dimensão de moeda de relatório para a conversão de moedas.  
  
 Especificar o tipo de conversão permite que o Assistente de Business Intelligence defina a consulta nomeada e a estrutura da dimensão de moeda de relatório, assim como a estrutura do script MDX definido para a conversão de moedas.  
  
### <a name="local-currencies"></a>Moedas locais  
 Se você escolher um tipo de conversão muitos para muitos, ou muitos para um, para sua conversão de moedas, será necessário especificar como identificar as moedas locais a partir das quais o script MDX gerado pelo Assistente de Business Intelligence executará os cálculos de conversão de moedas. A moeda local para uma transação em uma tabela de fatos pode ser identificada por um de dois modos:  
  
-   O grupo de medidas contém uma relação de dimensão regular com a dimensão de moeda. Por exemplo, no banco de dados de exemplo [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o grupo de medidas Vendas pela Internet tem uma relação regular de dimensão com a dimensão Moeda. A tabela de fatos desse grupo de medidas contém uma coluna de chave estrangeira que faz referência aos identificadores de moedas na tabela de dimensões daquela dimensão. Nesse caso, você pode selecionar o atributo da dimensão de moeda referenciada pelo grupo de medidas para identificar a moeda local para transações na tabela de fatos desse grupo de medidas. Essa situação acontece mais frequentemente em aplicativos de serviços bancários, onde a própria transação determina a moeda usada na transação.  
  
-   O grupo de medidas contém uma relação de dimensão referenciada com a dimensão de moeda, por meio de outra dimensão que referencia diretamente a dimensão de moeda. Por exemplo, no banco de dados de exemplo [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o grupo de medidas Relatórios Financeiros tem uma relação de dimensão referenciada com a dimensão Moeda por meio da dimensão Organização. A tabela de fatos para esse grupo de medidas contém uma coluna de chave estrangeira que referencia membros na tabela de dimensões da dimensão Organização. A tabela de dimensões da dimensão Organização, por sua vez, contém uma coluna de chave estrangeira que faz referência aos identificadores de moedas na tabela de dimensões Moeda. Essa situação acontece com mais frequência em aplicativos de relatórios financeiros onde o local ou a subsidiária de uma transação determina a moeda da transação. Nesse caso, você pode selecionar o atributo que referencia a dimensão de moeda a partir da dimensão para a entidade empresarial.  
  
### <a name="reporting-currencies"></a>Moedas de relatório  
 Se você escolher um tipo de conversão muitos para muitos, ou um para muitos, para sua conversão de moedas, será necessário especificar as moedas de relatório para as quais o script MDX gerado pelo Assistente de Business Intelligence executará os cálculos de conversão de moedas. Você pode especificar todos os membros da dimensão de moeda relacionada ao grupo de medidas de taxa ou selecionar membros individuais da dimensão.  
  
 O Assistente de Business Intelligence cria uma dimensão de moeda de relatório, com base em uma consulta nomeada criada a partir da tabela de dimensões para a dimensão de moeda, usando as moedas de relatório selecionadas.  
  
> [!NOTE]  
>  Se você selecionar o tipo de conversão de um para muitos, uma dimensão de moeda de relatório também será criada. A dimensão contém apenas um membro representando a moeda corrente, pois a moeda corrente é também usada como a moeda de relatório de uma conversão de moedas uma para muitos.  
  
 Uma dimensão de moeda de relatório separada está definida para cada conversão de moeda definida em um cubo. Você pode alterar o nome das dimensões de moeda de relatório após a criação, mas se você fizer isso será necessário também atualizar o script MDX gerado pela conversão de moedas para assegurar que o nome correto seja usado pelo comando de script ao referenciar a dimensão de moeda de relatório.  
  
## <a name="defining-multiple-currency-conversions"></a>Definindo várias conversões de moedas  
 Usando o Assistente de Business Intelligence, você pode definir a quantidade de conversões de moedas conforme for necessário para sua solução de Business Intelligence. Você pode substituir uma conversão de moedas existente ou anexar uma nova conversão de moedas ao script MDX de um cubo. Várias conversões de moedas definidas em um único cubo fornecem flexibilidade nos aplicativos de Business Intelligence que têm requisitos de relatórios complexos, como aplicativos de relatórios financeiros com suporte aos vários requisitos de conversão separados para relatórios internacionais.  
  
### <a name="identifying-currency-conversions"></a>Identificando conversões de moedas  
 O Assistente de Business Intelligence identifica cada conversão de moeda enquadrando os comandos de script para a conversão de moedas nos seguintes comentários:  
  
 `//<Currency conversion>`  
  
 `...`  
  
 `[MDX statements for the currency conversion]`  
  
 `...`  
  
 `//</Currency conversion>`  
  
 Se você alterar ou remover esses comentários, o Assistente de Business Intelligence não poderá detectar a conversão de moedas, e por isso, você não deve alterar esses comentários.  
  
 O assistente também armazena metadados em comentários com esses comentários, incluindo a data e hora de criação, o usuário e o tipo de conversão. Esses comentários não devem ser alterados, pois o Assistente de Business Intelligence usa esses metadados ao exibir conversões de moeda existentes.  
  
 Você pode alterar os comandos de script contidos em uma conversão de moeda conforme necessário. Se você substituir a conversão de moedas, porém, suas alterações serão perdidas.  
  
## <a name="see-also"></a>Consulte também  
 [Cenários de globalização para Analysis Services multidimensional](globalization-scenarios-for-analysis-services-multiidimensional.md)  
  
  
