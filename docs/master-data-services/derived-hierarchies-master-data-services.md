---
title: "Hierarquias derivadas (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "hierarquias derivadas"
  - "hierarquias [Master Data Services], hierarquias derivadas"
  - "hierarquias derivadas, sobre as hierarquias derivadas"
ms.assetid: a0fbd519-a10e-4cbd-92e6-5de9b8d3e3f0
caps.latest.revision: 13
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 13
---
# Hierarquias derivadas (Master Data Services)
  Uma hierarquia derivada do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] é derivada de relações de atributos baseados em domínio que já existem entre entidades em um modelo.  
  
 Você pode criar uma hierarquia derivada para destacar qualquer relação de atributo baseado em domínio existente no modelo.  
  
## Membros folha agrupam outros membros folha  
 Em uma hierarquia derivada, os membros folha de uma entidade são usados para agrupar os membros folha de outra entidade. Uma hierarquia derivada é baseada na relação entre essas entidades. Uma hierarquia explícita, ao contrário, é baseada apenas em membros de uma única entidade e é estruturada de qualquer maneira que você especificar.  
  
 Você pode alterar a estrutura de uma hierarquia derivada sem afetar os dados subjacentes. Contanto que as relações ainda existam no modelo, a exclusão de uma hierarquia derivada não afetará seus dados mestre.  
  
## Hierarquias explícitas versus hierarquias derivadas  
 A tabela a seguir mostra algumas das diferenças entre hierarquias explícitas e derivadas.  
  
> [!NOTE]  
>  Hierarquias explícitas são substituídas nesta versão do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
|Hierarquias explícitas|Hierarquias derivadas|  
|--------------------------|-------------------------|  
|A estrutura é definida pelo usuário|A estrutura é derivada das relações entre atributos baseados em domínio|  
|Contém os membros de uma única entidade|Contém os membros de várias entidades|  
|Usa membros consolidados para agrupar outros membros|Usa membros folha de uma entidade para agrupar membros folha de outra entidade|  
  
## Criando uma hierarquia de profundidade de variável  
 Há duas maneiras recomendadas de criar uma hierarquia de profundidade de variável:  
  
-   Se você precisar que todos os níveis tenham os mesmos atributos, crie uma única entidade e, em seguida, uma hierarquia recursiva nessa entidade usando um atributo de domínio que se baseie na entidade.  
  
-   Se você precisar de um conjunto de atributos para membros folha e outro conjunto de atributos nos níveis superiores, crie duas entidade para uma hierarquia derivada. Para a entidade folha, use um atributo de domínio que se baseie na entidade pai. Para a entidade pai, use um atributo de domínio que se baseie em si mesmo.  
  
## Exemplo de hierarquia derivada  
 No exemplo a seguir, os membros folha da entidade Product são agrupados por membros folha da entidade Subcategory, que são então agrupados por membros folha da entidade Category. Esta hierarquia é possível porque a entidade Product tem um atributo baseado em domínio denominado Subcategory, e a entidade Subcategory tem um atributo baseado em domínio denominado Category.  
  
 A estrutura de hierarquia mostra como os membros são agrupados. A entidade com a maioria dos membros está na parte inferior.  
  
 ![Hierarquia derivada da estrutura de modelos](../master-data-services/media/mds-conc-derived-hierarchy-structure.gif "Hierarquia derivada da estrutura de modelos")  
  
 Em uma hierarquia derivada, você pode realçar a relação entre Product e Subcategory, e depois entre Subcategory e Category. Quando você exibir os membros desta hierarquia, cada nível da árvore conterá membros da mesma entidade.  
  
 ![Exemplo de hierarquia derivada de mountain bike](../master-data-services/media/mds-conc-derived-hierarchy-example.gif "Exemplo de hierarquia derivada de mountain bike")  
  
 Este tipo de hierarquia impede que você mova um membro para um nível que não é válido. Por exemplo, você pode mover a Road-650 bike de uma subcategoria, Road Bikes, para outra, Mountain Bikes. Você não pode mover Road-650 diretamente abaixo de uma categoria, como 1 {Bikes}. Cada vez que você move um membro na árvore hierárquica, o valor de atributo baseado em domínio do membro muda para refletir a mudança.  
  
## Observações  
 Todos os membros na árvore hierárquica derivada são classificados por código. Você não pode alterar a ordem de classificação.  
  
 Se o atributo baseado em domínio de um membro estiver em branco e o atributo for usado para uma hierarquia derivada, o membro não será exibido na hierarquia. Crie regras de negócios para exigir o preenchimento de atributos. Para obter mais informações, consulte [exigem valores de atributo & #40. Master Data Services & 41;](../master-data-services/require-attribute-values-master-data-services.md).  
  
## Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma nova hierarquia derivada.|[Criar uma hierarquia derivada & #40. Master Data Services & 41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Ocultar ou excluir níveis em uma hierarquia derivada existente.|[Ocultar ou excluir níveis em uma hierarquia derivada & #40. Master Data Services & 41;](../master-data-services/hide-or-delete-levels-in-a-derived-hierarchy-master-data-services.md)|  
|Alterar o nome de uma hierarquia derivada existente.|[Alterar um nome de hierarquia derivada & #40. Master Data Services & 41;](../master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|Excluir uma hierarquia derivada existente.|[Excluir uma hierarquia derivada & #40. Master Data Services & 41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## Conteúdo relacionado  
  
-   [Atributos baseados em domínio & #40. Master Data Services & 41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Hierarquias explícitas e 40; Master Data Services & 41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Hierarquias recursivas & #40. Master Data Services & 41;](../master-data-services/recursive-hierarchies-master-data-services.md)  
  
-   [Hierarquias derivadas com delimitações explícitas e 40; Master Data Services & 41;](../master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)  
  
-   [Mostrar relações muitos-para-muitos em hierarquias derivadas e 40; Master Data Services & 41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md)  
  
-   [Coleções e 40; Master Data Services & 41;](../master-data-services/collections-master-data-services.md)  
  
  