---
title: Conceder acesso personalizado a dados de dimensão (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.dimensiondata.f1
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67bbc67db06e05a0f6a02f8e9efd8dcc46441aeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075059"
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Conceder acesso personalizado a dados da dimensão (Analysis Services)
  Após habilitar o acesso de leitura a um cubo, você pode definir permissões adicionais que permitem ou negam explicitamente o acesso a membros de dimensão (incluindo as medidas contidas na dimensão de medidas que contém todas as medidas usadas em um cubo). Por exemplo, considerando várias categorias de revendedores, você pode querer definir as permissões para excluir dados de um tipo de negócio específico. A ilustração a seguir mostra o antes e o depois da negação de acesso ao tipo de negócio Depósito na dimensão do Revendedor.  
  
 ![Tabelas dinâmicas com e sem um membro de dimensão](../media/ssas-permsdimdenied.png "Tabelas dinâmicas com e sem um membro de dimensão")  
  
 Por padrão, se você pode ler dados de um cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você automaticamente tem permissões de leitura sobre todos os membros da dimensão e medidas associados a esse cubo. Embora esse comportamento possa ser suficiente para muitos cenários, às vezes, os requisitos de segurança exigem uma estratégia de autorização mais segmentada, com níveis variáveis de acesso para usuários diferentes, na mesma dimensão.  
  
 Você pode restringir o acesso ao escolher a quais membros permitirá (AllowedSet) ou negará (DeniedSet) acesso. Você pode fazer isso marcando ou desmarcando os membros de dimensão a serem incluídos ou excluídos da função.  
  
 A segurança básica de dimensão é a mais fácil, uma vez que basta selecionar quais atributos de dimensão e hierarquias de atributo devem ser incluídas ou excluídas da função. A segurança avançada é mais complexa e exige conhecimentos em scripts MDX. Veja abaixo a descrição das duas abordagens.  
  
## <a name="prerequisites"></a>Prerequisites  
 Nem todos os membros de medidas ou dimensão podem ser usados ​​em cenários de acesso personalizados. A conexão irá falhar se uma função restringir o acesso a uma medida ou membro padrão ou restringir o acesso a medidas que fazem parte de expressões de medida.  
  
 **Verificar se há obstruções na segurança da dimensão: medidas padrão, membros padrão e medidas usadas em expressões de medida**  
  
1.  Em SQL Server Management Studio, clique com o botão direito do mouse em um cubo e selecione **cubo de script como** | **alterar para** | **nova janela do editor de consultas**.  
  
2.  Procure `DefaultMeasure`. Encontre um para o cubo e um para cada perspectiva. Ao definir a segurança de dimensão, evite restringir o acesso a medidas padrão.  
  
3.  Em seguida, procure a `MeasureExpression`. A expressão de medida é baseada em um cálculo que inclui frequentemente outras medidas. Verifique se a medida que deseja restringir não foi usada em uma expressão. Como alternativa, restrinja o acesso, apenas certifique-se de também excluir qualquer referência a essa medida no cubo.  
  
4.  Por fim, procure o `DefaultMember`. Anote todos os atributos que servem como membro padrão de um atributo. Evite colocar restrições sobre esses atributos ao configurar a segurança de dimensão.  
  
## <a name="basic-dimension-security"></a>Segurança básica de dimensão  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
     A função já deve ter acesso de leitura para o cubo. Consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) se precisar de ajuda com esta etapa.  
  
2.  Em **dimensão de dados** | **básico**, selecione a dimensão para a qual você está definindo permissões.  
  
3.  Escolha a hierarquia de atributo. Nem todos os atributos estarão disponíveis. Apenas os atributos que têm **AttributeHierarchyEnabled** aparecem na lista **Hierarquia de Atributo** .  
  
