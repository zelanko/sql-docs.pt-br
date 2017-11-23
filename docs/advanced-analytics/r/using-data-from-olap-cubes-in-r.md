---
title: Usando dados de cubos OLAP em R | Microsoft Docs
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1c55a5b834cd91478a87ded7ebb86884117c7bfb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="using-data-from-olap-cubes-in-r"></a>Usando dados de cubos OLAP em R

O **olapR** pacote é um pacote R, fornecido pela Microsoft para uso com o servidor de aprendizado de máquina e o SQL Server R Services, que permite a você executar consultas MDX para obter dados de cubos OLAP. Com este pacote, você não precisa criar servidores vinculados ou limpeza de conjuntos de linhas bidimensionais; Você pode usar dados OLAP diretamente em R.

Este artigo descreve a API, juntamente com uma visão geral fo OLAP e MDX para usuários de R que podem ser novos para bancos de dados de cubo multidimensional.

## <a name="what-is-an-olap-cube"></a>O que é um cubo OLAP?

OLAP é uma abreviação de processamento analítico Online. Soluções OLAP são amplamente usadas para capturar e armazenar dados essenciais aos negócios ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, consulte [processamento analítico on-line](https://en.wikipedia.org/wiki/Online_analytical_processing).

A Microsoft fornece [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services), que permite projetar, implantar e consultar dados OLAP na forma de _cubos_ ou _modelos de tabela_. Um cubo é um banco de dados multidimensional. _Dimensões_ são como facetas de dados ou fatores em r: você usar dimensões para identificar um subconjunto específico de dados que você deseja resumir ou analisar. Por exemplo, o tempo é uma dimensão importante tanta para que muitas soluções OLAP incluem vários calendários definidos por padrão, para usar quando a divisão e resumir dados. 

Por motivos de desempenho, um banco de dados OLAP geralmente calcula resumos (ou _agregações_) com antecedência e, em seguida, armazena-os para uma recuperação mais rápida. Resumos baseiam-se no *medidas*, que representam as fórmulas que podem ser aplicadas a dados numéricos. Usar as dimensões para definir um subconjunto de dados e, em seguida, calcular a medida em que os dados. Por exemplo, você usaria uma medida para calcular o total de vendas para uma determinada linha de produto em vários trimestres menos impostos para relatar os custos de envio médio para um fornecedor específico, year-to-date cumulativos salários pagos e assim por diante.

O MDX, abreviação de expressões MDX, é o idioma usado para consultar cubos. Uma consulta MDX normalmente contém uma definição de dados que inclui uma ou mais dimensões e pelo menos uma medida, consultas MDX thogh podem ser consideravelmente mais complexas e incluem a execução de windows, cumulativas médias ou somas, percentuais. 

Aqui estão algumas outras condições que podem ser úteis quando você começar a criar consultas MDX:

+ *Dividindo* usa um subconjunto do cubo usando valores de uma única dimensão.

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

Este tópico fornece mais exemplos de como a sintaxe básica para consultas em um cubo: 

+ [Como criar consultas MDX usando R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

## <a name="olapr-api"></a>olapR API

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX:

- **Use o construtor MDX.** Use as funções de R no pacote para gerar uma consulta MDX simples, escolhendo um cubo e os eixos de configuração e segmentações de dados. Isso é uma maneira fácil de criar uma consulta MDX válida, se você não tem acesso a ferramentas tradicionais de OLAP ou não tem conhecimento profundo da linguagem MDX.

    Nem todas as consultas MDX possíveis podem ser criadas usando esse método, como MDX pode ser complexo. No entanto, essa API dá suporte à maioria das operações mais comuns e úteis, inclusive fatia, dados, busca detalhada, rollup e dinâmica em dimensões N.

+ **Copiar e colar MDX bem formado.** Crie manualmente e, em seguida, cole em qualquer consulta MDX. Essa opção é o melhor se você tiver consultas MDX existentes que você deseja reutilizar, ou se a consulta que você deseja criar é muito complexa para **olapR** para tratar. 

    Construa o MDX usando o utilitário de cliente, como o SSMS ou o Excel e, em seguida, salvar a cadeia de caracteres que define a consulta MDX. Fornecer essa cadeia de caracteres MDX como um argumento para o *manipulador de consulta do SSAS* no **olapR** pacote. A função envia a consulta para o servidor do Analysis Services especificado e passa os resultados de volta para R, supondo que você tem permissões para consultar o cubo do curso.

Para obter exemplos de como criar um MDX consultarem ou executar uma consulta MDX existente, consulte [como criar consultas MDX usando R](../../advanced-analytics/r/how-to-create-mdx-queries-using-olapr.md).

## <a name="known-issues"></a>Problemas conhecidos

### <a name="tabular-models-not-supported"></a>Modelos de tabela não tem suportados

+ Se você se conectar a uma instância de tabela do Analysis Services, o `explore` função será relatada com êxito com um valor de retorno de TRUE. No entanto, os objetos de modelo de tabela não são um tipo compatível e não podem ser explorados.

+ Modelos de tabela podem ser consultados usando DAX ou MDX. Se você criar uma consulta MDX válida em um modelo de tabela usando uma ferramenta externa e, em seguida, cole a consulta Esta API, a consulta retorna um resultado nulo e não relata um erro.

## <a name="resources"></a>Recursos

Se você for novo no OLAP ou nas consultas MDX, consulte estes artigos da Wikipédia: [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
[Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Exemplos

Se você quiser saber mais sobre cubos, você pode criar o cubo que é usado nesses exemplos, seguindo o tutorial do Analysis Services até Lição 4: [Criar um Cubo OLAP](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)

Você também pode baixar um cubo existente como um backup e restaurá-lo em uma instância do Analysis Services. Por exemplo, você pode baixar um cubo completamente processado do [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)em formato compactado, e restaurá-lo na sua instância do SSAS. Para obter mais informações, consulte [Backup e Restauração](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)ou [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).
