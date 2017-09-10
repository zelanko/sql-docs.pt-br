---
title: "Conceder acesso personalizado aos dados da célula (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb753663f77dbe9fae2eb37cce9a654bfa22f483
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>Conceder acesso personalizado a dados de célula (Analysis Services)
  A segurança da célula é usada para permitir ou negar acesso a dados de medida de um cubo. A ilustração a seguir mostra uma combinação de medidas permitidas e negadas em uma Tabela Dinâmica quando conectada por um usuário cuja função permite acessar apenas algumas medidas. Neste exemplo, **Valor de Vendas do Revendedor** e **Custo Total do Produto do Revendedor** são as únicas medidas disponíveis por meio dessa função. Todas as outras medidas são negadas implicitamente (as etapas usadas para obter esse resultado são fornecidas abaixo, na seção Permitir acesso a medidas específicas).  
  
 ![Tabela dinâmica mostrando células permitidas e negadas](../../analysis-services/multidimensional-models/media/ssas-permscellsallowed.png "tabela dinâmica mostrando células permitidas e negadas")  
  
 As permissões de célula aplicam-se a dados dentro da célula e não aos seus metadados. Observe como a célula ainda está visível nos resultados de uma consulta, exibindo um valor **#N/A** em vez do valor real da célula. O valor **#N/A** aparecerá na célula a menos que o aplicativo cliente converta o valor, ou outro valor seja especificado definindo a propriedade Secured Cell Value na cadeia de conexão.  
  
 Para ocultar a célula totalmente, limite os membros visíveis – dimensões, atributos de dimensão e membros do atributo de dimensão. Para obter mais informações, consulte [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md).  
  
 Como administrador, você pode especificar se os membros da função têm permissões de leitura, contingente de leitura ou de leitura/gravação nas células de um cubo. Colocar permissões em uma célula é o nível mais baixo de segurança permitido, por isso, antes de aplicar permissões neste nível, é importante considerar alguns fatos:  
  
-   A segurança no nível da célula não pode expandir os direitos que foram restritos em um nível superior. Um exemplo: se uma função negar acesso aos dados de dimensão, a segurança no nível da célula não poderá substituir o conjunto negado. Outro exemplo: considere uma função com permissão de **Leitura** em um cubo e permissão de **Leitura/Gravação** em uma célula – a permissão de dados da célula não será de **Leitura/Gravação**, e sim de **Leitura**.  
  
-   As permissões personalizadas muitas vezes precisam ser coordenadas entre os membros de dimensão e as células dentro da mesma função. Por exemplo, imagine que você queira negar o acesso a várias medidas relacionadas a desconto para diferentes combinações de revendedores. Considerando **Revendedores** como os dados da dimensão e **Valor de Desconto** como uma medida, você precisará combinar dentro das mesmas permissões de função na medida (usando as instruções deste tópico) e nos membros da dimensão. Consulte [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) para obter detalhes sobre como definir as permissões da dimensão.  
  
 A segurança no nível de célula é especificada por meio de expressões MDX. Como a célula é uma tupla (isto é, um ponto de intersecção entre várias dimensões e medidas potenciais), é necessário usar MDX para identificar células específicas.  
  
## <a name="allow-access-to-specific-measures"></a>Permitir acesso a medidas específicas  
 Você pode usar a segurança da célula para escolher explicitamente quais medidas estão disponíveis. Depois de identificar especificamente quais membros são permitidos, todas as outras medidas se tornam indisponíveis. Talvez esse seja o cenário mais simples para implantar por meio de script MDX, como mostram as etapas a seguir.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], escolha um banco de dados, abra a pasta **Funções** e clique em uma função de banco de dados (ou crie uma nova função de banco de dados). A associação já deve estar especificada e a função deve ter acesso de **Leitura** ao cubo. Consulte [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) se precisar de ajuda com esta etapa.  
  
2.  Em **Dados da Célula**, marque a seleção do cubo para ter certeza de ter escolhido o correto e selecione **Habilitar permissões de leitura**.  
  
     Se você marcar apenas esta caixa de seleção e não fornecer uma expressão MDX, o efeito é o mesmo que negar o acesso a todas as células no cubo. Isso acontece porque o conjunto padrão permitido é um conjunto vazio sempre que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina um subconjunto de células de cubo.  
  
