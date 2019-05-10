---
title: Documentação do desenvolvedor do Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44be6e7ab0bb3598b2478f1a5f94e64fee48d05a
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449976"
---
# <a name="analysis-services-developer-documentation"></a>Documentação do desenvolvedor do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

No Analysis Services, quase todos os objetos e carga de trabalho são programável e, geralmente, há mais de uma abordagem à sua escolha.  As opções incluem escrever um código gerenciado, script ou usando padrões abertos, como XMLA e MSOLAP se seus requisitos de solução impedirem usando o .NET framework.

## <a name="what-you-can-accomplish-in-code"></a>O que você pode realizar no código
Cenários de programação típicos incluem o servidor e implantação de banco de dados, administração, modelo e criação de banco de dados e acesso a dados de seus aplicativos personalizados e relatórios que consomem dados do Analysis Services. Comum a todos esses cenários é uma fixa arquitetura e o objeto de definição hierarquia, com operações bem compreendidas que abrangem a definição de dados, processamento e cargas de trabalho de consulta.

Embora objetos e cargas de trabalho são programáveis, eles não são extensíveis. Especificamente, é possível criar cartuchos de dados personalizados que recuperam dados de fontes de dados sem suporte, personalizam ou substituir os comportamentos de mecanismo de fórmula ou armazenamento, nem você pode criar novos tipos de metadados de objeto em um servidor, o banco de dados ou o modelo.

Para elaborar ainda mais o último ponto sobre a criação de novos tipos de objeto: Embora seja possível criar um novo tipo de objeto, você pode criar objetos calculados, criados a partir de expressões ou código em tempo de execução. Nem tudo em seu modelo precisa ser predefinidos e mapeado para uma estrutura de dados existente. Além disso, você pode estender o esquema por meio de anotações no AMO para passar informações específicas do objeto ao seu aplicativo cliente.

## <a name="choose-a-platform-or-approach-to-development"></a>Escolha uma plataforma ou uma abordagem de desenvolvimento
O Analysis Services fornece várias maneiras de personalizar uma solução por meio de código, mas a maioria dos desenvolvedores usam o script ou as APIs gerenciadas.

- APIs gerenciadas incluem [AMO e TOM](http://msdn.microsoft.com/library/mt436122.aspx) para a definição de dados e tarefas administrativas, e [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) para suporte a consultas no código do cliente. No SQL Server 2016, o AMO é atualizado para usar os novos metadados de tabela para modelos criados ou atualizados para o nível de compatibilidade 1200 e superior.

- Script geralmente pode obter os mesmos resultados como um programa executável, possivelmente menos trabalho.

  - Você pode escrever um script do PowerShell usando os componentes do Analysis Services PowerShell que chamam a tipos de AMO diretamente. No PowerShell, você também pode criar e executar o ASSL/XMLA ou script TMSL (no JSON).

  - ASSL e TMSL são linguagens de script que fornecem objetos usados em descobrir e executar operações. Qual tipo de script que você usa depende do servidor, banco de dados ou modelo subjacente.

  - Modelos de tabela ou bancos de dados no nível de compatibilidade 1200 e superior usam o modelo de script TMSL (linguagem tabela), que está em JSON.

  - Modelos multidimensionais e tabulares nos níveis de compatibilidade 1050 – 1103 usar Scripting linguagem ASSL (Analysis Services), que é a extensão de serviços de análise de padrão aberto XMLA.

  - Você pode gerar um script ASSL ou TMSL no Management Studio. Você também pode usar **Exibir código** no SQL Server Data Tools para exibir a definição do modelo no ASSL ou TMSL.

- Embora seja possível criar uma solução baseada em padrões abertos de XMLA e MDX, é muito raro para fazê-lo. Não há nenhuma documentação diferente de XMLA e referência MDX para ajudar você e a maioria dos Fórum de suporte e comunidade desenha com experiências com .NET ou com tecnologias nativas de (MSOLAP).

## <a name="programming-in-analysis-services"></a>Programação no Analysis Services
[Programação de mineração de dados](../analysis-services/data-mining/data-mining-programming.md) descreve as abordagens que criam soluções que incluem objetos de mineração de dados.

[Programação de modelo multidimensional](../analysis-services/multidimensional-models/multidimensional-model-programming.md) descreve as tarefas de desenvolvimento e abordagens para integrar objetos de modelo multidimensional em uma solução personalizada.

[Programação do modelo tabular para o nível de compatibilidade 1200 e superior](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**novo no SQL Server 2016**.  Resume as interfaces e idiomas de script usados para trabalhar com Tabular 1200 e maior modelos por meio de programação.

[Programação do modelo tabular para níveis de compatibilidade 1050 até 1103](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) esta documentação destina-se a desenvolvedores que dão suporte a modelos tabulares nos níveis de compatibilidade anteriores. Ele descreve as extensões CSDL que definem um modelo de tabela em sintaxe XML. Ele também inclui informações sobre sintaxe e as definições de modelo de objeto de tabela.

[Gerenciamento de objetos AMO (Analysis Services)](https://msdn.microsoft.com/library/mt436122.aspx) documentação de referência do desenvolvedor para o provedor gerenciado, gerenciamento de objetos AMO (Analysis Services), para a definição de dados e administração, incluindo o processamento.

[O ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) documentação de referência do desenvolvedor para o provedor gerenciado, ADOMD.NET, usado para dados programáticos cargas de trabalho de acesso e de consulta.

[Conjuntos de linhas de esquema do Analysis Services](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets) descreve os conjuntos de linhas de esquema que fornecem informações sobre o estado do servidor, as operações do servidor e objetos de banco de dados.

[XML for Analysis &#40;XMLA&#41; referência](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference) conceitos de XMLA descreve que podem ajudar você a entender como o XMLA contribui para sua solução personalizada. Ele também descreve o nível de conformidade com a especificação do XMLA 1.1.

[Analysis Services Scripting Language &#40;ASSL para XMLA&#41; ](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) descreve as extensões ASSL para XMLA. O ASSL fornece uma definição de dados e uma linguagem de manipulação para os modelos multidimensionais do Analysis Services que complementa a especificação de XMLA.

[Tabular Model Scripting Language &#40;TMSL&#41; referência](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) TMSL é uma representação JSON de modelos tabulares no nível de compatibilidade 1200 e superior. Definições de objeto são com base em construções de metadados de tabela como tabela, coluna e relacionamento em vez de metadados multidimensionais que podem não ser familiares se você for novo para modelagem de dados do Analysis Services no modo de tabela.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) documenta os cmdlets usados para funções administrativas, além de uso geral **Invoke-ASCmd** cmdlet, que aceita qualquer script ou uma consulta como entrada.

## <a name="see-also"></a>Consulte também
[Referência técnica](../analysis-services/powershell/technical-reference-ssas.md)
[referência de linguagem de expressão e de consulta &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/gg492188.aspx)
