---
title: Usando dados de cubos OLAP no R - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e55093c83e9a306a06235d6bb613dac78d4677ce
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512963"
---
# <a name="using-data-from-olap-cubes-in-r"></a>Usando dados de cubos OLAP no R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O **olapR** pacote é um pacote de R, fornecido pela Microsoft para uso com o Machine Learning Server e o SQL Server, que permite executar consultas MDX para obter dados de cubos OLAP. Com esse pacote, você não precisa criar servidores vinculados ou limpar os conjuntos de linhas bidimensionais; Você pode obter dados OLAP diretamente do R.

Este artigo descreve a API, juntamente com uma visão geral de OLAP e MDX para os usuários de R que podem ser novos para bancos de dados de cubo multidimensional.

> [!IMPORTANT]
> Uma instância do Analysis Services pode dar suporte a convencionais cubos multidimensionais ou modelos de tabela, mas uma instância não oferece suporte a ambos os tipos de modelos. Portanto, antes de tentar criar uma consulta MDX em um cubo, verifique se a instância do Analysis Services contém modelos multidimensionais.

## <a name="what-is-an-olap-cube"></a>O que é um cubo OLAP?

O OLAP é a abreviação de processamento analítico Online. Soluções OLAP são amplamente usadas para capturar e armazenar dados críticos de negócios ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, consulte [processamento analítico Online](https://en.wikipedia.org/wiki/Online_analytical_processing).

A Microsoft fornece [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite projetar, implantar e consultar dados OLAP na forma de _cubos_ ou _modelos de tabela_. Um cubo é um banco de dados multidimensional. _Dimensões_ são como facetas de dados ou fatores no r: usar dimensões para identificar algum subconjunto específico de dados que você deseja resumir ou analisar. Por exemplo, o tempo é uma dimensão importante, tanta para que muitas soluções OLAP incluem vários calendários definidos por padrão, a ser usado ao segmentar e resumir dados. 

Por motivos de desempenho, um banco de dados OLAP geralmente calcula resumos (ou _agregações_) com antecedência e, em seguida, armazena-os para uma recuperação mais rápida. Resumos se baseiam *medidas*, que representam as fórmulas que podem ser aplicadas a dados numéricos. Você usa as dimensões para definir um subconjunto de dados e, em seguida, calcula a medida em que os dados. Por exemplo, você usaria uma medida para calcular o total de vendas para uma determinada linha de produto nos vários trimestres menos impostos, para relatar os custos de envio de média para um determinado fornecedor, year-to-date cumulativos salários pagos e assim por diante.

O MDX, abreviação de expressões MDX, é o idioma usado para consultar cubos. Normalmente, uma consulta MDX contém uma definição de dados que inclui uma ou mais dimensões e pelo menos uma medida, apesar de consultas MDX podem obter consideravelmente mais complexas e incluir o windows sem interrupção, as médias cumulativas, somas, classificações ou percentuais. 

Aqui estão alguns outros termos que podem ser úteis quando você começar a criar consultas MDX:

+ *Dividindo* usa um subconjunto do cubo usando valores de uma única dimensão.

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Como usar o olapR para criar consultas MDX

O artigo a seguir fornece exemplos detalhados da sintaxe para criar ou executar consultas em um cubo:

+ [Como criar consultas MDX usando R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>API de olapR

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX:

- **Use o construtor MDX.** Use as funções de R no pacote para gerar uma consulta MDX simples, escolhendo um cubo e, em seguida, definindo eixos e segmentações de dados. Isso é uma maneira fácil de criar uma consulta MDX válida, se você não tem acesso a ferramentas tradicionais de OLAP ou não tiver conhecimento profundo sobre a linguagem MDX.

    Nem todas as consultas MDX podem ser criadas usando esse método, como MDX pode ser complexa. No entanto, essa API dá suporte à maioria das operações mais comuns e úteis, incluindo a fatia, dice, busca detalhada, pacote cumulativo de atualizações e pivot em dimensões de N.

+ **Copie e cole o MDX bem formado.** Criar manualmente e, em seguida, cole em qualquer consulta MDX. Essa opção é a melhor se você tiver consultas MDX existentes que você deseja reutilizar, ou se a consulta que você deseja criar é muito complexa para **olapR** para manipular.

    Depois de criar a MDX usando qualquer utilitário de cliente, como o SSMS ou o Excel, salve a cadeia de caracteres de consulta. Forneça essa cadeia de caracteres MDX como um argumento para o *manipulador de consulta do SSAS* na **olapR** pacote. O provedor envia a consulta ao servidor do Analysis Services especificado e passa os resultados de volta para o R. 

Para obter exemplos de como criar um MDX consultarem ou executar uma consulta MDX existente, consulte [como criar consultas MDX usando R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista alguns problemas conhecidos e perguntas comuns sobre o **olapR** pacote.

### <a name="tabular-model-support"></a>Suporte de modelo de tabela

Se você se conectar a uma instância do Analysis Services que contém um modelo tabular, o `explore` função será relatada com êxito com um valor de retorno de TRUE. No entanto, os objetos de modelo de tabela são diferentes de objetos multidimensionais e a estrutura de um banco de dados multidimensional é diferente de um modelo de tabela.

Embora o DAX (expressões de análise de dados) é a linguagem normalmente usada com modelos de tabela, você pode criar consultas MDX válidas em relação a um modelo de tabela, se você já estiver familiarizado com MDX. É possível usar os construtores de olapR para criar consultas MDX válidas em um modelo tabular.

No entanto, consultas MDX são uma maneira eficiente para recuperar dados de um modelo de tabela. Se você precisar obter dados de um modelo de tabela para uso em R, considere estes métodos em vez disso:

+ Habilitar o DirectQuery no modelo e adicione o servidor como um servidor vinculado no SQL Server. 
+ Se o modelo de tabela foi criado em um data mart relacional, obter os dados diretamente da fonte.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Como determinar se uma instância contém modelos de tabela ou multidimensionais

Uma única instância do Analysis Services pode conter apenas um tipo de modelo, embora ele pode conter vários modelos. O motivo é que há diferenças fundamentais entre os modelos de tabela e em modelos multidimensionais que controlam a forma como os dados são armazenados e processados. Por exemplo, modelos de tabela são armazenados na memória e aproveitam os índices columnstore para executar cálculos muito rápidos. Em modelos multidimensionais, os dados são armazenados no disco e as agregações são definidas antecipadamente e recuperadas por meio de consultas MDX.

Se você se conectar ao Analysis Services usando um cliente como o SQL Server Management Studio, você pode informar rapidamente qual tipo de modelo é suportado, examinando o ícone para o banco de dados.

Você também pode exibir e consultar as propriedades do servidor para determinar qual tipo de modelo dá suporte para a instância. O **modo de servidor** propriedade dá suporte a dois valores: _multidimensional_ ou _tabular_.

Consulte o seguinte artigo para obter informações gerais sobre os dois tipos de modelos:

+ [Comparando modelos multidimensionais e tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Consulte o seguinte artigo para obter informações sobre como consultar as propriedades do servidor:

+ [Conjuntos de linhas de esquema OLE DB para OLAP](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Não há suporte para write-back

Não é possível gravar os resultados dos cálculos de R personalizados de volta para o cubo.

Em geral, mesmo quando um cubo está habilitado para write-back, limitadas somente as operações têm suporte e podem ser necessárias configurações adicionais. É recomendável que você usa MDX para essas operações.

+ [Dimensões habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partições habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Definir acesso personalizado aos dados da célula](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Consultas de MDX de longa execução bloqueiam o processamento do cubo

Embora o **olapR** pacote realiza somente operações de leitura, longas consultas MDX podem criar bloqueios que impedem que o cubo que está sendo processado. Sempre teste suas consultas MDX com antecedência para que você saiba que a quantidade de dados deve ser retornado.

Se você tentar se conectar a um cubo que está bloqueado, você poderá receber um erro que o data warehouse do SQL Server não pode ser alcançado. Resoluções sugeridas incluem habilitar conexões remotas, verificando o servidor ou nome da instância e assim por diante; No entanto, considere a possibilidade de uma conexão aberta anterior.

O administrador do SSAS pode evitar problemas de bloqueio, identificando e encerrando sessões abertas. Também pode ser aplicada a uma propriedade de tempo limite para consultas MDX no nível do servidor para forçar o encerramento de todas as consultas de longa execução.

## <a name="resources"></a>Recursos

Se você for novo no OLAP ou nas consultas MDX, consulte estes artigos da Wikipédia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
