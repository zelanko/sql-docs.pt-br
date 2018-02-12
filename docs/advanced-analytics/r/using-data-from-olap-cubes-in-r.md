---
title: Usando dados de cubos OLAP em R | Microsoft Docs
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: 
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 256a8a58a61f679cd5b2981134403cc389733e75
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="using-data-from-olap-cubes-in-r"></a>Usando dados de cubos OLAP em R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O **olapR** pacote é um pacote R, fornecido pela Microsoft para uso com o servidor de aprendizado de máquina e do SQL Server, que permite a você executar consultas MDX para obter dados de cubos OLAP. Com este pacote, você não precisa criar servidores vinculados ou limpeza de conjuntos de linhas bidimensionais; Você pode obter dados OLAP diretamente do R.

Este artigo descreve a API, juntamente com uma visão geral de OLAP e MDX para usuários de R que podem ser novos para bancos de dados de cubo multidimensional.

> [!IMPORTANT]
> Uma instância do Analysis Services pode dar suporte a convencionais cubos multidimensionais ou modelos de tabela, mas uma instância não oferece suporte a ambos os tipos de modelos. Portanto, antes de tentar criar uma consulta MDX em um cubo, verifique se a instância do Analysis Services contém modelos multidimensionais.

## <a name="what-is-an-olap-cube"></a>O que é um cubo OLAP?

