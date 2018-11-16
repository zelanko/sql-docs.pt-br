---
title: Agrupar membros de atributo (diferenciação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- NameColumn property
- discretization [Analysis Services]
- member groups [Analysis Services]
- grouping members
- DiscretizationNumber property
- sort orders [Analysis Services]
- DiscretizationMethod property
- adding members to member group
- number of member groups
- members [Analysis Services], groups
- names [Analysis Services], member groups
ms.assetid: 5cf2f407-accc-4baf-b54f-7703af338325
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8f7ff454dd4464fab5173c4d0022bd94543c1dad
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814039"
---
# <a name="group-attribute-members-discretization"></a>Agrupar membros de atributo (diferenciação)
  Um grupo de membros é uma coleção gerada pelo sistema de membros da dimensão consecutivos. No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível agrupar os membros de um atributo em diversos grupos de membros por meio de um processo chamado diferenciação. Um nível em uma hierarquia contém grupos de membro ou membros, mas não ambos. Quando os usuários da empresa procuram um nível que contém grupos de membros, eles veem nomes e valores de célula dos grupos de membros. Os membros gerados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para oferecer suporte aos grupos de membros são chamados membros do agrupamento e são similares aos membros comuns.  
  
 A propriedade `DiscretizationMethod` de um atributo controla como os membros são agrupados.  
  
|Configuração `DiscretizationMethod`|Description|  
|--------------------------------------|-----------------|  
|`None`|Exibe os membros.|  
|`Automatic`|Seleciona o método que melhor representa os dados: o método `EqualAreas` ou o método `Clusters`.|  
|`EqualAreas`|Tenta dividir os membros do atributo em grupos com o mesmo número de membros.|  
|`Clusters`|Tenta dividir os membros do atributo em grupos por meio de amostragem dos dados de treinamento, inicializando um número aleatório de pontos e executando várias interações do algoritmo de clustering Expectation Maximization (EM).<br /><br /> Esse método é útil pois funciona com qualquer curva de distribuição, mas é mais dispendioso em termos de tempo de processamento.|  
  
 A propriedade `DiscretizationNumber` dos atributos especifica o número de grupos que serão exibidos. Se for configurada com o valor padrão de 0, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determinará o número de grupos pela amostragem ou leitura dos dados, dependendo da configuração da propriedade `DiscretizationMethod`.  
  
 A ordem de classificação dos membros dos grupos de membros é controlada pela propriedade `OrderBy` do atributo. Com base nessa ordem de classificação, os membros de um grupo são ordenados consecutivamente.  
  
 Um uso comum para grupos de membros é a busca detalhada a partir de um nível com poucos membros até um nível com muitos membros. Para que os usuários possam fazer uma busca detalhada entre os níveis, altere a propriedade `DiscretizationMethod` do atributo do nível que contém vários membros de `None` para um dos métodos de diferenciação descritos na tabela anterior. Por exemplo, uma dimensão Cliente contém uma hierarquia de atributo Nome do Cliente com 500.000 membros. Você pode renomear esse atributo Grupos de Clientes e configurar a propriedade `DiscretizationMethod` como `Automatic` para exibir os grupos de membros no nível do membro da hierarquia do atributo.  
  
 Para fazer a busca detalhada de clientes individuais de cada grupo, é possível criar outra hierarquia do atributo Nome do Cliente vinculada à mesma coluna da tabela. Em seguida, crie uma nova hierarquia de usuários baseada nos dois atributos. O nível superior deve basear-se no atributo Grupos de Clientes e o inferior no atributo Nome do Cliente. A propriedade `IsAggregatable` seria `True` em ambos os atributos. O usuário pode então expandir o nível (All) da hierarquia para exibir os membros do grupo e expandir os membros do grupo para exibir os membros folha da hierarquia. Para ocultar o grupo ou o nível de cliente, seria possível definir a propriedade `AttributeHierarchyVisible` como `False` no atributo correspondente.  
  
## <a name="naming-template"></a>Modelo de nomeação  
 Os nomes dos grupos de membros são gerados automaticamente quando os grupos de membros são criados. A menos que você especifique um modelo de nomeação, será usado o modelo de nomeação padrão. É possível alterar esse método de nomeação especificando um modelo de nomeação na opção `Format` da propriedade `NameColumn` de um atributo. Modelos de nomeação diferentes podem ser redefinidos para cada idioma especificado na coleção `Translations` da associação de coluna que foi usada para a propriedade `NameColumn` do atributo.  
  
 A configuração `Format` usa a expressão de cadeia de caracteres a seguir para definir o modelo de nomeação:  
  
 `<Naming template> ::= <First definition> [;<Intermediate definition>;<Last definition>]`  
  
 `<First definition> ::= <Name expression>`  
  
 `<Intermediate definition> ::= <Name expression>`  
  
 `<Last definition> ::= <Name expression>`  
  
 O parâmetro `<First definition>` aplica-se apenas ao primeiro ou ao único grupo de membros gerado pelo método de diferenciação. Se os parâmetros opcionais `<Intermediate definition>` e `<Last definition>` não forem fornecidos, o parâmetro `<First definition>` será usado em todos os grupos de medidas gerados para esse atributo.  
  
 O parâmetro `<Last definition>` aplica-se somente ao último grupo de membros gerado pelo método de diferenciação.  
  
 O parâmetro `<Intermediate bucket name>` aplica-se a todos os grupos de membros além do primeiro ou último grupo de membros gerado pelo método de diferenciação. Se forem gerados dois ou menos grupos de membros, esse parâmetro será ignorado.  
  
 O parâmetro `<Bucket name>` é uma expressão de cadeia de caracteres que pode incorporar um conjunto de variáveis para representar informações de membros ou grupos de membros como parte do nome do grupo de membros:  
  
|Variável|Description|  
|--------------|-----------------|  
|% {Primeiro membro do bloco}|O nome do primeiro membro que será incluído no grupo de membros atual.|  
|% {Último membro do bloco}|O nome do último membro que será incluído no grupo de membros atual.|  
|% {Último membro do bloco anterior}|O nome do último membro atribuído ao grupo de membros anterior.|  
|% {Primeiro membro do próximo bloco}|O nome do primeiro membro que será atribuído ao próximo grupo de membros.|  
|% {Mín. do bloco}|O valor mínimo de membros que será atribuído ao grupo de membros atual.|  
|% {Máx. do bloco}|O valor máximo de membros que será atribuído ao grupo de membros atual.|  
|% {Máx. do bloco anterior}|O valor máximo de membros que será atribuído ao grupo de membros anterior.|  
|% {Mín. do próximo bloco}|O valor mínimo dos membros que será atribuído ao próximo grupo de membros.|  
  
 O modelo de nomeação padrão é `"%{First bucket member} - %{Last bucket member}"`, para proporcionar compatibilidade com versões anteriores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Para incluir um ponto-e-vírgula (;) como caractere literal no modelo de nomeação, acrescente como prefixo o caractere de percentual (%).  
  
### <a name="example"></a>Exemplo  
 A expressão de cadeia de caracteres a seguir serviria para classificar o atributo Receita anual da dimensão Cliente do banco de dados de exemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , sendo que o atributo Receita anual usa o agrupamento de membros:  
  
 "Menor que % {Mín. do próximo bloco}; Entre % {Primeiro membro do bloco} e % {Último membro do bloco}; Maior que % {Máx. do bloco anterior}"  
  
## <a name="adding-new-members-to-existing-member-groups"></a>Adicionando novos membros a grupos de membros existentes  
 Se forem incluídos novos membros na dimensão, eles serão atribuídos aos grupos de membros apropriados ao se comparar o valor do membro com o layout do grupo de membros atual.  
  
 Se o membro for inserido entre o último membro do grupo de membros anterior e o primeiro do próximo grupo de membros, o novo membro passará a ser o último membro do grupo de membros anterior.  
  
## <a name="updating-a-dimension-with-discretized-attributes"></a>Atualizando uma dimensão com atributos de diferenciação  
 Quando você processar uma dimensão, um atributo diferenciado será novamente diferenciado somente no caso de atualização completa (ProcessFull). Para diferenciar novamente um atributo, execute uma atualização completa da dimensão. Se a tabela de dimensões de um atributo diferenciado for atualizada e você processar a dimensão com uma atualização incremental (ProcessAdd), o atributo diferenciado não será diferenciado novamente. Os nomes e os filhos dos novos blocos permanecem os mesmos. Para obter mais informações sobre as dimensões de processamento, consulte [Processamento de objetos do Analysis Services](processing-analysis-services-objects.md).  
  
## <a name="usage-limitations"></a>Limitações de uso  
  
-   Não é possível criar grupos de membros no nível mais alto ou mais baixo de uma hierarquia. No entanto, se isso for necessário, você pode adicionar um nível de modo que o nível no qual você deseja criar grupos de membros deixe de ser o mais alto ou mais baixo. Você pode ocultar o nível adicionado configurando sua propriedade `Visible` como `False`.  
  
-   Não é possível criar grupos de membros em dois níveis consecutivos de uma hierarquia.  
  
-   Não há suporte para grupos de membros em dimensões que usam modo de armazenamento ROLAP.  
  
-   Se a tabela de dimensões de uma dimensão que contém grupos de membros for atualizada e, na sequência, a dimensão for totalmente processada, será gerado um novo conjunto de grupos de membros. Os nomes e os filhos dos novos grupos de membros podem ser diferentes dos anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Atributos e hierarquias de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
