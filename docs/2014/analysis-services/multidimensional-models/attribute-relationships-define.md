---
title: Definir relações de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
ms.assetid: 9184d344-e96d-4025-ad6f-3f75129746df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93e3ca09b1d1d20be103db8bbd92aa15e3a1ba5a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360428"
---
# <a name="define-attribute-relationships"></a>Definir relações de atributo
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os atributos representam o principal bloco de construção de uma dimensão. Uma dimensão contém um conjunto de atributos organizados com base em relações de atributo.  
  
 Para cada tabela incluída em uma dimensão, existe uma relação de atributo que relaciona o atributo de chave da tabela a outros atributos da tabela em questão. Essa relação é gerada na criação da dimensão.  
  
 Uma relação de atributo fornece as seguintes vantagens:  
  
-   Reduz a quantidade de memória necessária para o processamento da dimensão. Isso acelera o processamento de dimensão, partição e de consulta.  
  
-   Aumenta o desempenho de consulta, pois o acesso ao armazenamento é mais rápido e existe melhor otimização dos planos de execução.  
  
-   Resulta na seleção de agregações mais efetivas pelos algoritmos de design de agregação, contanto que as hierarquias definidas pelo usuário tenham sido definidas ao longo dos caminhos de relação.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre a importância e implicações de definir e configurar relações de atributo, consulte a seção "Enhancing query performance", na [SQL Server 2005 Analysis Services Performance Guide](https://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="attribute-relationship-considerations"></a>Considerações de relação de atributo  
 Quando os dados subjacentes permitirem, também é necessário definir relações de atributo exclusivas entre atributos. Para definir relações de atributo exclusivas, use a guia **Relações de Atributo** do Designer de Dimensão.  
  
 Qualquer atributo que tenha uma relação de saída deve ter uma chave exclusiva relacionada ao respectivo atributo. Em outras palavras, um membro em um atributo de origem deve identificar um e somente um membro em um atributo relacionado. Por exemplo, considere a relação Cidade -> Estado. Nesta relação, o atributo de origem é Cidade e o atributo relacionado é Estado. O atributo de origem é o lado "muitos" e o lado relacionado é o lado "um" da relação muitos-para-um. A chave para o atributo de origem seria Cidade + Estado. Para obter mais informações, consulte [Criar, modificar ou excluir uma relação de atributo](attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Para obter mais informações sobre as propriedades de uma relação de atributo, consulte [Configurar propriedades de relação de atributo](attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Definir incorretamente relações de atributo pode causar resultados de consulta inválidos.  
  
## <a name="see-also"></a>Consulte também  
 [Relações de Atributo](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