3.  Insira a seguinte expressão MDX.  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     Essa expressão identifica explicitamente quais medidas são visíveis aos usuários. Nenhuma outra medida estará disponível para usuários que se conectarem com essa função. Observe que [CurrentMember &#40;MDX&#41;](../../mdx/currentmember-mdx.md) define o contexto e é seguido da medida permitida. O efeito dessa expressão, se o membro atual incluir o **Valor de Vendas do Revendedor** ou o **Custo Total do Produto do Revendedor**, será mostrar o valor. Caso contrário, negar o acesso. A expressão tem várias partes, com cada uma delas entre parênteses. O operador **OR** é usado para especificar várias medidas.  
  
## <a name="deny-access-to-specific-measures"></a>Negar acesso a medidas específicas  
 A expressão MDX a seguir, também especificada em **Criar Função** | **Dados da Célula** | **Permitir leitura do conteúdo do cubo**, tem o efeito oposto, tornando certas medidas indisponíveis. Neste exemplo, tornamos o **Valor de Desconto** e **Percentual de Desconto** indisponíveis usando os operadores **NOT** e **AND** . Todas as outras medidas estarão disponíveis para usuários que se conectarem por meio dessa função.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 No Excel, a segurança da célula é evidente na ilustração a seguir:  
  
 ![Colunas Excel exibindo células como não disponíveis](../../analysis-services/multidimensional-models/media/ssas-permscellshidemeasure.png "colunas Excel exibindo células como não disponíveis")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>Definir permissões de leitura em medidas calculadas  
 As permissões em uma medida calculada podem ser definidas de forma independente das suas partes constituintes. Vá para a próxima seção sobre Contingente de Leitura se quiser coordenar permissões entre uma medida calculada e suas medidas dependentes.  
  
 Para entender como as permissões de Leitura funcionam para uma medida calculada, considere **Lucro Bruto do Revendedor** no AdventureWorks. É derivado das medidas **Valor das Vendas do Revendedor** e **Custo Total do Produto do Revendedor** . Enquanto uma função tiver permissão de Leitura nas células **Lucro Bruto do Revendedor** , essa medida será visível, mesmo que as permissões sejam expressamente negadas nas outras medidas. Como demonstração, copie a expressão MDX a seguir em **Criar Função** | **Dados da Célula** | **Permitir leitura do conteúdo do cubo**.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 No Excel, conecte-se ao cubo usando a função atual e escolha as três medidas para ver os efeitos de segurança da célula. Observe que as medidas no conjunto negado não estão disponíveis, mas a medida calculada está visível para o usuário.  
  
 ![Tabela do Excel com disponíveis e cellls](../../analysis-services/multidimensional-models/media/ssas-permscalculatedcells.png "tabela do Excel com cellls disponíveis e não está disponível")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>Definir permissões de Contingente de Leitura em medidas calculadas  
 A segurança da célula oferece uma alternativa, Contingente de Leitura, para definir permissões nas células relacionadas que formam um cálculo. Considere novamente o exemplo **Lucro Bruto do Revendedor** . Quando você insere a mesma expressão MDX fornecida na seção anterior, colocada nesse momento na segunda área de texto da caixa de diálogo **Criar Função** | **Dados da Célula** (na área de texto abaixo **Permitir leitura do conteúdo da célula contingente na segurança da célula**), o resultado é aparente quando exibido no Excel. Como **Lucro Bruto do Revendedor** é contingente em relação a **Valor das Vendas do Revendedor** e **Custo Total do Produto do Revendedor**, o lucro bruto passa a ficar inacessível porque suas partes constituintes não podem ser acessadas.  
  
> [!NOTE]  
>  O que acontece se você definir as permissões de Leitura e Contingente de Leitura em uma célula dentro da mesma função? A função fornecerá permissões de Leitura na célula, e não de Contingente de Leitura.  
  
 Lembre-se das seções anteriores que marcar apenas a caixa de seleção **Habilitar permissões de contingente de leitura** , sem fornecer nenhuma expressão MDX, nega o acesso a todas as células do cubo. Isso acontece porque o conjunto padrão permitido é um conjunto vazio sempre que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina um subconjunto de células de cubo.  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>Definir permissão de Leitura/Gravação na célula  
 As permissões de Leitura/Gravação na célula são usadas para habilitar write-back, desde que os membros tenham permissões de leitura/gravação para o cubo. As permissões que são concedidas no nível de célula não podem ser maiores que as permissões que concedidas no nível de cubo. Consulte [Definir write-back de partição](../../analysis-services/multidimensional-models/set-partition-writeback.md) para obter detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Construtor MDX&#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f)   
 [O script básico de MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [Conceder permissões de processo &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)   
 [Conceder permissões em uma dimensão &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)   
 [Conceder acesso personalizado a dimensão de dados &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
  
