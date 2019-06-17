---
title: Definir relações de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e49207e99887e13cdd5321821e7325b4a2dac7dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62717799"
---
# <a name="attribute-relationships---define"></a>Relações de atributo – Definir
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os atributos representam o principal bloco de construção de uma dimensão. Uma dimensão contém um conjunto de atributos organizados com base em relações de atributo.  
  
 Para cada tabela incluída em uma dimensão, existe uma relação de atributo que relaciona o atributo de chave da tabela a outros atributos da tabela em questão. Essa relação é gerada na criação da dimensão.  
  
 Uma relação de atributo fornece as seguintes vantagens:  
  
-   Reduz a quantidade de memória necessária para o processamento da dimensão. Isso acelera o processamento de dimensão, partição e de consulta.  
  
-   Aumenta o desempenho de consulta, pois o acesso ao armazenamento é mais rápido e existe melhor otimização dos planos de execução.  
  
-   Resulta na seleção de agregações mais efetivas pelos algoritmos de design de agregação, contanto que as hierarquias definidas pelo usuário tenham sido definidas ao longo dos caminhos de relação.  
  
  
## <a name="attribute-relationship-considerations"></a>Considerações de relação de atributo  
 Quando os dados subjacentes permitirem, também é necessário definir relações de atributo exclusivas entre atributos. Para definir relações de atributo exclusivas, use a guia **Relações de Atributo** do Designer de Dimensão.  
  
 Qualquer atributo que tenha uma relação de saída deve ter uma chave exclusiva relacionada ao respectivo atributo. Em outras palavras, um membro em um atributo de origem deve identificar um e somente um membro em um atributo relacionado. Por exemplo, considere a relação Cidade -> Estado. Nesta relação, o atributo de origem é Cidade e o atributo relacionado é Estado. O atributo de origem é o lado "muitos" e o lado relacionado é o lado "um" da relação muitos-para-um. A chave para o atributo de origem seria Cidade + Estado. Para obter mais informações, consulte [Criar, modificar ou excluir uma relação de atributo](../../analysis-services/multidimensional-models/attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Para obter mais informações sobre as propriedades de uma relação de atributo, consulte [Configurar propriedades de relação de atributo](../../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Definir incorretamente relações de atributo pode causar resultados de consulta inválidos.  
  
## <a name="see-also"></a>Consulte também  
 [Relações de Atributo](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
