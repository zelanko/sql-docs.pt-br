---
title: Usando dados de cubos OLAP em R
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3063758e1186dc81e5ce9e70891403e7afd3a89f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345105"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Usando dados de cubos OLAP em R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O  pacote olapr é um pacote R, fornecido pela Microsoft para uso com Machine Learning Server e SQL Server, que permite executar consultas MDX para obter dados de cubos OLAP. Com este pacote, você não precisa criar servidores vinculados ou limpar conjuntos de linhas bidimensionais; Você pode obter dados OLAP diretamente do R.

Este artigo descreve a API, juntamente com uma visão geral de OLAP e MDX para usuários de R que podem ser novos em bancos de dados de cubo multidimensionais.

> [!IMPORTANT]
> Uma instância do Analysis Services pode dar suporte a cubos multidimensionais convencionais ou modelos de tabela, mas uma instância não pode dar suporte a ambos os tipos de modelos. Portanto, antes de tentar criar uma consulta MDX em um cubo, verifique se a instância de Analysis Services contém modelos multidimensionais.

## <a name="what-is-an-olap-cube"></a>O que é um cubo OLAP?

O OLAP é abreviado para processamento analítico online. As soluções OLAP são amplamente usadas para capturar e armazenar dados críticos de negócios ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, consulte [processamento analítico online](https://en.wikipedia.org/wiki/Online_analytical_processing).

A Microsoft fornece [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite projetar, implantar e consultar dados OLAP na forma de cubos  ou _modelos de tabela_. Um cubo é um banco de dados multidimensional. As _dimensões_ são como facetas dos dados, ou fatores em R: você usa dimensões para identificar um subconjunto específico de dados que você deseja resumir ou analisar. Por exemplo, o tempo é uma dimensão importante, tanto para que muitas soluções OLAP incluam vários calendários definidos por padrão, para usar na divisão e no Resumo de dados. 

Por motivos de desempenho, um banco de dados OLAP geralmente calcula resumos (ou agregações) antecipadamente e, em seguida, os armazena para recuperação mais rápida. Os resumos se baseiam em *medidas*, que representam fórmulas que podem ser aplicadas a dados numéricos. Você usa as dimensões para definir um subconjunto de dados e, em seguida, computa a medida sobre esses dados. Por exemplo, você usaria uma medida para calcular o total de vendas de uma determinada linha de produto em vários trimestres, menos impostos, para relatar os custos médios de envio de um fornecedor específico, os salários cumulativos acumulados no ano, pagos e assim por diante.

MDX, abreviação de expressões multidimensionais, é a linguagem usada para consultar cubos. Uma consulta MDX normalmente contém uma definição de dados que inclui uma ou mais dimensões, e pelo menos uma medida, embora as consultas MDX possam ser consideravelmente mais complexas e incluem janelas sem interrupção, médias acumuladas, somas, classificações ou percentuais. 

Aqui estão alguns outros termos que podem ser úteis quando você começa a criar consultas MDX:

+ A *divisão* usa um subconjunto do cubo usando valores de uma única dimensão.

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Como usar o olapr para criar consultas MDX

O artigo a seguir fornece exemplos detalhados da sintaxe para criar ou executar consultas em um cubo:

+ [Como criar consultas MDX usando o R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API olapr

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX:

- **Use o Construtor MDX.** Use as funções do R no pacote para gerar uma consulta MDX simples, escolhendo um cubo e, em seguida, configurando eixos e Segmentações de objetos. Essa é uma maneira fácil de criar uma consulta MDX válida se você não tem acesso às ferramentas OLAP tradicionais ou não tem conhecimento profundo da linguagem MDX.

    Nem todas as consultas MDX podem ser criadas usando esse método, porque a linguagem MDX pode ser complexa. No entanto, essa API oferece suporte à maioria das operações mais comuns e úteis, incluindo fatia, data, busca detalhada, acúmulo e tabela dinâmica em N dimensões.

+ **Copiar e colar MDX bem formado.** Crie e cole manualmente qualquer consulta MDX. Essa opção é a melhor se você tiver consultas MDX existentes que deseja reutilizar ou se a consulta que você deseja Compilar for muito complexa para o processamento de **OLAP** .

    Depois de criar o MDX usando qualquer utilitário cliente, como o SSMS ou o Excel, salve a cadeia de caracteres de consulta. Forneça esta cadeia de caracteres MDX como um argumento para o *manipulador de consultas do SSAS* no pacote **olapr** . O provedor envia a consulta para o servidor de Analysis Services especificado e retorna os resultados para R. 

Para obter exemplos de como criar uma consulta MDX ou executar uma consulta MDX existente, consulte [como criar consultas MDX usando o R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista alguns problemas conhecidos e perguntas comuns sobre o  pacote olapr.

### <a name="tabular-model-support"></a>Suporte ao modelo de tabela

Se você se conectar a uma instância do Analysis Services que contém um modelo de tabela `explore` , a função relatará êxito com um valor de retorno de true. No entanto, os objetos de modelo de tabela são diferentes de objetos multidimensionais e a estrutura de um banco de dados multidimensional é diferente da de um modelo de tabela.

Embora o DAX (Data Analysis Expressions) seja a linguagem normalmente usada com modelos de tabela, você pode criar consultas MDX válidas em relação a um modelo de tabela, se você já estiver familiarizado com o MDX. Você não pode usar os construtores olapr para criar consultas MDX válidas em um modelo tabular.

No entanto, as consultas MDX são uma maneira ineficiente de recuperar dados de um modelo de tabela. Se você precisar obter dados de um modelo de tabela para uso em R, considere estes métodos:

+ Habilite o DirectQuery no modelo e adicione o servidor como um servidor vinculado no SQL Server. 
+ Se o modelo de tabela foi criado em um data mart relacional, obtenha os dados diretamente da origem.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Como determinar se uma instância contém modelos de tabela ou multidimensionais

Uma única instância de Analysis Services pode conter apenas um tipo de modelo, embora possa conter vários modelos. O motivo é que há diferenças fundamentais entre modelos de tabela e modelos multidimensionais que controlam a maneira como os dados são armazenados e processados. Por exemplo, modelos de tabela são armazenados na memória e aproveitam índices columnstore para executar cálculos muito rápidos. Em modelos multidimensionais, os dados são armazenados em disco e as agregações são definidas com antecedência e recuperadas usando consultas MDX.

Se você se conectar ao Analysis Services usando um cliente como o SQL Server Management Studio, poderá perceber rapidamente qual tipo de modelo tem suporte, examinando o ícone do banco de dados.

Você também pode exibir e consultar as propriedades do servidor para determinar a qual tipo de modelo a instância oferece suporte. A propriedade **modo de servidor** dá suporte a dois valores: multidimensional ou _tabular_.

Consulte o seguinte artigo para obter informações gerais sobre os dois tipos de modelos:

+ [Comparando modelos multidimensionais e de tabela](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Consulte o seguinte artigo para obter informações sobre como consultar as propriedades do servidor:

+ [Conjuntos de linhas de esquema OLE DB para OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Não há suporte para Write-back

Não é possível gravar os resultados de cálculos de R personalizados de volta para o cubo.

Em geral, mesmo quando um cubo está habilitado para Write-back, só há suporte para operações limitadas e configuração adicional pode ser necessária. Recomendamos que você use MDX para essas operações.

+ [Dimensões habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partições habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Definir o acesso personalizado aos dados da célula](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Consultas MDX de execução longa bloqueiam o processamento do cubo

Embora o  pacote olapr execute apenas operações de leitura, as consultas MDX de execução longa podem criar bloqueios que impedem que o cubo seja processado. Sempre teste suas consultas MDX com antecedência para que você saiba a quantidade de dados que deve ser retornada.

Se você tentar se conectar a um cubo bloqueado, poderá receber um erro de que o data warehouse de SQL Server não pode ser acessado. As resoluções sugeridas incluem a habilitação de conexões remotas, a verificação do nome do servidor ou da instância e assim por diante; no entanto, considere a possibilidade de uma conexão aberta anterior.

Um administrador do SSAS pode evitar problemas de bloqueio identificando e encerrando sessões abertas. Uma Propriedade Timeout também pode ser aplicada a consultas MDX no nível do servidor para forçar o encerramento de todas as consultas de execução longa.

## <a name="resources"></a>Recursos

Se você for novo no OLAP ou em consultas MDX, consulte estes artigos da Wikipédia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
