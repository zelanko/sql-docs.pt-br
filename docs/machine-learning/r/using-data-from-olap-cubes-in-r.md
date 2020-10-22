---
title: Como usar dados de cubos OLAP no R
description: Este artigo descreve a API do olapR, juntamente com uma visão geral do OLAP e do MDX para usuários do R que talvez não tenham familiaridade com bancos de dados de cubo multidimensional.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/15/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5a5219b034abdd390a77e1dacd6b2b71d83a770e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195760"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Como usar dados de cubos OLAP no R
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

O pacote **olapR** é um pacote R, fornecido pela Microsoft para uso com o Machine Learning Server e o SQL Server, que permite executar consultas MDX para obter dados de cubos OLAP. Com esse pacote, você não precisa criar servidores vinculados nem limpar conjuntos de linhas bidimensionais; você pode obter os dados OLAP diretamente no R.

Este artigo descreve a API, juntamente com uma visão geral do OLAP e do MDX para usuários do R que talvez não tenham familiaridade com bancos de dados de cubo multidimensional.

> [!IMPORTANT]
> Uma instância do Analysis Services pode dar suporte a cubos multidimensionais convencionais ou modelos de tabela, mas uma instância não pode dar suporte a ambos os tipos de modelos. Portanto, antes de tentar criar uma consulta MDX em um cubo, verifique se a instância do Analysis Services contém modelos multidimensionais.

## <a name="what-is-an-olap-cube"></a>O que é um cubo OLAP?

