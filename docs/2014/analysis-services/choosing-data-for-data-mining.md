---
title: Escolhendo os dados para mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- content type [data mining]
- nested tables
- key [data mining]
- continuous values
- key sequence [data mining]
- table data type
- key time [data mining]
- discrete values
- discretized
ms.assetid: 7c72d80e-913c-4bbe-b258-444294a78838
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9bec249e483c5736ee7cf0e66f4aff0af98e08c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088030"
---
# <a name="choosing-data-for-data-mining"></a>Escolhendo os dados para a mineração de dados
  Conforme você começa a mineração de dados, talvez você pergunte: "quantos dados precisarei?" ou "Há algum requisito especial que eu deva saber ao apagar ou formatar meus dados?"  
  
 Em particular, as pessoas iniciantes na mineração de dados frequentemente têm problemas com dados do Excel, como a necessidade de formatar os dados de forma consistente dentro das colunas, apagar valores ausentes ou compartimentalizar números. Esta seção também lista os requisitos de dados para tipos específicos de modelos.  
  
 [Escolhendo os dados](#bkmk_ChoosingData)  
  
 [Problemas comuns de dados](#bkmk_CommonDataProblems)  
  
 [Outros requisitos de dados](#bkmk_OtherRequirements)  
  
##  <a name="bkmk_ChoosingData"></a> Escolhendo os dados  
 A seleção dos dados usados para a análise é talvez a parte mais importante do processo de mineração de dados, mais importante até mesmo que a seleção de um algoritmo. A razão é que a mineração de dados não é, em geral, controlada por hipóteses, e sim por dados. Em vez de selecionar e testar variáveis com antecedência, assim como você faria no modelo estatístico tradicional, a mineração de dados pode usar dados e descobrir novas correlações (ou não descobrir padrão nenhum). A qualidade e a quantidade de dados pode ter um efeito significativo nos resultados.  
  
 Em geral, observe as seguintes regras:  
  
-   Obtenha o máximo possível de dados limpos.  
  
-   Realize a criação de perfil de dados antes de tentar qualquer modelo. Você precisa entender os dados antes que você possa derivar o significado deles. No mínimo:  
  
    1.  Use as ferramentas nos suplementos para localizar os valores mínimo e máximo, os valores mais comuns e os valores médios.  
  
    2.  Preencha os valores ausentes. Os suplementos (assim como alguns algoritmos) fornecem ferramentas para a entrada de valores ausentes.  
  
    3.  Corrija os dados incorretos sempre que possível. Os projetos de mineração de dados servem frequentemente como ímpeto para novas iniciativas de qualidade de dados.  
  
-   Tente criar um modelo de teste e descobrir os problemas de dados dessa forma. À medida que examina os resultados, você pode descobrir, por exemplo, se as projeções de vendas estão baseadas em dados anômalos devido a um erro de conversão de moeda.  
  
-   Tente converter os dados em diferentes formatos, ou tente criar buckets de números. Os padrões surgem com frequência quando os dados são transformados.  
  
     Por exemplo, o nível de serviço no call center pode ser afetado conforme o dia da semana, o que você não verá se estiver usando apenas os valores datetime. As previsões podem ser melhores quando geradas em ciclos de 10 dias em vez de unidades semanais ou diárias.  
  
-   Coloque os números nos compartimentos apropriados para reduzir o número de valores possíveis para a análise.  
  
-   Crie várias versões dos seus dados e compile vários modelos.  
  
 Para obter dicas adicionais sobre como selecionar, modificar e examinar os dados, consulte [lista de verificação de preparação para mineração de dados](checklist-of-preparation-for-data-mining.md).  
  
### <a name="how-much-data-do-i-need"></a>De quantos dados precisarei?  
 Uma regra básica é nunca ter menos de 50 a 100 linhas de dados para os tipos e cenários de modelos mais simples. Por exemplo, se você estiver prevendo um único atributo usando um modelo Naïve Bayes e o conjunto de dados estiver bem-formado, poderá gerar previsões razoavelmente precisas usando de 50 a 100 linhas de dados.  
  
 Para modelos de associação, você normalmente precisa de muito mais dados – mil linhas podem não ser suficiente se você estiver analisando muitos atributos, como associações entre produtos. Se o seu conjunto de dados for muito grande ou muito pequeno, às vezes você poderá obter resultados melhores recolhendo as linhas em categorias. Por exemplo, em vez de analisar associações entre produtos individuais, você pode categorizar os produtos.  
  
 Se você tiver um conjunto de dados de um tamanho razoável, concentre-se mais na qualidade dos dados em vez de adicionar cada vez mais dados. Após um determinado ponto, todos os padrões estatisticamente válidos terão sido encontrados, e adicionar mais dados não melhora sua validade. Por outro lado, à medida que adiciona mais dados, você às vezes pode introduzir correlações acidentais.  
  
### <a name="discrete-vs-continuous-numbers"></a>Vs discretos. Números contínuos  
 Uma coluna *discreta* contém um número finito de valores. Por exemplo, textos sempre são tratados como valores discretos.  
  
 Há alguns atributos importantes para valores discretos. Por exemplo, se você tratar os números como sendo discretos, nenhuma ordem será implícita entre eles, e você não poderá especificar a média ou somar os números. Os códigos de área de telefone são um bom exemplo de dados numéricos discretos que você nunca usaria para executar operações matemáticas.  
  
 Os valores discretos algumas vezes são mencionados como valores de categoria, porque você pode agrupar um conjunto de dados por eles, embora não seja possível fazer isso com números organizados em uma série infinita.  
  
 Você também pode optar por tratar os números como sendo discretos quando os valores estiverem claramente separados e não houver nenhuma possibilidade de valores fracionários, ou os valores fracionários não forem úteis.  
  
 Dados numéricos*contínuos* podem conter um número infinito de valores fracionários. Uma coluna de renda é um exemplo de uma coluna de atributo contínua. Se você especificar que uma coluna é numérica, todos os valores dessa coluna deverão ser números, exceto os nulos. Observe que, no Excel, carimbos de data/hora e qualquer outra representação de data e hora que possa ser convertida em um tipo de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem ser considerados.  
  
 **Convertendo números em variáveis categóricas**  
  
 Só porque uma coluna contém números, isso não significa que você deverá tratá-los como números contínuos. A*discretização* oferece várias vantagens para análise. Uma delas é a redução do problema de espaço. Outra vantagem é que às vezes os números não são o modo apropriado de expressar um resultado.  
  
 Por exemplo, o número de filhos por domicílio pode ser tratado como um valor contínuo ou discreto. Como não é possível ter 2,5 filhos em casa, e residências com 3 filhos ou mais podem se comportar de forma muito diferente de residências com 2 filhos, você pode obter resultados melhores tratando esse número como uma categoria. Entretanto, se estiver criando um modelo de regressão ou de outra forma precisar de uma média (como 1,357 filhos por domicílio), você deverá usar um tipo de dados numérico contínuo.  
  
 Não é possível criar um modelo de mineração que tenha dados contínuos e depois tratar a coluna como distinta. Os dois conjuntos de dados devem ser processados de forma diferente e ser tratados no back-end como estruturas de mineração separadas. Se você não tiver certeza da forma correta de tratar os dados, você deverá criar modelos separados que manipulam os dados de maneira diferente. Em qualquer caso, é recomendável obter uma perspectiva diferente de seus dados e, talvez, resultados diferentes.  
  
 **Convertendo números em texto**  
  
 Com muita frequência, os valores que devam ser discretos, como Homem e Mulher, são representados como dados numéricos, usando os rótulos 1 e 2. Em geral, essa codificação é executada para simplificar a entrada de dados ou economizar espaço de armazenamento em um banco de dados, mas a codificação pode levar a uma ambiguidade quanto à natureza ou ao significado dos valores. Além disso, como os valores discretos são armazenados como números, ao mover dados entre aplicativos, talvez você encontre erros de conversão de tipo de dados e os valores sejam calculados ou tratados como contínuos. Para evitar esses problemas, antes de iniciar a mineração de dados, você deve converter os rótulos numéricos novamente em rótulos de texto discretos.  
  
 **Compartimentalizando números**  
  
 Embora todos os números em princípio sejam infinitos e, portanto, contínuos, quando você estiver modelando informações, talvez ache mais eficiente *discretizar* ou *guardar* os valores disponíveis.  
  
 Você pode guardar dados de muitas maneiras:  
  
-   Especifique um número finito de buckets e permita que o algoritmo classifique os valores em buckets.  
  
-   Agrupe-os previamente por sua conta, criando alguns agrupamentos que tenham significativo de negócios ou que sejam mais fáceis de trabalhar. Com esta abordagem, quase sempre você perde a verdadeira distribuição de valores, mas os intervalos são mais fáceis de ler para os usuários.  
  
-   Permita que o algoritmo determine o número ideal de buckets e a distribuição de valores. Esse é o padrão na maioria das ferramentas, mas você pode substituir esses padrões nos assistentes de barra de ferramentas **Mineração de Dados** .  
  
-   Aproximando valores a um meio central ou a um valor representativo.  
  
##  <a name="bkmk_CommonDataProblems"></a> Problemas comuns de dados  
  
### <a name="excel-number-formats"></a>Formatos numéricos do Excel  
 Excel é uma ferramenta fácil de usar porque é tolerante - você pode colocar qualquer tipo de dados em qualquer lugar! Entretanto, antes de começar a procurar por padrões e por correlações de análise, será preciso impor estrutura ou limites a seus dados.  
  
 Por padrão, quando você importa dados numéricos para o [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel, os números são armazenados em um formato decimal com duas casas decimais. Se esse não for um formato numérico apropriado, altere-o para outro formato numérico ou altere o número de casas decimais.  
  
 Uma opção é usar a ferramenta [Rotular Novamente](relabel-sql-server-data-mining-add-ins.md) para alterar o modo como os números são exibidos ou agrupados.  
  
 Contudo, se os dados forem complexos demais para serem processados com a ferramenta **Rotular Novamente** , use as funções numéricas do Excel para convertê-los em intervalos discretos, salve o resultado em uma coluna separada e use a coluna de dados discretos para classificação.  
  
 Por exemplo, se você estiver analisando os resultados de uma corrida e quiser agrupar os corredores pelo tempo de chegada em minutos, poderá arredondar para o minuto mais próximo e salvar esse valor arredondado em uma nova coluna. Também é possível extrair apenas o valor de minuto usando a função `MINUTE` e salvar esse valor em uma nova coluna para uso em análises.  
  
### <a name="discretizing-numbers-and-dates-in-excel"></a>Discretizando números e datas no Excel  
 Por padrão, os dados numéricos no Excel são armazenados como `Double`. As datas e as horas também são armazenadas no formato numérico. Se for necessário discretizar números ou datas para mineração de dados, você deverá adicionar novas colunas antes de criar o modelo de mineração de dados ou converter datas e números em outro formato antecipadamente.  
  
### <a name="scientific-number-formats"></a>Formatos numéricos científicos  
 Com frequência, as ferramentas de mineração de dados geram probabilidade em notação científica, para representar números muito grandes ou muito pequenos. Se você não estiver familiarizado com notação científica, poderá exibir facilmente esses números em outro formato simplesmente alterando a formatação da célula.  
  
##### <a name="to-change-scientific-notation-to-a-decimal-numeric-format"></a>Para alterar notação científica para um formato numérico decimal  
  
1.  Na tabela de dados do Excel, realce a coluna ou a célula que contém o número em notação científica.  
  
2.  Clique com o botão direito do mouse e selecione **Formatar células** no menu de atalho.  
  
3.  Na lista **Categoria** , selecione **Número**.  
  
4.  Aumente o número de casas decimais. Uma probabilidade que é representada em notação científica geralmente é muito pequena.  
  
     Somente a exibição do número é alterada, não o valor subjacente.  
  
### <a name="working-with-dates-and-times"></a>Trabalhando com data e hora  
 Quando há datas em uma tabela do Excel e você usa a coluna como entrada ou para previsão, talvez receba resultados inesperados, dependendo da formatação das informações de data ou hora. Por exemplo, quando você usa **Detectar Categorias** ou **Classificar** e inclui uma coluna que contém datas, as datas são categorizadas como números com muitas casas decimais. Isso não é um erro; trata-se de uma representação precisa dos dados subjacentes. O algoritmo de mineração de dados funciona com o formato de armazenamento subjacente, não o formato de exibição.  
  
 Se você tiver dificuldade em trabalhar com datas e quiser analisar datas usando agrupamentos de senso comum como mês ou dia, use as funções DATE no Excel para extrair o ano, o mês ou o dia em uma coluna separada e use essa coluna para classificação.  
  
##  <a name="bkmk_OtherRequirements"></a> Outros requisitos de dados  
  
### <a name="requirements-by-algorithm-type"></a>Requisitos por tipo de algoritmo  
 Alguns algoritmos usados nos suplementos requerem tipos de dados ou tipos de conteúdo específicos para criar um modelo.  
  
 **Modelos de Naïve Bayes**  
  
-   O algoritmo Naive Bayes do [!INCLUDE[msCoName](../includes/msconame-md.md)] não pode usar colunas contínuas como entrada. Isso significa que você deve compartimentalizar os números, ou se houver poucos valores suficientes, tratá-los como valores discretos.  
  
-   Esse tipo de modelo também não pode prever valores contínuos. Em virtude disso, se você quiser prever um número contínuo como renda (por exemplo), você deve primeiro compartimentalizar os valores em intervalos significativos. Se você não tiver certeza de quais são os intervalos apropriados, você pode usar o algoritmo de clustering para identificar grupos de números em seus dados.  
  
-   Quando você usa um assistente baseado neste algoritmo (como [analisar os influenciadores principais &#40;ferramentas de análise de tabela para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)), colunas contínuas serão compartimentalizadas pelo Assistente de você.  
  
-   Se você criar um modelo Naive Bayes usando a [avançadas de modelagem &#40;Data Mining Add-ins para Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) opção, colunas de número serão removidas do modelo. Se você quiser evitar isso, use o [rotular novamente &#40;SQL Server Data Mining Add-ins&#41; ](relabel-sql-server-data-mining-add-ins.md) ferramenta para criar uma nova coluna com valores guardados.  
  
 **Modelos de clustering**  
  
-   As ferramentas de clustering ([Assistente de Cluster &#40;Data Mining Add-ins para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) e [detectar categorias &#40;ferramentas de análise de tabela para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)) também não é possível usar contínua números, mas ambas as ferramentas serão automaticamente compartimentalizar as colunas numéricas para você.  
  
-   Ambas as ferramentas oferecem a opção de escolher o número de categorias de saída nos resultados, mas se você quiser controlar a maneira como os valores em colunas individuais são agrupados, deverá criar uma nova coluna com o agrupamento desejado.  
  
 **Modelos de previsão**  
  
-   Todas as ferramentas de previsão exigem que você preveja um número contínuo. Você não pode prever um número que foi salvo como texto.  
  
-   Se seus dados contiverem colunas numéricas que têm o tipo de dados incorreto, você pode usar as funções do Excel ou do PowerPivot para fazer uma cópia da coluna que tem o tipo de dados numérico correto. Se você fizer isso, não se esqueça de remover a cópia da coluna que tem os números de texto, de modo que os valores não sejam duplicados.  
  
-   Se você quiser criar um gráfico de dispersão de um modelo de regressão, as variáveis de entrada também devem ser números contínuos, expressados como um tipo de dados apropriado.  
  
### <a name="using-content-types-to-make-better-models"></a>Usando tipos de conteúdo para criar modelos melhores  
 Um *tipo de conteúdo* é uma propriedade que você aplica uma coluna para especificar como os dados da coluna devem ser usados pelo modelo. O algoritmo pode usar o tipo de conteúdo como uma instrução ou uma dica ao executar a análise.  
  
 Por exemplo, se uma coluna contiver números que se repetem em um determinado intervalo para indicar os dias da semana, você poderia especificar o tipo de conteúdo dessa coluna como `Cyclical`.  
  
 Você não precisa se preocupar sobre tipos de conteúdo, se você usar os assistentes e ferramentas fornecidas neste suplemento. No entanto, se você usar o [Adicionar modelo à estrutura &#40;Data Mining Add-ins para Excel&#41; ](add-model-to-structure-data-mining-add-ins-for-excel.md) modelagem opção para adicionar um novo modelo de dados existentes, você poderá receber um erro relacionado a tipos de conteúdo.  
  
 O motivo é que alguns tipos de modelo exigem um determinado tipo de dados (como um carimbo de data e hora). As ferramentas processam essas colunas de acordo com requisitos específicos e também adicionam uma propriedade de tipo de conteúdo. Em virtude disso, se você reutilizar os dados com um algoritmo completamente diferente, poderá ser necessário alterar o tipo de dados ou tipo de conteúdo.  
  
 A lista a seguir descreve os tipos de conteúdo usados na mineração de dados e identifica os tipos de dados que oferecem suporte para cada tipo.  
  
 `Discrete`  
 A coluna contém um número finito de valores sem continuidade entre os valores. Por exemplo, uma coluna de gênero é uma coluna típica do atributo discreto, pois os dados representam um número específico de categorias.  
  
 O tipo de conteúdo `Discrete` pode ser usado com todos os tipos de dados.  
  
 `Continuous`  
 A coluna contém valores que representam dados numéricos em uma escala que permite valores provisórios. Uma coluna contínua representa medições escaláveis e é possível que os dados contenham um número infinito de valores fracionários. Uma coluna de temperaturas é um exemplo de uma coluna do atributo contínuo.  
  
 O tipo de conteúdo `Continuous` pode ser usado com os seguintes tipos de dados: `Date`, `Double` e `Long`.  
  
 `Discretized`  
 A coluna contém valores que representam grupos de valores derivados de uma coluna contínua. Os buckets são tratados como valores **ordenados** e discretos.  
  
 O tipo de conteúdo `Discretized` pode ser usado com os seguintes tipos de dados: `Date`, `Double` e `Long`.  
  
 **Chave**  
 A coluna identifica uma linha com exclusividade.  
  
 Tipicamente, a coluna de chave é um identificador numérico ou de texto que não deve ser usada para análise, somente para rastrear registros. As exceções são séries temporais e chaves sequenciais.  
  
 As**chaves de tabela aninhadas** são usadas somente quando você obtém dados de uma fonte de dados externa que tenha sido definida como uma exibição da fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para obter mais informações sobre tabelas aninhadas, consulte [ https://msdn.microsoft.com/library/ms175659.aspx ](https://msdn.microsoft.com/library/ms175659.aspx):  
  
 Esse tipo de conteúdo pode ser usado com os seguintes tipos de dados: `Date`, `Double`, `Long` e `Text`.  
  
 **Sequência de teclas**  
 A coluna contém valores que representam uma sequência de eventos. Os valores são ordenados, mas a distância entre eles não precisa ser igual.  
  
 Esse tipo de conteúdo tem suporte dos seguintes tipos de dados: `Double`, `Long`, `Text` e `Date`.  
  
 **Tempo-chave**  
 A coluna contém valores que são ordenados e representam uma escala de tempo. Use o tipo de conteúdo Key Time somente se o modelo for um modelo de série temporal ou de clustering de sequências.  
  
 Esse tipo de conteúdo é suportado pelos seguintes tipos de dados: `Double`, `Long` e `Date`.  
  
 **Table**  
 Esse tipo de conteúdo também é usado somente quando você obtém dados de uma fonte de dados externa que tenha sido definida como uma exibição da fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 O que isso significa é que cada linha de dados realmente contém uma tabela de dados aninhada, com uma ou mais colunas e uma ou mais linhas.  
  
 Tabelas aninhadas são muito úteis, mas você pode usá-los apenas com o [avançadas de modelagem &#40;Data Mining Add-ins para Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md) opções de modelagem. Por exemplo, os dados de exemplo para o [Assistente de associação de &#40;cliente de mineração de dados para Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) assistente e [análise da cesta de compras &#40;ferramentas de análise de tabela para Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) ferramenta contém dados bidimensionais de uma tabela aninhada.  

  
  
