---
title: "Criar uma dimens&#227;o usando uma tabela existente | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "hierarquias [Analysis Services], dimensões"
  - "tabelas de dimensões principais"
  - "dimensões [Analysis Services], padrão"
  - "dimensões padrão [Analysis Services]"
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# Criar uma dimens&#227;o usando uma tabela existente
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o Assistente para Dimensões no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para criar uma dimensão por meio de uma tabela existente. Isso é feito selecionando a opção **Usar uma tabela existente** na página **Selecionar Método de Criação** do assistente. Se você selecionar essa opção, o assistente fornecerá a base da estrutura de dimensão nas tabelas de dimensão, suas colunas e qualquer relação entre essas colunas em uma exibição da fonte de dados existente. O assistente dá exemplos de dados na tabela de origem e nas tabelas relacionadas. Ele usa esses dados para definir as colunas de atributo baseadas nas colunas das tabelas de dimensão, e para definir hierarquias de atributos (chamadas hierarquias *definidas pelo usuário*). Depois que você usar o Assistente para Dimensões para criar sua dimensão, é possível usar o Designer de Dimensão para adicionar, remover e configurar atributos e hierarquias na dimensão.  
  
 Quando você estiver usando uma tabela existente para criar uma dimensão, o Assistente para Dimensões o orientará nas seguintes etapas:  
  
-   Especificando informações sobre a origem  
  
-   Selecionando tabelas relacionadas  
  
-   Selecionando atributos de dimensão  
  
-   Definindo inteligência de conta  
  
> [!NOTE]  
>  Para obter instruções passo a passo que correspondam às informações apresentada neste tópico, consulte [Criar uma dimensão usando o Assistente de Dimensões](../../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md).  
  
