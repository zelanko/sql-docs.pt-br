---
title: "Conceder acesso personalizado a dados de dimensão (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.roledesignerdialog.dimensiondata.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- AllowedSet property
- IsAllowed property
- DeniedSet property
- user access rights [Analysis Services], dimensions
- custom dimension data access [Analysis Services]
- permissions [Analysis Services], dimensions
- DefaultMember property
- VisualTotals property
- ApplyDenied property
ms.assetid: b028720d-3785-4381-9572-157d13ec4291
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6cf115e0e7c931dd4e0b173b937a476cd08635df
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Conceder acesso personalizado a dados da dimensão (Analysis Services)
  Após habilitar o acesso de leitura a um cubo, você pode definir permissões adicionais que permitem ou negam explicitamente o acesso a membros de dimensão (incluindo as medidas contidas na dimensão de medidas que contém todas as medidas usadas em um cubo). Por exemplo, considerando várias categorias de revendedores, você pode querer definir as permissões para excluir dados de um tipo de negócio específico. A ilustração a seguir mostra o antes e o depois da negação de acesso ao tipo de negócio Depósito na dimensão do Revendedor.  
  
 ![Tabelas dinâmicas com e sem um membro de dimensão](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "tabelas dinâmicas com e sem um membro de dimensão")  
  
 Por padrão, se você pode ler dados de um cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você automaticamente tem permissões de leitura sobre todos os membros da dimensão e medidas associados a esse cubo. Embora esse comportamento possa ser suficiente para muitos cenários, às vezes, os requisitos de segurança exigem uma estratégia de autorização mais segmentada, com níveis variáveis de acesso para usuários diferentes, na mesma dimensão.  
  
 Você pode restringir o acesso ao escolher a quais membros permitirá (AllowedSet) ou negará (DeniedSet) acesso. Você pode fazer isso marcando ou desmarcando os membros de dimensão a serem incluídos ou excluídos da função.  
  
 A segurança básica de dimensão é a mais fácil, uma vez que basta selecionar quais atributos de dimensão e hierarquias de atributo devem ser incluídas ou excluídas da função. A segurança avançada é mais complexa e exige conhecimentos em scripts MDX. Veja abaixo a descrição das duas abordagens.  

> [!NOTE]  
>  As instruções a seguir pressupõem uma conexão de cliente que emite consultas MDX. Se o cliente usa o DAX, como o Power View no Power BI, a segurança de dimensão não fica evidente nos resultados da consulta. Consulte [Compreendendo o Power View para modelos multidimensionais](understanding-power-view-for-multidimensional-models.md) .para obter mais informações.
      
## <a name="prerequisites"></a>Pré-requisitos  
 Nem todos os membros de medidas ou dimensão podem ser usados ​​em cenários de acesso personalizados. A conexão irá falhar se uma função restringir o acesso a uma medida ou membro padrão ou restringir o acesso a medidas que fazem parte de expressões de medida.  
  
 **Verifique se há obstruções à segurança da dimensão: medidas padrão, membros padrão e medidas usados em expressões de medidas**  
  
1.  No SQL Server Management Studio, clique com o botão direito do mouse em um cubo e selecione **Aplicar script de Cubo como** | **ALTERAR para** | **Nova Janela do Editor de Consulta**.  
  
2.  Procure **DefaultMeasure**. Encontre um para o cubo e um para cada perspectiva. Ao definir a segurança de dimensão, evite restringir o acesso a medidas padrão.  
  
3.  Em seguida, procure a **MeasureExpression**. A expressão de medida é baseada em um cálculo que inclui frequentemente outras medidas. Verifique se a medida que deseja restringir não foi usada em uma expressão. Como alternativa, restrinja o acesso, apenas certifique-se de também excluir qualquer referência a essa medida no cubo.  
  
4.  Por fim, procure o **DefaultMember**. Anote todos os atributos que servem como membro padrão de um atributo. Evite colocar restrições sobre esses atributos ao configurar a segurança de dimensão.  
  
## <a name="basic-dimension-security"></a>Segurança básica de dimensão  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
     A função já deve ter acesso de leitura para o cubo. Consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) se precisar de ajuda com esta etapa.  
  
