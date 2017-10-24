---
title: Criando subcubos em MDX (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], subcubes
- subcubes [MDX]
- filtered views [MDX]
- MDX [Analysis Services], subcubes
- Multidimensional Expressions [Analysis Services], subcubes
- CREATE SUBCUBE statement
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a60ea4f39735f9dfb6d8b3283faa58d38e6a075
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="building-subcubes-in-mdx-mdx"></a>Criando subcubos em MDX (MDX)
  Um subcubo é um subconjunto de um cubo representando uma exibição filtrada dos dados subjacentes. Limitando o cubo a um subcubo, é possível melhorar o desempenho das consultas.  
  
 Para definir um subcubo, use a instrução [CREATE SUBCUBE](../../../mdx/mdx-data-definition-create-subcube.md) , como descrito neste tópico.  
  
## <a name="create-subcube-syntax"></a>Sintaxe de CREATE SUBCUBE  
 Use a sintaxe a seguir para criar um subcubo:  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 A sintaxe de CREATE SUBCUBE é bem simples. O parâmetro *Subcube_Identifier* identifica o cubo que servirá de base para o subcubo. O parâmetro *Subcube_Expression* seleciona a parte do cubo que se tornará o subcubo  
  
 Criado um subcubo, ele passa a ser o contexto de todas as consultas MDX até que a sessão seja encerrada ou você execute a instrução [DROP SUBCUBE](../../../mdx/mdx-data-definition-drop-subcube.md) .  
  
### <a name="what-a-subcube-contains"></a>O que um subcubo contém  
 Embora a instrução CREATE SUBCUBE seja bem simples de usar, a instrução em si não mostra explicitamente todos os membros que se tornam parte integrante do subcubo. Aplicam-se as regras a seguir na definição de um subcubo:  
  
-   Se incluir o membro **(All)** de uma hierarquia, você incluirá todos os membros dessa hierarquia.  
  
-   Se você incluir qualquer membro, incluirá seus ascendentes e descendentes.  
  
-   Se você incluir todos os membros de um nível, incluirá todos os membros da hierarquia. Membros de outras hierarquias serão excluídos se eles não existirem com os membros do nível (por exemplo, uma hierarquia desequilibrada, como uma cidade, não contém clientes).  
  
-   Um subcubo sempre conterá todos os membros **(All)** do cubo.  
  
 Além disso, valores de agregação de um subcubo são visualmente totalizados. Por exemplo, um subcubo contém `USA`, `WA`e `OR`. O valor de agregação para `USA` será a soma de `{WA,OR}` , pois `WA` e `OR` são os únicos estados definidos pelo subcubo. Todos os outros estados serão ignorados.  
  
 Além disso, referências explicitas a células fora do subcubo retornarão valores de células que são avaliados no contexto do cubo inteiro. Por exemplo, você cria um subcubo limitado ao ano atual. Você usa a função [ParallelPeriod](../../../mdx/parallelperiod-mdx.md) para comparar o ano atual ao anterior. A diferença em valores será retornada mesmo o valor do ano anterior estando fora do subcubo.  
  
 Por fim, se o contexto original não for substituído, as funções de conjunto de uma subseleção serão avaliadas no contexto da subseleção. Se o contexto for substituído, as funções de conjunto serão avaliadas no contexto do cubo inteiro.  
  
## <a name="create-subcube-example"></a>Exemplo de CREATE SUBCUBE  
 O exemplo a seguir cria um subcubo que restringe o cubo Orçamento às contas 4200 e 4300:  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 Havendo um subcubo criado para a sessão, qualquer consulta subsequente será feita no subcubo, e não no cubo inteiro. Por exemplo, você executa a consulta abaixo. Ela retornará apenas os membros das contas 4200 e 4300.  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## <a name="see-also"></a>Consulte também  
 [Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