## Especificando informações sobre a origem  
 Você especifica as informações sobre origem na página **Especificar Informações sobre a Origem**. Você começa esse processo selecionando a exibição da fonte de dados que contém a tabela onde quer que seja baseada a dimensão. Depois, você especifica a tabela principal de dimensão para a dimensão que está definindo. A tabela principal de dimensão é a tabela que está diretamente vinculada à tabela de fatos. Por exemplo, especifique uma tabela Produto como a tabela principal para uma dimensão de Produto, ou uma tabela Funcionário para uma dimensão de Funcionários. O assistente automaticamente seleciona uma coluna de chave com base na chave primária da exibição da fonte de dados. Entretanto, você pode alterar a coluna de chave conforme apropriado. A coluna de chave determina os membros da dimensão. Por exemplo, você definiria ProductKey como a coluna de chave para uma dimensão de Produto.  
  
 Opcionalmente, você pode definir uma coluna que contém o nome do membro. Por padrão, o nome do membro que será exibido aos usuários é o valor da coluna de chave. Os valores em uma coluna de chave, como ProductID ou EmployeeID, são muitas vezes chaves exclusivas, geradas pelo sistema, que não tem sentido para o usuário. Muitas vezes você pode fornecer informações significativas ao usuário se alterar o nome que os usuários veem em um valor correspondente em uma ou outra coluna na dimensão. Por exemplo, você pode definir uma coluna de nome de membro que contém nomes de produto ou de funcionário. Se você alterar o nome do membro, os usuários podem ver um nome mais descritivo, mas as consultas ainda usam os valores de coluna de chave para distinguir corretamente os membros que compartilham o mesmo nome. Se você especificar uma chave composta para a coluna de chave, também precisará especificar a coluna que fornece os valores de membro para o atributo de chave. Para obter mais informações sobre como configurar as propriedades do atributo, consulte [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## Selecionando tabelas relacionadas  
  
> [!NOTE]  
>  O assistente ignora este passo se a tabela principal de dimensão não tiver nenhuma relação definida na exibição da fonte de dados com outras tabelas de dimensão.  
  
 Se você estiver criando uma dimensão floco de neve, especifique as tabelas relacionadas de onde serão definidos atributos adicionais na página **Selecionar Tabelas Relacionadas**. Por exemplo, você está criando uma dimensão de cliente onde você quer definir uma tabela de geografia de cliente. Nesse caso, é possível definir uma tabela de geografia como uma tabela relacionada.  
  
## Selecionando atributos de dimensão  
 Depois de selecionar as tabelas de dimensão, use a página **Selecionar Atributos de Dimensão** para selecionar os atributos que você quer incluir na dimensão por meio destas tabelas. Todas as colunas subjacentes de todas essas tabelas estão disponíveis como atributos potenciais de dimensão. O atributo de chave de dimensão deve ser selecionado e habilitado para procura.  
  
 Por padrão, o assistente define o tipo de um atributo como **Regular**. Entretanto, convém mapear atributos específicos para um tipo de atributo diferente que melhor represente os dados. Por exemplo, a tabela dbo.DimAccount do banco de dados de exemplo [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW contém uma coluna AccountCodeAlternateKey que fornece o número da conta. Em vez de definir o tipo como **Regular** para esse atributo, convém mapear o atributo para o tipo **Número de Conta**.  
  
> [!NOTE]  
>  Se o tipo de dimensão e os tipos de atributo padrão não forem definidos quando você criar a dimensão, use o Assistente de Business Intelligence para definir estes valores depois que criar a dimensão. Para obter mais informações, consulte [Adicionar inteligência de dimensão a uma dimensão](../../analysis-services/multidimensional-models/add-dimension-intelligence-to-a-dimension.md) ou (para uma dimensão do tipo Contas) [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
 O assistente define o tipo de dimensão automaticamente com base nos tipos de atributo especificados. Os tipos de atributo especificados no assistente definem a propriedade **Tipo** dos atributos. As configurações de propriedade **Tipo** para a dimensão e seus atributos fornecem informações sobre o conteúdo de uma dimensão para aplicativos cliente e servidor. Em alguns casos, essas configurações de propriedade **Tipo** somente fornecem orientação para aplicativos cliente e são opcionais. Em outros casos, como para dimensões de Contas, Tempo ou Moeda, essas configurações de propriedade **Tipo** determinam um comportamento específico baseado em servidor e são necessárias para implementar alguns comportamentos de cubo.  
  
 Para obter mais informações sobre tipos de dimensões e atributos, consulte [Tipos de dimensão](../Topic/Dimension%20Types.md) e [Configurar tipos de atributo](../../analysis-services/multidimensional-models/configure-attribute-types.md).  
  
## Definindo inteligência de conta  
  
> [!NOTE]  
>  O Assistente para Dimensões mostrará esta etapa somente se você tiver definido um atributo de dimensão de **Tipo de Conta** na página **Selecionar Atributos de Dimensão** do assistente.  
  
 Use a página **Definir Inteligência de Conta** para criar uma dimensão de tipo de Conta. Se estiver criando uma dimensão de tipo de Conta, você terá que mapear tipos de conta padrão com suporte por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para membros do atributo de tipo de conta na dimensão. O servidor usa esses mapeamentos para fornecer funções de agregação e aliases separados para cada tipo de dados de conta.  
  
 Para mapear esses tipos de conta, o assistente fornece uma tabela com as seguintes colunas:  
  
-   A coluna **Tipos de Conta de Tabela de Origem** lista de tipos de conta da tabela de fonte de dados.  
  
-   A coluna **Tipos de Conta Interna** lista os tipos de conta padrão correspondentes com suporte pelo servidor. Se os dados de origem usarem nomes padrão, o assistente mapeará automaticamente o tipo de origem para o tipo de servidor e populará a coluna **Tipos de Conta Interna** com essas informações. Se o servidor não mapear os tipos de conta ou se você quiser alterar o mapeamento, selecione um tipo diferente da lista na coluna **Tipos de Conta Interna**.  
  
> [!NOTE]  
>  Se os tipos de conta não forem mapeados quando o assistente criar uma dimensão de Contas, use o Assistente de Business Intelligence para configurar esses mapeamentos depois que você criar a dimensão. Para obter mais informações, consulte [Adicionar inteligência de conta a uma dimensão](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Concluindo o assistente  
 O assistente examina as tabelas de dimensão para detectar as relações. Ele cria automaticamente as relações de atributo entre os atributos de chave em dimensões floco de neve.  
  
 O assistente também detecta automaticamente se existe uma relação pai-filho na dimensão. Uma relação pai-filho existe quando um atributo pai faz referência a membros do atributo de chave da dimensão. Essa relação define relações hierárquicas e caminhos de agregação entre membros folha da dimensão. Para obter mais informações sobre hierarquias pai-filho, consulte [Atributos em hierarquias pai-filho](../../analysis-services/multidimensional-models/attributes-in-parent-child-hierarchies.md).  
  
 Na página **Concluindo o Assistente**, você conclui o assistente digitando um nome para a nova dimensão e revisando a estrutura da dimensão.  
  
## Consulte também  
 [Criar uma dimensão ao gerar uma tabela que não seja de tempo na fonte de dados](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [Criar uma dimensão de tempo ao gerar uma tabela de tempo](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Referência de propriedades de atributo de dimensão](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Criar uma dimensão de tempo ao gerar uma tabela de tempo](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Criar uma dimensão ao gerar uma tabela que não seja de tempo na fonte de dados](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  