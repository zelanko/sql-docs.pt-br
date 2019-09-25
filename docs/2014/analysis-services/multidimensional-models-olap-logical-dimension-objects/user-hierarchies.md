---
title: Hierarquias de usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1192deaa556dd8546d0d9fbf17d5ff79335173a
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2019
ms.locfileid: "68887822"
---
# <a name="user-hierarchies"></a>Hierarquias do usuário
  As hierarquias definidas pelo usuário são hierarquias definidas pelo usuário de atributos que são usados [!INCLUDE[msCoName](../../includes/msconame-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para organizar os membros de uma dimensão em estruturas hierárquicas e fornecer caminhos de navegação em um cubo. Por exemplo, a tabela a seguir define uma tabela de dimensões para uma dimensão temporal. A tabela de dimensão oferece suporte para três atributos nomeados, Ano, Trimestre e Mês.  
  
|Year|Quarter|Month|  
|----------|-------------|-----------|  
|1999|1º Trimestre|Jan|  
|1999|1º Trimestre|Fev|  
|1999|1º Trimestre|Mar|  
|1999|2º Trimestre|Abr|  
|1999|2º Trimestre|Mai|  
|1999|2º Trimestre|Jun|  
|1999|3º Trimestre|Jul|  
|1999|3º Trimestre|Ago|  
|1999|3º Trimestre|Set|  
|1999|4º Trimestre|Oct|  
|1999|4º Trimestre|Nov|  
|1999|4º Trimestre|Dez|  
  
 São usados os atributos Ano, Trimestre e Mês para criar uma hierarquia definida pelo usuário, nomeado Calendário, na dimensão temporal. A relação entre os níveis e membros da dimensão Calendário (uma dimensão comum) é mostrada no diagrama a seguir.  
  
 ![Hierarquia de nível e membro para uma dimensão de tempo](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-levelconcepts.gif "Hierarquia de nível e membro para uma dimensão de tempo")  
  
> [!NOTE]  
>  Toda hierarquia diferente da hierarquia de atributo de dois níveis padrão é chamada de hierarquia definida pelo usuário. Para obter mais informações sobre hierarquias de atributo, consulte [atributos e hierarquias de atributo](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="member-structures"></a>Estruturas de membro  
 Com exceção das hierarquias pai-filho, as posições de membros dentro da hierarquia são controladas pela ordem dos atributos na definição de hierarquia. Cada atributo na definição de hierarquia constitui um nível na hierarquia. A posição de um membro dentro de um nível é determinada pela ordem do atributo usada para criar o nível. As estruturas de membro de hierarquias definidas pelo usuário podem ter uma de quatro formas básicas, dependendo de como os membros estão relacionados entre si.  
  
### <a name="balanced-hierarchies"></a>Hierarquias equilibradas  
 Em uma hierarquia equilibrada, todas as ramificações da hierarquia decrescem do mesmo nível e cada pai lógico do membro está no nível imediatamente acima do membro. A hierarquia Categorias de Produtos da dimensão Produto na amostra [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é um exemplo de hierarquia equilibrada. Cada membro no nível Nome do Produto tem um membro pai no nível Subcategoria que, por sua vez, tem um membro pai no nível Categoria. Além disso, toda ramificação na hierarquia tem um membro folha no nível Nome do Produto.  
  
### <a name="unbalanced-hierarchies"></a>Hierarquias desbalanceadas  
 Em uma hierarquia desbalanceada, ramificações da hierarquia decresce para níveis diferentes. As hierarquias pai-filho são hierarquias desbalanceadas. Por exemplo, a dimensão Organização na amostra [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contém um membro para cada funcionário. O CEO é o membro que ocupa o lugar no topo da hierarquia e os gerentes de divisão e secretária executiva estão imediatamente abaixo do CEO. Os gerentes de divisão têm membros subordinados, mas a secretária executiva não.  
  
 Pode ser impossível para usuários finais distinguirem entre hierarquias desbalanceadas e imperfeitas. Entretanto, você emprega técnicas e propriedades diferentes no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para oferecer suporte a esses dois tipos de hierarquias. Para obter mais informações, consulte [Hierarquias desbalanceadas](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md) e [atributos em hierarquias pai-filho](../multidimensional-models/parent-child-dimension-attributes.md).  
  
### <a name="ragged-hierarchies"></a>Hierarquias desbalanceadas  
 Em uma hierarquia imperfeita, o membro pai lógico de pelo menos um membro não está no nível imediatamente acima do membro. Isso pode fazer com que ramificações da hierarquia decresçam a níveis diferentes. Por exemplo, em uma dimensão Geografia definida com os níveis Continente, PaísRegião e Cidade, nessa ordem o membro Europa aparece no nível mais alto da hierarquia, o membro França aparece no nível intermediária e o membro Paris aparece no nível mais baixo. França é mais específico que a Europa e Paris é mais específico que França. Para essa hierarquia regular, as seguintes alterações são feitas:  
  
-   A Cidade do Vaticano é adicionada para o nível PaísRegião.  
  
-   Os membros são adicionados para o nível Cidade e são associados ao membro Cidade do Vaticano no nível de PaísRegião.  
  
-   Um nível, noemado Província, é adicionado entre os níveis PaísRegião e Cidade.  
  
 O nível Província é populado com membros associados a outros membros no nível PaísRegião e os membros no nível Cidade são associados a seus membros correspondentes no nível Província. Entretanto, como o membro Cidade do Vaticano no nível PaísRegião não possui membros associados no nível Província, os membros devem ser associados do nível Cidade diretamente ao membro Cidade do Vaticano no nível PaísRegião. Devido às alterações, a hierarquia da dimensão está agora imperfeita. O pai de Cidade do Vaticano é a região/país Cidade do Vaticano, que não está imediatamente no nível acima do membro Cidade do Vaticano no nível Cidade. Para obter mais informações, consulte [Hierarquias desbalanceadas](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
### <a name="parent-child-hierarchies"></a>Hierarquias pai-filho  
 As hierarquias pai-filho de dimensões são definidas usando um atributo especial, chamado de atributo pai, para determinar como os membros relacionam-se entre si. Um atributo pai descreve uma *relação de autorreferência*, ou *autojunção*, em uma tabela principal da dimensão. As hierarquias filho são construídas a partir de um único atributo pai. Somente um nível é atribuído a uma hierarquia pai-filho, pois os níveis existentes na hierarquia são extraídos das relações pai-filho entre os membros associados ao atributo pai. O esquema de dimensão de uma hierarquia pai-filho depende de uma relação de autorreferência existente na tabela principal da dimensão. Por exemplo, o diagrama a seguir ilustra a tabela principal de dimensões de **dimorganização** no banco de dados de [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] exemplo.  
  
 ![Junção de referência automática na tabela de Dimorganização](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimorganization.gif "Junção de referência automática na tabela de Dimorganização")  
  
 Nessa tabela de dimensão, a coluna **ParentOrganizationKey** possui uma relação de chave estrangeira com a coluna da chave primária **OrganizationKey** . Em outras palavras, cada registro dessa tabela pode ser relacionado por meio de uma relação pai-filho com outro registro da tabela. Geralmente, esse tipo de autojunção é usado para representar os dados de uma empresa, como a estrutura de gerenciamento dos funcionários de um departamento.  
  
 Quando você cria uma hierarquia pai-filho, as colunas representadas por ambos os atributos devem ter o mesmo tipo de dados. Ambos os atributos também devem estar na mesma tabela. Por padrão, todo membro cuja chave pai é igual à sua própria chave de membro, nulo, 0 (zero) ou um valor ausente da coluna para as chaves de membro, é assumido como um membro no nível mais alto (excluindo o nível Todos).  
  
 A profundidade de uma hierarquia pai-filho pode variar entre suas ramificações hierárquicas. Em outras palavras, uma hierarquia pai-filho é considerada uma hierarquia desbalanceada.  
  
 Diferentemente de hierarquias definidas pelo usuário, na qual o número de níveis na hierarquia determina o número de níveis que podem ser visualizados por usuários finais, uma hierarquia pai-filho é definida com o único nível de um atributo de hierarquia e os valores nesse único nível produzem os vários níveis visualizados por usuários. O número de níveis exibidos depende do conteúdo das colunas da tabela de dimensões que armazenam as chaves de membro e as chaves de pai. O número de níveis pode ser alterado quando os dados nas tabelas de dimensões alteram. Para obter mais informações, consulte [hierarquia pai-filho](../multidimensional-models/parent-child-dimension.md)e [atributos em hierarquias pai-filho](../multidimensional-models/parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Criar hierarquias definidas pelo usuário](../multidimensional-models/user-defined-hierarchies-create.md)   
 [Propriedades de hierarquia do usuário](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Referência de propriedades de atributo de dimensão](../multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
