---
title: Atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- free-form attributes [Master Data Services]
- attributes [Master Data Services], about attributes
- attributes [Master Data Services], file attributes
- file attributes [Master Data Services]
- attributes [Master Data Services], free-form attributes
- attributes [Master Data Services]
ms.assetid: 95ecb75f-c559-41c3-933c-40ae60a4c2fd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 88f1f0909e667db38c3b9b5d13bf11a2262b405b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480153"
---
# <a name="attributes-master-data-services"></a>Atributos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , atributos são objetos contidos em entidades. Os valores de atributos descrevem os membros da entidade. Um atributo pode ser usado para descrever um membro folha, um membro consolidado ou uma coleção.  
  
## <a name="how-attributes-relate-to-other-model-objects"></a>Como os atributos se relacionam com outros objetos modelo  
 Você pode pensar em um atributo como uma coluna em uma tabela de entidade. Um valor de atributo é o valor usado para descrever um membro específico.  
  
 ![Entidade de Master Data Services representada como tabela](../../2014/master-data-services/media/mds-conc-entity-table.gif "Entidade de Master Data Services representada como tabela")  
  
 Ao criar uma entidade que contém muitos atributos, você pode organizar os atributos em grupos de atributos. Para obter mais informações, consulte [Grupos de atributos &#40;Master Data Services&#41;](attribute-groups-master-data-services.md).  
  
## <a name="required-attributes"></a>Atributos necessários.  
 Quando você cria uma entidade, os atributos Name e Code são criados automaticamente. Code requer um valor e precisa ser exclusivo dentro da entidade. Não é possível remover os atributos Name e Code.  
  
## <a name="attribute-types"></a>Tipos de atributo  
 Há três tipos de atributos:  
  
-   Atributos de forma livre que permitem entrada de forma livre para texto, números, datas ou links.  
  
-   Atributos baseados em domínio que são populados por entidades. Para obter mais informações, consulte [Atributos baseados em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md).  
  
-   Atributos de arquivo, que são usados para armazenar arquivos, documentos ou imagens. A finalidade dos atributos de arquivo é ajudar na consistência dos seus dados ao exigir que os arquivos tenham uma extensão específica. Os atributos de arquivo não impedem que um usuário mal-intencionado carregue um arquivo de um tipo diferente.  
  
### <a name="numeric-free-form-attributes"></a>Atributos de forma livre numéricos  
 Os atributos de forma livre numéricos exigem tratamento especial, porque os valores de atributos de forma livre numéricos são limitados ao tipo de valor **SqlDouble** .  
  
 Por padrão, um valor **SqlDouble** contém 15 dígitos decimais de precisão, embora um máximo de 17 dígitos seja mantido interiormente. A precisão de um número de ponto flutuante tem várias consequências:  
  
-   Dois números de ponto flutuante que pareçam iguais para uma determinada precisão podem não ser comparados como iguais porque seus dígitos menos significantes são diferentes.  
  
-   Uma operação matemática ou de comparação que use um número de ponto flutuante talvez não produza o mesmo resultado se um número decimal for usado, porque o número de ponto flutuante pode não ser exatamente idêntico ao número decimal.  
  
-   Um valor poderá não fazer uma *viagem de ida e volta* se um número de ponto flutuante estiver envolvido. Diz-se que um valor faz uma viagem de ida e volta quando uma operação converte um número de ponto flutuante original para outra forma, uma operação inversa transforma a forma convertida de volta para um número de ponto flutuante e o número de ponto flutuante final é igual ao número de ponto flutuante original. A viagem de ida e volta pode falhar porque um ou mais dígitos menos significantes são perdidos ou alterados na conversão.  
  
## <a name="attribute-examples"></a>Exemplos de atributos  
 No exemplo a seguir, a entidade tem os atributos: Name, Code, Subcategory, StandardCost, ListPrice e FilePhoto. Esses atributos descrevem os membros, Cada membro é representado por uma única linha de valores de atributo.  
  
 ![Tabela da entidade de produto bicicleta](../../2014/master-data-services/media/mds-conc-entity-table-w-data.gif "Tabela da entidade de produto bicicleta")  
  
 No exemplo a seguir, a entidade Product contém:  
  
-   Os atributos de forma livre Name, Code, StandardCost e ListPrice.  
  
-   O atributo com base no domínio Subcategory.  
  
-   O atributo de arquivo FilePhoto.  
  
 Subcategory é uma entidade usada como atributo com base em domínio da entidade Product. Category é uma entidade usada como atributo com base em domínio de Subcategory. Assim como a entidade Product, as entidades Category e Subcategory contêm os atributos padrão Name e Code.  
  
 ![Estrutura de árvore de entidade de produto](../../2014/master-data-services/media/mds-conc-entity-ui.gif "Estrutura de árvore de entidade de produto")  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um novo atributo de texto de formato livre|[Criar um atributo de texto &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-text-attribute-master-data-services.md)|  
|Criar um novo atributo numérico de formato livre|[Criar um atributo numérico &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-numeric-attribute-master-data-services.md)|  
|Criar um novo atributo de link de formato livre|[Criar um atributo de vínculo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-link-attribute-master-data-services.md)|  
|Criar um novo atributo de arquivo.|[Criar um atributo de arquivo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-file-attribute-master-data-services.md)|  
|Criar um novo atributo baseado em domínio.|[Criar um atributo baseado em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Alterar o nome de um atributo existente.|[Alterar um nome de atributo &#40;Master Data Services&#41;](change-an-attribute-name-and-data-type-master-data-services.md)|  
|Adicionar atributos existentes a um grupo de rastreamento de alterações.|[Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../../2014/master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|Excluir um atributo existente.|[Excluir um atributo &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-master-data-services.md)|  
|Alterar a ordem dos atributos.|[Alterar a ordem dos atributos](../../2014/master-data-services/change-the-order-of-attributes.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atributos baseados em domínio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Grupos de atributos &#40;Master Data Services&#41;](attribute-groups-master-data-services.md)  
  
-   [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)  
  
-   [Permissões de folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md)  
  
-   [Permissões consolidadas &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)  
  
  