2.  Em **Dados de Dimensão** | **Básico**, selecione a dimensão para a qual você está definindo as permissões.  
  
3.  Escolha a hierarquia de atributo. Nem todos os atributos estarão disponíveis. Apenas os atributos que têm **AttributeHierarchyEnabled** aparecem na lista **Hierarquia de Atributo** .  
  
4.  Escolha à quais membros permitirá ou negará acesso. Permitir o acesso pela opção **Selecionar todos os membros** é o padrão. Sugerimos que você mantenha esse padrão e exclua individualmente os membros que não devem ser visíveis para as contas de usuário e de grupo do Windows no painel **Associações** por meio dessa função. A vantagem é que os novos membros adicionados nas operações de processamento futuras estarão automaticamente disponíveis para as pessoas que se conectarem por meio dessa função.  
  
     Como alternativa, você pode **Cancelar seleção de todos os membros** para revogar o acesso geral e, em seguida, escolher os membros que receberão a permissão. Nas futuras operações de processamento, os novos membros não serão visíveis até que você edite manualmente a segurança dos dados de dimensão para permitir o acesso a eles.  
  
5.  Como opção, clique em **Avançado** para habilitar os **Totais Visuais** para essa hierarquia de atributo. Essa opção recalcula as agregações com base nos membros disponíveis por meio da função.  
  
    > [!NOTE]  
    >  Ao aplicar permissões que cortam membros de dimensão, os totais agregados não são recalculados automaticamente. Suponha que o membro **Todos** de uma hierarquia de atributo retorne uma contagem de 200 antes das permissões serem aplicadas. Depois de aplicar as permissões que negam o acesso a alguns membros, **Todos** ainda retorna 200, embora os valores de membros visíveis para o usuário sejam muito menores. Para evitar confundir os consumidores de seu cubo, você pode configurar o membro **Todos** para agregar somente os membros aos quais os membros da função tenham acesso, em vez de agregar todos os membros da hierarquia de atributo. Para invocar esse comportamento, habilite **Visual Totals** na guia **Avançado** ao configurar a segurança de dimensão. Uma vez habilitada, a agregação é calculada na hora da consulta, em vez de recuperada de agregações pré-calculadas. Isso pode ter um efeito significativo no desempenho da consulta, portanto, use-a somente quando necessário.  
  
## <a name="hiding-measures"></a>Ocultar medidas  
 No [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md), foi explicado que ocultar completamente todos os aspectos visuais de uma medida, e não apenas os seus dados de célula, requer permissões dos membros de dimensão. Esta seção explica como negar o acesso aos metadados do objeto de uma medida.  
  
1.  Em **Dados de Dimensão** | **Básico**, role a lista Dimensão para baixo até chegar às dimensões do cubo e selecione **Dimensão de Medidas**.  
  
2.  Na lista de medidas, desmarque a caixa de seleção das medidas que não devem aparecer para usuários que se conectam por meio dessa função.  
  
> [!NOTE]  
>  Verifique os pré-requisitos para saber identificar as medidas que podem interromper a segurança da função.  
  