4.  Escolha à quais membros permitirá ou negará acesso. Permitir o acesso pela opção **Selecionar todos os membros** é o padrão. Sugerimos que você mantenha esse padrão e exclua individualmente os membros que não devem ser visíveis para as contas de usuário e de grupo do Windows no painel **Associações** por meio dessa função. A vantagem é que os novos membros adicionados nas operações de processamento futuras estarão automaticamente disponíveis para as pessoas que se conectarem por meio dessa função.  
  
     Como alternativa, você pode **Cancelar seleção de todos os membros** para revogar o acesso geral e, em seguida, escolher os membros que receberão a permissão. Nas futuras operações de processamento, os novos membros não serão visíveis até que você edite manualmente a segurança dos dados de dimensão para permitir o acesso a eles.  
  
5.  Opcionalmente, clique em **avançado** para `Visual Totals` habilitar essa hierarquia de atributo. Essa opção recalcula as agregações com base nos membros disponíveis por meio da função.  
  
    > [!NOTE]  
    >  Ao aplicar permissões que cortam membros de dimensão, os totais agregados não são recalculados automaticamente. Suponha que `All` o membro de uma hierarquia de atributo retorne uma contagem de 200 antes que as permissões sejam aplicadas. Depois de aplicar permissões que negam acesso a alguns `All` Membros, o ainda retorna 200, embora os valores de membro visíveis para o usuário sejam muito menos. Para evitar a confusão dos consumidores do seu cubo, você pode configurar `All` o membro como o agregado apenas dos membros aos quais os membros da função, em vez da agregação de todos os membros da hierarquia de atributo. Para invocar esse comportamento, você pode `Visual Totals` habilitar na guia **avançado** ao configurar a segurança da dimensão. Uma vez habilitada, a agregação é calculada na hora da consulta, em vez de recuperada de agregações pré-calculadas. Isso pode ter um efeito significativo no desempenho da consulta, portanto, use-a somente quando necessário.  
  
## <a name="hiding-measures"></a>Ocultar medidas  
 No [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md), foi explicado que ocultar completamente todos os aspectos visuais de uma medida, e não apenas os seus dados de célula, requer permissões dos membros de dimensão. Esta seção explica como negar o acesso aos metadados do objeto de uma medida.  
  
1.  Na **dimensão dados** | **básicos**, role para baixo na lista dimensão até alcançar as dimensões do cubo e selecione **medir dimensão**.  
  
2.  Na lista de medidas, desmarque a caixa de seleção das medidas que não devem aparecer para usuários que se conectam por meio dessa função.  
  
> [!NOTE]  
>  Verifique os pré-requisitos para saber identificar as medidas que podem interromper a segurança da função.  
  
