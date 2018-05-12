---
title: Definindo dados de um fonte de exibição (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6966a0763146c9fd787be39d5be011704c048f66
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="defining-a-data-source-view-analysis-services"></a>Definindo uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma exibição de fonte de dados, contém o modelo lógico do esquema usado pelos objetos do banco de dados multidimensionais do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — ou seja, cubos, dimensões e estruturas de mineração de dados. Uma exibição de fonte de dados é a definição de metadados, armazenada no formato XML, dos elementos de esquema usados pelo modelo UDM (Unified Dimensional Model) e por estruturas de mineração de dados. Uma exibição da fonte de dados:  
  
-   Contém os metadados que representam os objetos selecionados, de uma ou mais fontes de dados subjacentes, ou os metadados que serão usados para gerar um armazenamento de dados relacional subjacente se você estiver seguindo a abordagem de cima para baixo para a geração de esquemas.  
  
-   Pode ser criado sobre uma ou mais fontes de dados, permitindo definir objetos multidimensionais e de mineração de dados que integram dados de várias fontes.  
  
-   Pode conter relações, chaves primárias, nomes de objetos, colunas calculadas e consultas que não estão presentes em uma fonte de dados subjacente e que existem separadamente das fontes de dados subjacentes.  
  
-   Não está visível ou disponível para consulta por aplicativos cliente.  
  
 Um DSV é um componente necessário de um modelo multidimensional. A maioria dos desenvolvedores do Analysis Services cria um DSV durante as etapas iniciais do design de modelo, gerando pelo menos um DSV com base em um banco de dados relacional externo que fornece dados subjacentes. No entanto, você também pode criar o DSV em uma etapa posterior, gerando as estruturas de esquema e banco de dados subjacentes depois que as dimensões e os cubos são criados. Essa segunda abordagem é chamada às vezes de design hierárquico e é usado com frequência na criação de protótipos e modelagem de análise. Quando você usar esta abordagem, usará o Assistente de Geração de Esquema para criar a exibição de fonte de dados subjacente e os objetos de fonte de dados baseados nos objetos OLAP definidos em um projeto ou banco de dados do Analysis Services. Independentemente de como e quando você cria um DSV, todo modelo deve ter um antes de você poder processá-lo.  
  
 Este tópico inclui as seguintes seções:  
  
 [Composição de uma exibição da fonte de dados](#bkmk_dsvdef)  
  
 [Criar um DSV usando o Assistente de Exibição da Fonte de Dados](#bkmk_startWiz)  
  
 [Especificar critérios de correspondência de nomes para relações](#bkmk_NameMatch)  
  
 [Adicionar uma fonte de dados secundária](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> Composição de uma exibição da fonte de dados  
 A exibição da fonte de dados contém:  
  
-   Um nome e uma descrição.  
  
-   Uma definição de cada subconjunto do esquema recuperado a partir de uma ou mais fontes de dados, até o esquema inteiro, incluindo:  
  
    -   Nomes de tabela.  
  
    -   Nomes de coluna.  
  
    -   Tipos de dados.  
  
    -   Nulidade.  
  
    -   Comprimentos de coluna.  
  
    -   Chaves primárias.  
  
    -   Relações entre chaves primária–estrangeira.  
  
-   Anotações para o esquema extraídas das fontes de dados subjacentes, incluindo:  
  
    -   Nomes amigáveis para tabelas, exibições e colunas.  
  
    -   Consultas nomeadas que retornam colunas de uma ou mais fontes de dados (mostradas como tabelas no esquema).  
  
    -   Cálculos nomeados que retornam colunas de uma fonte de dados (mostradas como colunas nas tabelas ou exibições).  
  
    -   As chaves primárias lógicas (necessárias se a chave primária não foi definida na tabela subjacente ou se ela não foi incluída na exibição ou na consulta nomeada).  
  
    -   Relações lógicas entre as chaves primária-estrangeira entre tabelas, exibições e consultas nomeadas.  
  
##  <a name="bkmk_startWiz"></a> Criar um DSV usando o Assistente de Exibição da Fonte de Dados  
 Para criar um DSV, execute o Assistente de Exibição da Fonte de Dados do Gerenciador de Soluções no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
> [!NOTE]  
>  Como alternativa, você pode construir dimensões e cubos primeiro e, em seguida, gerar um DSV para o modelo usando o Assistente de Geração de Esquema. Para obter mais informações, consulte [Assistente de Geração de Esquema &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md).  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Exibições da Fonte de Dados e, em seguida, clique em **Nova Exibição da Fonte de Dados**.  
  
2.  Especifique um novo objeto de fonte de dados ou um existente que fornece informações de conexão para um banco de dados relacional externo (você só pode selecionar uma fonte de dados no assistente).  
  
3.  Na mesma página, clique em **Avançado** para escolher esquemas específicos, aplicar um filtro ou excluir informações de relação de tabelas.  
  
     **Escolher esquemas**  
  
     Para fontes de dados muito grandes que contêm vários esquemas, você pode selecionar quais esquemas usar em uma lista delimitada por vírgulas, sem espaços.  
  
     **Recuperar relações**  
  
     Você pode omitir propositadamente informações de relações de tabelas desmarcando a caixa de seleção **Recuperar relações** na caixa de diálogo Opções Avançadas de Exibição da Fonte de Dados, permitindo criar manualmente relações entre tabelas no Designer de Exibição da Fonte de Dados.  
  
4.  **Filtrar objetos disponíveis**  
  
     Se a lista de objetos disponíveis contiver um número muito grande de objetos, você poderá reduzir a lista aplicando um filtro simples que especifica uma cadeia de caracteres como critérios de seleção. Por exemplo, se você digitar **dbo** e clicar no botão **Filtro** , somente os itens que começam com "dbo" aparecerão na lista **Objetos disponíveis** . O filtro pode ser uma cadeia de caracteres parcial (por exemplo, "sal" retorna vendas e salário) mas não pode incluir várias cadeias de caracteres ou operadores.  
  
5.  Para fontes de dados relacionais que não têm relações de tabelas definidas, uma página **Correspondência de Nomes** é exibida de modo que você possa selecionar o método de correspondência de nome apropriado. Para obter mais informações, consulte a seção [Especificar critérios de correspondência de nomes para relações](#bkmk_NameMatch) neste tópico.  
  
##  <a name="bkmk_secondaryDS"></a> Adicionar uma fonte de dados secundária  
 Ao definir uma exibição da fonte de dados que contenha tabelas, exibições ou colunas extraídas de diversas fontes de dados, a primeira fonte de dados a partir da qual você adiciona objetos é designada como fonte de dados principal (não é possível alterar a fonte de dados principal após sua definição). Depois de definir a exibição da fonte de dados com base nos objetos de uma única fonte de dados, você poderá adicionar objetos de outras fontes de dados.  
  
 Se um processamento OLAP ou uma consulta de mineração de dados precisar de várias fontes de dados em uma mesma consulta, a fonte de dados principal deverá oferecer suporte a consultas remotas usando **OpenRowset**. Normalmente, será uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, se você criar uma dimensão OLAP que contenha atributos associados a colunas de várias fontes de dados, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] construirá uma consulta **OpenRowset** para preencher essa dimensão durante o processamento. No entanto, se um objeto OLAP puder ser preenchido ou uma consulta de mineração de dados puder ser resolvida com uma única fonte de dados, a consulta **OpenRowset** não será construída. Em determinadas situações, pode ser possível definir relações de atributo entre os atributos para eliminar a necessidade de uma consulta **OpenRowset** . Para obter mais informações sobre relações de atributo, consulte [Relações de atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md), [Como adicionar ou remover tabelas ou exibições em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) e [Definir relações de atributo](../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
 Para adicionar tabelas e colunas de uma segunda fonte de dados, você clica duas vezes no DSV no Gerenciador de Soluções para abri-lo no Designer de exibição da fonte de dados e, em seguida, use a caixa de diálogo Adicionar/Remover Tabelas para incluir objetos de outras fontes de dados que são definidas em seu projeto. Para obter mais informações, consulte [Como adicionar ou remover tabelas ou exibições em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md).  
  
##  <a name="bkmk_NameMatch"></a> Especificar critérios de correspondência de nomes para relações  
 Quando você cria um DSV, são criadas relações entre as tabelas a partir das restrições de chave estrangeira da fonte de dados. Essas relações são necessárias para que o mecanismo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] construa o processamento OLAP apropriado e as consultas de mineração de dados. Entretanto, às vezes, uma fonte de dados com várias tabelas não tem nenhuma restrição de chave estrangeira. Se a fonte de dados não tiver restrições de chave estrangeira, o Assistente de Exibição da Fonte de Dados pedirá que você defina como quer que o assistente tente fazer a correspondência entre os nomes de colunas de tabelas diferentes.  
  
> [!NOTE]  
>  Será solicitada a especificação dos critérios de correspondência de nomes apenas se não forem detectadas relações de chave estrangeira na fonte de dados subjacente. Se forem detectadas relações de chave estrangeira, elas serão utilizadas e você terá que definir manualmente qualquer outra relação adicional que deseje incluir na DSV, incluindo chaves primárias lógicas. Para obter mais informações, consulte [Definir relações lógicas em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md) e [Definir chaves primárias lógicas em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md).  
  
 O Assistente de Exibição da Fonte de Dados usa sua resposta para fazer a correspondência entre os nomes de colunas e criar relações entre as tabelas diferentes na DSV. Você pode especificar qualquer um dos critérios listados na tabela a seguir.  
  
|Critérios de correspondência de nomes|Description|  
|----------------------------|-----------------|  
|**Mesmo nome que a chave primária**|O nome da coluna de chave estrangeira da tabela de origem é igual ao nome da coluna de chave primária da tabela de destino. Por exemplo, a coluna de chave estrangeira `Order.CustomerID` é igual à coluna de chave primária `Customer.CustomerID`.|  
|**Mesmo nome que a tabela de destino**|O nome da coluna de chave estrangeira da tabela de origem é igual ao nome da tabela de destino. Por exemplo, a coluna de chave estrangeira `Order.Customer` é igual à coluna de chave primária `Customer.CustomerID`.|  
|**Nome da tabela de destino + nome de chave primária**|O nome da coluna de chave estrangeira da tabela de origem é igual ao nome da tabela de destino concatenado com o nome da coluna de chave primária. É permitido o uso de espaço ou sublinhado como separador. Por exemplo, os pares de chave primária-estrangeira a seguir são correspondentes:<br /><br /> `Order.CustomerID` e `Customer.ID`<br /><br /> `Order.Customer ID` e `Customer.ID`<br /><br /> `Order.Customer_ID` e `Customer.ID`|  
  
 Os critérios selecionados alteram a configuração da propriedade **NameMatchingCriteria** da DSV. Essa configuração determina como o assistente adiciona tabelas relacionadas. Quando você altera a exibição da fonte de dados usando o Designer de Exibição da Fonte de Dados, essa especificação determina como o designer deve fazer a correspondência das colunas para criar relações entre as tabelas na DSV. Você pode alterar a configuração da propriedade **NameMatchingCriteria** no Designer de Exibição da Fonte de Dados. Para obter mais informações, consulte [Alterar propriedades em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Depois de concluir o Assistente de Exibição da Fonte de Dados, você pode adicionar ou remover relações no painel de esquemas do Designer de Exibição da Fonte de Dados. Para obter mais informações, consulte [Definir relações lógicas em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como adicionar ou remover tabelas ou exibições em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [Definir chaves primárias lógicas em uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [Definir cálculos nomeados em uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Definir consultas nomeadas em uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)   
 [Substituir uma tabela ou uma consulta nomeada em uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [Trabalhar com diagramas em Designer de exibição de fonte de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [Explorar dados em uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)   
 [Excluir uma exibição da fonte de dados &#40;do Analysis Services&#41;](../../analysis-services/multidimensional-models/delete-a-data-source-view-analysis-services.md)   
 [Atualizar o esquema em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  