OLAP é uma abreviação de processamento analítico Online. Soluções OLAP são amplamente usadas para capturar e armazenar dados essenciais aos negócios ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, consulte [processamento analítico on-line](https://en.wikipedia.org/wiki/Online_analytical_processing).

A Microsoft fornece [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite projetar, implantar e consultar dados OLAP na forma de _cubos_ ou _modelos de tabela_. Um cubo é um banco de dados multidimensional. _Dimensões_ são como facetas de dados ou fatores em r: você usar dimensões para identificar um subconjunto específico de dados que você deseja resumir ou analisar. Por exemplo, o tempo é uma dimensão importante tanta para que muitas soluções OLAP incluem vários calendários definidos por padrão, para usar quando a divisão e resumir dados. 

Por motivos de desempenho, um banco de dados OLAP geralmente calcula resumos (ou _agregações_) com antecedência e, em seguida, armazena-os para uma recuperação mais rápida. Resumos baseiam-se no *medidas*, que representam as fórmulas que podem ser aplicadas a dados numéricos. Usar as dimensões para definir um subconjunto de dados e, em seguida, calcular a medida em que os dados. Por exemplo, você usaria uma medida para calcular o total de vendas para uma determinada linha de produto em vários trimestres menos impostos para relatar os custos de envio médio para um fornecedor específico, year-to-date cumulativos salários pagos e assim por diante.

O MDX, abreviação de expressões MDX, é o idioma usado para consultar cubos. Normalmente, uma consulta MDX contém uma definição de dados que inclui uma ou mais dimensões e pelo menos uma medida, embora as consultas MDX podem ser consideravelmente mais complexas e incluem o windows sem interrupção, médias cumulativas, somas, classificações ou percentuais. 

Aqui estão algumas outras condições que podem ser úteis quando você começar a criar consultas MDX:

+ *Dividindo* usa um subconjunto do cubo usando valores de uma única dimensão.

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

## <a name="how-to-use-olapr-to-create-mdx-queries"></a>Como usar olapR para criar consultas MDX

O artigo a seguir fornece exemplos detalhados de sintaxe para criar ou executar consultas em um cubo:

+ [Como criar consultas MDX usando R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX:

- **Use o construtor MDX.** Use as funções de R no pacote para gerar uma consulta MDX simples, escolhendo um cubo, e, em seguida, definindo eixos e segmentações de dados. Isso é uma maneira fácil de criar uma consulta MDX válida, se você não tem acesso a ferramentas tradicionais de OLAP ou não tem conhecimento profundo da linguagem MDX.

    Nem todas as consultas MDX podem ser criadas usando esse método, como MDX pode ser complexo. No entanto, essa API dá suporte à maioria das operações mais comuns e úteis, inclusive fatia, dados, busca detalhada, rollup e dinâmica em dimensões N.

+ **Copiar e colar MDX bem formado.** Crie manualmente e, em seguida, cole em qualquer consulta MDX. Essa opção é o melhor se você tiver consultas MDX existentes que você deseja reutilizar, ou se a consulta que você deseja criar é muito complexa para **olapR** para tratar.

    Depois de criar o MDX usando o utilitário de cliente, como o SSMS ou o Excel, salve a cadeia de caracteres de consulta. Fornecer essa cadeia de caracteres MDX como um argumento para o *manipulador de consulta do SSAS* no **olapR** pacote. O provedor envia a consulta para o servidor do Analysis Services especificado e passa os resultados de volta para R. 

Para obter exemplos de como criar um MDX consultarem ou executar uma consulta MDX existente, consulte [como criar consultas MDX usando R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista alguns problemas conhecidos e perguntas comuns sobre o **olapR** pacote.

### <a name="tabular-model-support"></a>Suporte de modelo de tabela

Se você se conectar a uma instância do Analysis Services que contém um modelo de tabela, o `explore` função será relatada com êxito com um valor de retorno de TRUE. No entanto, os objetos de modelo de tabela são diferentes de objetos multidimensionais e a estrutura de um banco de dados multidimensional é diferente do que um modelo de tabela.

Embora DAX (expressões de análise de dados) é a linguagem geralmente usada com modelos de tabela, você pode criar consultas MDX válidas em um modelo de tabela, se você já estiver familiarizado com MDX. Você não pode usar os construtores olapR a criar consultas MDX válidas em um modelo de tabela.

No entanto, as consultas MDX são uma maneira ineficiente para recuperar dados de um modelo de tabela. Se você precisar obter dados de um modelo de tabela para uso em R, considere estes métodos em vez disso:

+ Habilitar o DirectQuery no modelo e adicione o servidor como um servidor vinculado no SQL Server. 
+ Se o modelo de tabela foi criado em um armazém de dados relacionais, obtenha os dados diretamente da fonte.

### <a name="how-to-determine-whether-an-instance-contains-tabular-or-multidimensional-models"></a>Como determinar se uma instância contém modelos de tabela ou multidimensionais

Uma única instância do Analysis Services pode conter apenas um tipo de modelo, que pode conter vários modelos. O motivo é que há diferenças fundamentais entre modelos de tabela e os modelos multidimensionais que controlam a forma como os dados são armazenados e processados. Por exemplo, modelos de tabela são armazenados na memória e aproveitam os índices columnstore para executar cálculos muito rápidos. Em modelos multidimensionais, os dados são armazenados em disco e agregações são definidas antecipadamente e recuperadas por meio de consultas MDX.

Se você se conectar ao Analysis Services usando um cliente como o SQL Server Management Studio, você pode determinar rapidamente qual tipo de modelo é suportado, examinando o ícone para o banco de dados.

Você também pode visualizar e consultar as propriedades do servidor para determinar qual tipo de modelo oferece suporte a instância. O **modo de servidor** propriedade oferece suporte a dois valores: _multidimensionais_ ou _tabela_.

Consulte o seguinte artigo para obter informações gerais sobre os dois tipos de modelos:

+ [Comparando modelos multidimensionais e tabulares](https://docs.microsoft.com/sql/analysis-services/comparing-tabular-and-multidimensional-solutions-ssas)

Consulte o seguinte artigo para obter informações sobre como consultar as propriedades do servidor:

+ [OLE DB para OLAP Schema Rowsets](https://docs.microsoft.com/sql/analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets)

### <a name="writeback-is-not-supported"></a>Não há suporte para write-back

Não é possível gravar os resultados de cálculos personalizados de R de volta para o cubo.

Em geral, mesmo quando um cubo é habilitado para write-back, só limitadas operações têm suporte e podem ser necessárias configurações adicionais. É recomendável que você usar MDX para essas operações.

+ [Dimensões habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions)
+ [Partições habilitadas para gravação](https://docs.microsoft.com/sql/analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions)
+ [Definir acesso personalizado aos dados da célula](https://docs.microsoft.com/sql/analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services)

### <a name="long-running-mdx-queries-block-cube-processing"></a>Consultas MDX de longa execução bloqueiam o processamento do cubo

Embora o **olapR** pacote executa operações somente leitura longas consultas MDX podem criar bloqueios que impedem que o cubo seja processada. Sempre teste suas consultas MDX com antecedência para que você saiba que a quantidade de dados deve ser retornado.

Se você tentar se conectar a um cubo que está bloqueado, você poderá receber um erro que o data warehouse do SQL Server não pode ser alcançado. Resoluções sugeridas incluem habilitar conexões remotas, verificando o servidor ou nome de instância e assim por diante; No entanto, considere a possibilidade de uma conexão aberta anterior.

O administrador do SSAS pode evitar problemas de bloqueio, identificando e encerrando sessões abertas. Uma propriedade de tempo limite também pode ser aplicada às consultas MDX no nível do servidor para forçar o encerramento de todas as consultas de longa execução.

## <a name="resources"></a>Recursos

Se você for novo para OLAP ou para consultas MDX, consulte estes artigos da Wikipedia: 

+ [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
+ [Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)
