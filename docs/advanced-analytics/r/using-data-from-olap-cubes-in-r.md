---
title: Usando dados de cubos OLAP no R | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 8093599c-8307-4237-983b-0908d0f8ab77
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: bdd86896b43d79b5d7cd00383476700735accff4
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="using-data-from-olap-cubes-in-r"></a>Usando dados de cubos OLAP no R

O pacote **olapR** é um novo pacote de R, fornecido no Microsoft R Server e no SQL Server R Services, que permite executar consultas MDX e usar os dados de cubos OLAP em sua solução de R.

Com esse pacote, você não precisa criar servidores vinculados ou limpar os conjuntos de linhas bidimensionais. Você pode usar dados OLAP diretamente no R,

## <a name="overview"></a>Visão geral

Um cubo OLAP é um banco de dados multidimensional que contém agregações pré-calculadas sobre *medidas*, que normalmente capturam métricas de negócio importantes, como quantidade de vendas, contagem de vendas ou outros valores numéricos. Os Cubos OLAP são amplamente usados para capturar e armazenar dados críticos de negócios ao longo do tempo. Os dados OLAP são consumidos por análise de negócios através de uma variedade de ferramentas, painéis e visualizações. Para obter mais informações, consulte [Processamento analítico online](https://en.wikipedia.org/wiki/Online_analytical_processing)

O pacote **olapR** dá suporte a dois métodos de criação de consultas MDX: 

- Você pode gerar uma consulta MDX simples usando uma API do estilo do R para escolher um cubo, eixos e segmentações de dados. Usando essas funções, você pode criar consultas MDX válidas mesmo se não tiver acesso a ferramentas tradicionais de OLAP ou não tiver conhecimento profundo sobre a linguagem MDX.

  Observe que nem todas as possíveis consultas MDX podem ser criadas usando esse método no pacote **olapR** , pois a MDX pode ser bastante complexa. No entanto, ele dá suporte a todas as operações mais comuns e úteis, incluindo dividir, cortar, analisar detalhadamente, acumular e dinamizar em dimensões de N.

+ Você pode criar manualmente e, em seguida, colar em qualquer consulta MDX. Essa opção é útil se você tem consultas MDX existentes que deseja reutilizar, ou se a consulta que você deseja criar é muito complexa para ser manipulada pelo **olapR** . 

  Com essa abordagem, você cria a MDX usando qualquer utilitário de cliente, como o SSMS ou o Excel, e então usa como um argumento de cadeia de caracteres para o *manipulador de consulta do SSAS* que é fornecido por este pacote. A função **olapR** enviará a consulta ao servidor do Analysis Services especificado e transmitirá de volta os resultados para o R.

Para exemplos de como criar uma consulta MDX ou executar uma consulta MDX existente, veja [Como criar consultas MDX usando R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md).


## <a name="mdx-basics"></a>Noções básicas do MDX

Os dados em um cubo podem ser recuperados usando a linguagem de consulta MDX (MultiDimensional Expression). Como os dados em um cubo OLAP (ou banco de dados do Analysis Services) são multidimensionais, em vez de tabulares, a MDX dá suporte a uma sintaxe complexa e a uma variedade de operações de filtragem e segmentação de dados:

+ *Dividir* usa um subconjunto do cubo selecionando um valor para uma dimensão, resultando em um cubo que é uma dimensão menor. 

+ *Segmentar* cria um subcubo, especificando um intervalo de valores em várias dimensões.

+ *Analisar detalhadamente* navega de um resumo para os detalhes.

+ *Fazer drill up* move-se de detalhes para um nível de agregação mais alto.

+ *Acumular* resume os dados em uma dimensão.

+ *Dinamizar* girar o cubo ou a seleção de dados.

Este tópico fornece mais exemplos. Os exemplos a seguir mostram a sintaxe básica para consultar um cubo.
[Como criar consultas MDX usando R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)


## <a name="known-issues"></a>Problemas conhecidos

### <a name="tabular-models-not-supported-currently"></a>No momento não há suporte para modelos tabulares

Você pode se conectar a uma instância tabular do Analysis Services e a função `explore` relatará êxito, com valor retornado de VERDADEIRO, mas objetos de modelo tabular não são um tipo compatível e não podem ser explorados. 

Os modelos tabulares oferecem suporte a consultas MDX, mas uma consulta MDX válida em um modelo tabular retornará um resultado NULO e não reportará um erro.

## <a name="resources"></a>Recursos

Se você for novo no OLAP ou nas consultas MDX, consulte estes artigos da Wikipédia: [Cubos OLAP](https://en.wikipedia.org/wiki/OLAP_cube)
[Consultas MDX](https://en.wikipedia.org/wiki/MultiDimensional_eXpressions)

### <a name="samples"></a>Exemplos

Se você quiser saber mais sobre cubos, você pode criar o cubo que é usado nesses exemplos, seguindo o tutorial do Analysis Services até Lição 4: [Criar um Cubo OLAP](../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)

Você também pode baixar um cubo existente como um backup e restaurá-lo em uma instância do Analysis Services. Por exemplo, você pode baixar um cubo completamente processado do [Adventure Works Multidimensional Model SQL 2014](http://msftdbprodsamples.codeplex.com/downloads/get/882334)em formato compactado, e restaurá-lo na sua instância do SSAS. Para obter mais informações, consulte [Backup e Restauração](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)ou [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).

## <a name="see-also"></a>Consulte também
[Como criar consultas MDX usando R](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md)

[Designer de consulta MDX do Analysis Services](http://msdn.microsoft.com/library/7e288eee-2d37-485e-a6a0-dbba5e041e26)