OLAP é a abreviação de processamento analítico online. As soluções OLAP são amplamente usadas para capturar e armazenar dados corporativos críticos ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, confira [Processamento analítico online](https://en.wikipedia.org/wiki/Online_analytical_processing).

A Microsoft fornece o [Analysis Services](/analysis-services/analysis-services-overview), que permite projetar, implantar e consultar dados OLAP na forma de _cubos_ ou _modelos de tabela_. Um cubo é um banco de dados multidimensional. As _dimensões_ são como facetas dos dados ou fatores no R: você usa as dimensões para identificar um subconjunto específico de dados que deseja resumir ou analisar. Por exemplo, o tempo é uma dimensão importante, tanto que muitas soluções OLAP incluem vários calendários definidos por padrão, a ser usada na divisão e no resumo de dados. 

Por motivos de desempenho, um banco de dados OLAP muitas vezes calcula resumos (ou _agregações_) com antecedência e, em seguida, os armazena para uma recuperação mais rápida. Os resumos são baseados em *medidas*, que representam fórmulas que podem ser aplicadas a dados numéricos. Você usa as dimensões para definir um subconjunto de dados e, em seguida, calcula a medida nesses dados. Por exemplo, você usa uma medida para calcular o total de vendas de determinada linha de produtos em vários trimestres, menos impostos, para relatar os custos médios de envio de um fornecedor específico, os salários cumulativos pagos do ano atual etc.

O MDX, abreviação de expressões multidimensionais, é a linguagem usada para consultar cubos. Uma consulta MDX normalmente contém uma definição de dados que inclui uma ou mais dimensões e, pelo menos, uma medida, embora as consultas MDX possam ser consideravelmente mais complexas e incluir janelas de rolagem, médias cumulativas, somas, classificações ou percentis. 

Estes são alguns outros termos que poderão ser úteis quando você começar a criar consultas MDX:

+ A *divisão* usa um subconjunto do cubo usando valores de uma única dimensão.

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Como usar o olapR para criar consultas MDX

O seguinte artigo fornece exemplos detalhados da sintaxe usada para criar ou executar consultas em um cubo:

+ [Como criar consultas MDX usando o R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API do olapR

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX:

- **Use o Construtor MDX.** Use as funções do R no pacote para gerar uma consulta MDX simples, escolhendo um cubo e, em seguida, configurando eixos e segmentações. Essa é uma maneira fácil de criar uma consulta MDX válida se você não tem acesso a ferramentas OLAP tradicionais nem um conhecimento profundo da linguagem MDX.

    Nem todas as consultas MDX podem ser criadas com esse método, porque a linguagem MDX pode ser complexa. No entanto, essa API dá suporte a maioria das operações mais comuns e úteis, incluindo dividir, segmentar, fazer drill down, fazer rollup e dinamizar em N dimensões.

+ **Copiar e colar um MDX bem formado.** Faça uma criação manual e, em seguida, uma colagem em qualquer consulta MDX. Essa opção é a melhor se você tem consultas MDX que deseja reutilizar ou se a consulta que deseja criar é muito complexa para ser tratada pelo **olapR**.

    Depois de criar o MDX usando qualquer utilitário de cliente, como o SSMS ou o Excel, salve a cadeia de consulta. Forneça essa cadeia de caracteres MDX como um argumento para o *manipulador de consulta do SSAS* no pacote **olapR**. O provedor envia a consulta ao servidor especificado do Analysis Services e passa novamente os resultados para o R. 

Para obter exemplos de como criar uma consulta MDX ou executar uma consulta MDX existente, confira [Como criar consultas MDX usando o R](../../machine-learning/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista alguns problemas conhecidos e perguntas comuns sobre o pacote **olapR**.

### <a name="tabular-model-support"></a>Suporte ao modelo de tabela

Se você se conectar a uma instância do Analysis Services que contém um modelo de tabela, a função `explore` relatará êxito com um valor retornado igual a TRUE. No entanto, os objetos de modelo de tabela são diferentes de objetos multidimensionais e a estrutura de um banco de dados multidimensional é diferente daquela de um modelo de tabela.

Embora o DAX (Data Analysis Expressions) seja a linguagem normalmente usada com modelos de tabela, você pode criar consultas MDX válidas em um modelo de tabela se já tem familiaridade com o MDX. Não é possível usar os construtores do olapR para criar consultas MDX válidas em um modelo de tabela.

No entanto, as consultas MDX são uma maneira ineficiente de recuperar dados de um modelo de tabela. Caso você precise obter dados de um modelo de tabela para uso no R, considere estes métodos:

+ Habilite o DirectQuery no modelo e adicione o servidor como um servidor vinculado no SQL Server. 
+ Se o modelo de tabela foi criado em um data mart relacional, obtenha os dados diretamente da fonte.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Como determinar se uma instância contém modelos de tabela ou multidimensionais

Uma única instância do Analysis Services pode conter apenas um tipo de modelo, embora possa conter vários modelos. O motivo disso é que há diferenças fundamentais entre modelos de tabela e modelos multidimensionais que controlam a maneira como os dados são armazenados e processados. Por exemplo, os modelos de tabela são armazenados na memória e aproveitam índices columnstore para fazer cálculos muito rápidos. Em modelos multidimensionais, os dados são armazenados em disco e as agregações são definidas com antecedência e recuperadas usando consultas MDX.

Se você se conectar ao Analysis Services usando um cliente como o SQL Server Management Studio, poderá perceber rapidamente qual tipo de modelo é compatível examinando o ícone do banco de dados.

Você também pode ver e consultar as propriedades do servidor para determinar a qual tipo de modelo a instância dá suporte. A propriedade **Modo de servidor** dá suporte a dois valores: _multidimensional_ ou _de tabela_.

Confira o seguinte artigo para obter informações gerais sobre os dois tipos de modelos:

+ [Como comparar modelos multidimensionais e de tabela](/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Confira o seguinte artigo para obter informações sobre como consultar as propriedades do servidor:

+ [Conjuntos de linhas de esquema OLE DB para OLAP](/previous-versions/sql/sql-server-2012/ms126079(v=sql.110))

### <a name="writeback-is-not-supported"></a>Não há suporte para write-back

Não é possível gravar os resultados de cálculos personalizados do R novamente no cubo.

Em geral, mesmo quando um cubo está habilitado para write-back, só há suporte para operações limitadas e uma configuração adicional pode ser necessária. Recomendamos que você use o MDX para essas operações.

+ [Dimensões habilitadas para gravação](/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partições habilitadas para gravação](/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Definir o acesso personalizado a dados de célula](/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Consultas MDX de execução longa bloqueiam o processamento do cubo

Embora o pacote **olapR** só execute operações de leitura, as consultas MDX de execução longa podem criar bloqueios que impedem o processamento do cubo. Sempre teste as consultas MDX com antecedência para saber a quantidade de dados que deve ser retornada.

Se você tentar se conectar a um cubo bloqueado, poderá receber um erro indicando que o data warehouse do SQL Server não pode ser acessado. As resoluções sugeridas incluem a habilitação de conexões remotas, a verificação do nome do servidor ou da instância etc.; no entanto, considere a possibilidade de uma conexão aberta anterior.

Um administrador do SSAS pode evitar problemas de bloqueio identificando e encerrando as sessões abertas. Uma propriedade de tempo limite também pode ser aplicada a consultas MDX no nível do servidor para forçar o encerramento de todas as consultas de execução longa.

## <a name="resources"></a>Recursos

Se você não tem familiaridade com o OLAP nem com as consultas MDX, confira estes artigos da Wikipédia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)