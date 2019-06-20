---
title: Adicionar modelos de mineração a uma estrutura (Analysis Services - mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], creating
- mining models [Analysis Services], creating
- mining models [Analysis Services], modifying
ms.assetid: a175daa5-58ea-474c-a82f-9648c5155dc8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd25682f12ce0a3ddad5e8f135d82aaf08115762
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086246"
---
# <a name="add-mining-models-to-a-structure-analysis-services---data-mining"></a>Adicionar modelos de mineração a uma estrutura (Analysis Services - Mineração de dados)
  Uma estrutura de mineração é destinada a dar suporte a diversos modelos de mineração. Portanto, após a finalização do assistente, você poderá abrir a estrutura e adicionar novos modelos de mineração. Cada vez que você cria um modelo, pode usar um algoritmo diferente, alterar os parâmetros ou aplicar filtros para usar com um subconjunto diferente dos dados.  
  
## <a name="adding-new-mining-models"></a>Adicionando novos modelos de mineração  
 Ao usar o Assistente de Mineração de Dados para criar um novo modelo de mineração, por padrão você deve sempre criar primeiro uma estrutura de mineração. O assistente em seguida dá a você a opção de adicionar um modelo de mineração inicial à estrutura. No entanto, não é necessário criar um modelo imediatamente. Se apenas a estrutura for criada, você não precisa tomar uma decisão sobre qual coluna deve ser usada como o atributo previsível ou sobre como usar os dados em um modelo específico. Em vez disso, configure a estrutura de dados geral que deseja usar no futuro e, posteriormente, use o [Designer de Mineração de Dados](data-mining-designer.md) para adicionar novos modelos de mineração baseados na estrutura.  
  
> [!NOTE]  
>  Em DMX, a instrução CREATE MINING MODEL começa com o modelo de mineração. Desse modo, você define sua escolha de modelo de mineração e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gera a estrutura subjacente automaticamente. Posteriormente, você pode continuar a adicionar novos modelos de mineração a essa estrutura, usando a instrução ALTER STRUCTURE... Instrução ADD MODEL.  
  
## <a name="choosing-an-algorithm"></a>Escolhendo um algoritmo  
 Ao adicionar um novo modelo a uma estrutura existente, a primeira coisa que você deve fazer é selecionar um algoritmo de mineração de dados a ser usado nesse modelo. Escolher o algoritmo é importante porque cada algoritmo executa um tipo diferente de análise e tem requisitos diferentes.  
  
 Quando você selecionar um algoritmo que é incompatível com seus dados, receberá um aviso. Em alguns casos, você pode precisar ignorar colunas que não podem ser processadas pelo algoritmo. Em outros casos, o algoritmo fará os ajustes automaticamente para você. Por exemplo, se sua estrutura contiver dados numéricos, e o algoritmo só puder funcionar com valores discretos, ela agrupará os valores numéricos em intervalos discretos para você. Em alguns casos, você pode precisar primeiro corrigir os dados manualmente, escolhendo uma chave ou um atributo previsível.  
  
 Você não precisa alterar o algoritmo ao criar um novo modelo. Geralmente você pode obter resultados muito diferentes usando o mesmo algoritmo, mas filtrando os dados ou alterando um parâmetro como o método de clustering ou o tamanho mínimo do conjunto de itens. É recomendável fazer experiências com diversos modelos para ver quais parâmetros produzem os melhores resultados.  
  
 Observe que todos os novos modelos precisam ser processados antes de você poder usá-los.  
  
## <a name="specifying-the-usage-of-columns-in-a-new-mining-model"></a>Especificando o uso de colunas em um novo modelo de mineração  
 Ao adicionar novos modelos de mineração para uma estrutura de mineração existente, você deverá especificar como cada coluna de dados deve ser usada pelo modelo. Dependendo do tipo de algoritmo que você escolher para o modelo, algumas destas escolhas podem ser feitas por padrão. Se você não especificar um tipo de uso para uma coluna, ela não será incluída na estrutura de mineração. Porém, os dados na coluna ainda poderão estar disponíveis para detalhamento, se o modelo suportá-lo.  
  
 As colunas da estrutura de mineração que são usadas pelo modelo (se não forem definidas para Ignorar) devem ser uma chave, uma coluna de entrada, uma coluna previsível ou uma coluna previsível dos valores dos quais também são usados como entradas para o modelo.  
  
-   Colunas de chave contêm um identificador exclusivo para cada linha em uma tabela. Alguns modelos de mineração, como aquele com base no cluster de sequência ou em algoritmos de série temporal, podem conter várias colunas de chave. Porém, estas chaves múltiplas não são chaves compostas no sentido relacional, mas devem ser selecionadas de modo a fornecer suporte para séries temporais e análise de clustering de sequências.  
  
-   As colunas de entrada fornecem as informações das quais as previsões são feitas. O Assistente de Mineração de Dados fornece o recurso **Sugerir** , que é habilitado quando você seleciona uma coluna previsível. Se você clicar neste botão, o assistente trará uma amostra dos valores previsíveis e determinará quais das outras colunas na estrutura produzirão boas variáveis. Ele rejeitará as colunas de chave ou outras colunas com muitos valores exclusivos e sugerirá colunas que parecem eatar correlacionadas com o resultado.  
  
     Este recurso é particularmente útil quando os conjuntos de dados contiverem mais colunas do que você realmente precisar para criar um modelo de mineração. O recurso **Sugerir** calcula uma pontuação numérica, de 0 a 1, que descreve o relacionamento entre cada coluna no conjunto de dados e a coluna previsível. Com base nesta pontuação, o recurso sugere quais colunas usar como entrada para o modelo de mineração. Ao usar o recurso **Sugerir** , você pode utilizar as colunas sugeridas, modificar as seleções de acordo com suas necessidades ou ignorar as sugestões.  
  
-   As colunas previsíveis contêm as informações que você tenta prever no modelo de mineração. Você pode selecionar várias colunas como os atributos previsíveis. Os modelos de clustering são a exceção na qual um atributo previsível é opcional.  
  
     Dependendo do tipo do modelo, a coluna previsível pode precisar ser um tipo de dados específico: por exemplo, um modelo de regressão linear exige uma coluna numérica como o valor previsto; o algoritmo de Naïve Bayes exige um valor discreto (e todas as entradas também devem ser discretas).  
  
## <a name="specifying-column-content"></a>Especificando o conteúdo da coluna  
 Para algumas colunas, talvez seja necessário especificar o *conteúdo da coluna*também. Na mineração de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a propriedade Tipo de Conteúdo de cada coluna de dados informa como o algoritmo deve processar os dados da coluna. Por exemplo, se seus dados tiverem uma coluna Receita, você deve especificar que a coluna contém números contínuos definindo o tipo de conteúdo como Contínuo. No entanto, também é possível especificar que os números da coluna Receita sejam agrupados em blocos definindo o tipo de conteúdo como Diferenciado e, opcionalmente, especificando o número exato de blocos. Você pode criar modelos que manipulam colunas de modos diferentes; por exemplo, é possível criar um modelo que agrupa clientes em três faixas etárias e outro modelo que agrupa clientes em 10 faixas etárias.  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas de Mineração &#40;Analysis Services – Data Mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Criar uma estrutura de mineração relacional](create-a-relational-mining-structure.md)   
 [Propriedades do modelo de mineração](mining-model-properties.md)   
 [Colunas do modelo de mineração](mining-model-columns.md)  
  
  
