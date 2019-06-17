---
title: Habilitar write-back de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying dimensions
- writeback [Analysis Services], setting up
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], writeback
- dimensions [Analysis Services], writeback
- writeback [Analysis Services]
- dimensions [Analysis Services], modifying
- manual dimension structure modifications
ms.assetid: a4b5eb5a-366d-4fc8-ad0d-5bdb8e7b4163
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6051f62caac2878b689a50e5773b047cb8df7afe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076847"
---
# <a name="enable-dimension-writeback"></a>Habilitar Write-back de Dimensão
  Adicione o aprimoramento de write-back de dimensão a um cubo ou dimensão para que os usuários possam modificar manualmente a estrutura e os membros da dimensão. Atualizações em uma dimensão habilitada para gravação são registradas diretamente na tabela de dimensões. Esse aprimoramento altera a configuração de propriedade `WriteEnabled` de uma dimensão.  
  
 Para adicionar o write-back da dimensão, use o Assistente de Business Intelligence e selecione a opção **Habilitar o write-back de dimensão** na página **Escolher Aprimoramento** . Esse assistente orientará você durante as etapas para selecionar a dimensão à qual você deseja aplicar um write-back de dimensão e para configurar essa opção para a dimensão selecionada.  
  
> [!NOTE]  
>  Write-back tem suporte apenas em bancos de dados relacionais do SQL Server e data marts.  
  
## <a name="selecting-a-dimension"></a>Selecionando uma dimensão  
 Na primeira página **Habilitar o Write-back de Dimensão** do assistente, especifique a dimensão à qual você deseja aplicar o write-back de dimensão. O aprimoramento de write-back de dimensão adicionado à dimensão selecionada provocará alterações na dimensão. Essas alterações serão herdadas por todos os cubos que tiverem a dimensão selecionada.  
  
## <a name="setting-dimension-writeback-capability"></a>Definindo a capacidade de write-back de dimensão  
 Na segunda página **Habilitar o Write-back de Dimensão** do assistente, você realmente define a opção **Habilitar write-back na dimensão** . A seleção dessa opção definirá automaticamente a propriedade `WriteEnabled` da dimensão como `True`. Desmarcar essa opção definirá automaticamente a propriedade como `False`.  
  
## <a name="remarks"></a>Comentários  
 Ao criar um novo membro, você deve incluir todo atributo em uma dimensão. Você não pode inserir um membro sem especificar um valor para o atributo de chave da dimensão. Portanto, a criação de membros está sujeita às restrições (como valores de chave não nulos) definidas na tabela de dimensões. Você também deve considerar opcionalmente colunas especificadas por propriedades de dimensão, como colunas especificadas na propriedade de dimensão `CustomRollupColumn`, `CustomRollupPropertiesColumn` ou `UnaryOperatorColumn`.  
  
> [!WARNING]  
>  Se você usar o SQL Azure como uma fonte de dados para executar writeback em um banco de dados do Analysis Services, a operação falhará. Isto ocorre por design, porque a opção de provedor que habilita vários conjuntos de resultados ativos (MARS) não é ativada por padrão.  
>   
>  A solução alternativa é adicionar a configuração a seguir na cadeia de conexão, para dar suporte a MARS e habilitar writeback:  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  Para obter mais informações, consulte [Usando MARS &#40;vários conjuntos de resultados ativos&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões habilitadas para gravação](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