## <a name="advanced-dimension-security"></a>Segurança de dimensão avançada  
 Se você tiver conhecimentos em MDX, outra abordagem possível é escrever expressões MDX que definem os critérios para quais membros será permitido ou negado o acesso. Clique em criar dimensão de **função** | **dados** | **avançados** para fornecer o script.  
  
 Você pode usar o Construtor MDX para escrever a instrução MDX. Consulte [Construtor MDX&#40;Analysis Services – Dados Multidimensionais&#41;](../mdx-builder-analysis-services-multidimensional-data.md) para ver os detalhes. A guia **Avançado** contém as seguintes opções:  
  
 **Attribute**  
 Selecione o atributo do qual você deseja gerenciar segurança de membro.  
  
 **Conjunto de membros permitido**  
 O AllowedSet pode determinar nenhum membro (padrão), todos ou alguns membros. Se você permitir acesso a um atributo e não definir nenhum membro do conjunto permitido, será concedido acesso a todos os membros. Se você permitir acesso a um atributo e definir um conjunto específico de membros de atributo, apenas os membros explicitamente permitidos ficarão visíveis.  
  
 Criar um AllowedSet gera um efeito dominó quando o atributo participa de uma hierarquia de vários níveis. Por exemplo, suponha que uma função permita o acesso ao estado de Washington (imagine um cenário em que a função está concedendo permissões para a divisão de vendas do estado de Washington de uma empresa). Para as pessoas que se conectam por meio dessa função, as consultas que incluem ancestrais (Estados Unidos) ou descendentes (Seattle e Redmond) só verão os membros em uma cadeia incluindo o estado de Washington. Como os outros estados não são explicitamente permitidos, o efeito será o mesmo que se eles fossem negados.  
  
> [!NOTE]  
>  Se você definir um conjunto vazio ({}) de membros de atributo, nenhum membro do atributo será visível para a função de banco de dados. A ausência de um conjunto permitido não é interpretada como um conjunto vazio.  
  
 **Conjunto de membros negado**  
 A propriedade DeniedSet pode determinar nenhum membro, todos os membros (padrão) ou alguns membros de atributo. Quando o conjunto negado contiver apenas um conjunto específico de membros de atributo, a função de banco de dados tem o acesso negado apenas a esses membros específicos, bem como a descendentes se o atributo estiver em uma hierarquia de vários níveis. Considere o exemplo da divisão de vendas do estado de Washington. Se Washington for colocado em DeniedSet, as pessoas que se conectam por meio desse papel verão todos os outros estados, exceto Washington e seus atributos descendentes.  
  
 Lembre-se da seção anterior que o conjunto negado é uma coleção fixa. Se o processamento introduzir posteriormente novos membros, aos quais também deve ser negado o acesso, será preciso editar essa função para adicionar esses membros à lista.  
  
 **Membro padrão**  
 A propriedade DefaultMember determina o conjunto de dados retornado a um cliente quando um atributo não for incluído explicitamente em uma consulta. Quando o atributo não é incluído explicitamente, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa um dos seguintes membros padrão para o atributo:  
  
-   Se a função de banco de dados definir um membro padrão para o atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará esse membro padrão.  
  
-   Se a função de banco de dados não definir um membro padrão para o atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o membro padrão que está definido para o próprio atributo. O membro padrão para um atributo, a menos que você especifique algo diferente, é o membro `All` (a menos que o atributo esteja definido como não agregável).  
  
 Por exemplo, suponha que uma função de banco de dados especifica `Male` como o membro padrão para o atributo `Gender`. A menos que uma consulta inclua explicitamente o atributo `Gender` e especifique um membro diferente para esse atributo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará um conjunto de dados que incluirá apenas clientes masculinos. Para obter mais informações sobre como definir o membro padrão, consulte [Definir um membro padrão](attribute-properties-define-a-default-member.md).  
  
 **Habilitar total Visual**  
 A propriedade VisualTotals indica se os valores da célula agregada exibidos são calculados de acordo com todos os valores de célula ou só de acordo com os valores da células visíveis à função de banco de dados.  
  
 Por padrão, a propriedade VisualTotals é desabilitada (definida `False`como). Essa configuração padrão maximiza o desempenho porque o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode calcular rapidamente o total de todos os valores da célula, em vez de ter que passar tempo selecionando quais valores de células deverão ser calculados.  
  
 Porém, ter a propriedade VisualTotals desabilitada poderá criar um problema de segurança se um usuário puder usar os valores de célula agregada para deduzir valores para membros de atributo para os quais a função de banco de dados do usuário não tem acesso. Por exemplo, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa os valores para três membros de atributo calcularem um valor de célula agregada. A função de banco de dados tem acesso para exibir dois desses três membros de atributo. Usando o valor de célula agregada, um membro dessa função de banco de dados poderia deduzir o valor para o terceiro membro de atributo.  
  
 A definição da propriedade `True` VisualTotals como pode eliminar esse risco. Ao habilitar a propriedade VisualTotals, uma função de banco de dados pode exibir apenas totais agregados de membros de dimensão para os quais a função tem permissão.  
  
 **Verificação**  
 Clique para testar a sintaxe MDX definida nesta página.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)   
 [Conceder permissões em estruturas e modelos de Data Mining &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder permissões em um objeto de fonte de dados &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