## <a name="advanced-dimension-security"></a>Segurança de dimensão avançada  
 Se você tiver conhecimentos em MDX, outra abordagem possível é escrever expressões MDX que definem os critérios para quais membros será permitido ou negado o acesso. Clique em **Criar Função** | **Dados de Dimensão** | **Avançado** para fornecer o script.  
  
 Você pode usar o Construtor MDX para escrever a instrução MDX. Consulte [Construtor MDX&#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f) para ver os detalhes. A guia **Avançado** contém as seguintes opções:  
  
 **Atributo**  
 Selecione o atributo do qual você deseja gerenciar segurança de membro.  
  
 **Conjunto de membros permitido**  
 O AllowedSet pode determinar nenhum membro (padrão), todos ou alguns membros. Se você permitir acesso a um atributo e não definir nenhum membro do conjunto permitido, será concedido acesso a todos os membros. Se você permitir acesso a um atributo e definir um conjunto específico de membros de atributo, apenas os membros explicitamente permitidos ficarão visíveis.  
  
 Criar um AllowedSet gera um efeito dominó quando o atributo participa de uma hierarquia de vários níveis. Por exemplo, suponha que uma função permita o acesso ao estado de Washington (imagine um cenário em que a função está concedendo permissões para a divisão de vendas do estado de Washington de uma empresa). Para as pessoas que se conectam por meio dessa função, as consultas que incluem ancestrais (Estados Unidos) ou descendentes (Seattle e Redmond) só verão os membros em uma cadeia incluindo o estado de Washington. Como os outros estados não são explicitamente permitidos, o efeito será o mesmo que se eles fossem negados.  
  
> [!NOTE]  
>  Se você definir um conjunto vazio ({}) de membros de atributo, nenhum membro do atributo ficará visível à função de banco de dados. A ausência de um conjunto permitido não é interpretada como um conjunto vazio.  
  
 **Conjunto de membros negado**  
 A propriedade DeniedSet pode determinar nenhum membro, todos os membros (padrão) ou alguns membros de atributo. Quando o conjunto negado contiver apenas um conjunto específico de membros de atributo, a função de banco de dados tem o acesso negado apenas a esses membros específicos, bem como a descendentes se o atributo estiver em uma hierarquia de vários níveis. Considere o exemplo da divisão de vendas do estado de Washington. Se Washington for colocado em DeniedSet, as pessoas que se conectam por meio desse papel verão todos os outros estados, exceto Washington e seus atributos descendentes.  
  
 Lembre-se da seção anterior que o conjunto negado é uma coleção fixa. Se o processamento introduzir posteriormente novos membros, aos quais também deve ser negado o acesso, será preciso editar essa função para adicionar esses membros à lista.  
  
 **Membro padrão**  
 A propriedade DefaultMember determina o conjunto de dados retornado a um cliente quando um atributo não for incluído explicitamente em uma consulta. Quando o atributo não é incluído explicitamente, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um dos seguintes membros padrão para o atributo:  
  
-   Se a função de banco de dados definir um membro padrão para o atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará esse membro padrão.  
  
-   Se a função de banco de dados não definir um membro padrão para o atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o membro padrão que está definido para o próprio atributo. O membro padrão para um atributo, a menos que você especifique algo diferente, é o membro **Tudo** (a menos que o atributo esteja definido como não agregável).  
  
 Por exemplo, suponha que uma função de banco de dados especifique **Male** como o membro padrão para o atributo **Gender** . A menos que uma consulta inclua explicitamente o atributo **Gênero** e especifique um membro diferente para esse atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará um conjunto de dados que incluirá apenas clientes masculinos. Para obter mais informações sobre como definir o membro padrão, consulte [Definir um membro padrão](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 **Habilitar Totais Visuais**  
 A propriedade VisualTotals indica se os valores da célula agregada exibidos são calculados de acordo com todos os valores de célula ou só de acordo com os valores da células visíveis à função de banco de dados.  
  
 Por padrão, a propriedade VisualTotals está desabilitada (definida como **False**). Essa configuração padrão maximiza o desempenho porque o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode calcular rapidamente o total de todos os valores da célula, em vez de ter que passar tempo selecionando quais valores de células deverão ser calculados.  
  
 Porém, ter a propriedade VisualTotals desabilitada poderá criar um problema de segurança se um usuário puder usar os valores de célula agregada para deduzir valores para membros de atributo para os quais a função de banco de dados do usuário não tem acesso. Por exemplo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa os valores para três membros de atributo calcularem um valor de célula agregada. A função de banco de dados tem acesso para exibir dois desses três membros de atributo. Usando o valor de célula agregada, um membro dessa função de banco de dados poderia deduzir o valor para o terceiro membro de atributo.  
  
 Definir a propriedade VisualTotals como **True** pode eliminar esse risco. Ao habilitar a propriedade VisualTotals, uma função de banco de dados pode exibir apenas totais agregados de membros de dimensão para os quais a função tem permissão.  
  
 **Verificar**  
 Clique para testar a sintaxe MDX definida nesta página.  
  
## <a name="see-also"></a>Consulte também  
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acesso personalizado a célula de dados &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [Conceder permissões em estruturas de mineração de dados e modelos de &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder permissões em um objeto de fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
