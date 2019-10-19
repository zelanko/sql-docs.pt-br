---
title: Relações de dimensão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- relationships [Analysis Services]
- member groups [Analysis Services]
- regular dimensions [Analysis Services]
- many-to-many relationships [Analysis Services]
- cubes [Analysis Services], relationships
- reference dimensions
- dimensions [Analysis Services], relationships
- fact dimensions [Analysis Services]
- relationships [Analysis Services], dimensions
ms.assetid: de54c059-cb0f-4f66-bd70-8605af05ec4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1fe1521f2eebaa4413b49c315f17a6b1b6a5914
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "68887934"
---
# <a name="dimension-relationships"></a>Relações de dimensão
  O uso da dimensão define as relações entre uma dimensão de cubo e os grupos de medidas em um cubo. Uma dimensão de cubo é uma instância de uma dimensão de banco de dados que é usada em um cubo específico. Um cubo pode, e muitas vezes, tem dimensões de cubo que não estão diretamente relacionadas a um grupo de medidas, mas que podem estar indiretamente relacionados ao grupo de medidas por meio de outra dimensão ou grupo de medidas. Quando você adiciona uma dimensão de banco de dados ou grupo de medidas a um cubo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta determinar o uso da dimensão examinando as relações entre as tabelas de dimensões e as tabelas de fatos na exibição da fonte de dados do cubo e examinando as relações entre atributos em dimensões. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] define automaticamente as configurações de uso da dimensão para as relações que ele pode detectar.  
  
 Uma relação entre uma dimensão e um grupo de medidas consiste nas tabelas de dimensões e fatos que participam da relação e um atributo de granularidade que especifica a granularidade da dimensão no grupo de medidas específico.  
  
## <a name="regular-dimension-relationships"></a>Relações de dimensão regulares  
 Uma relação de dimensão regular entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão é unida diretamente à tabela de fatos. Essa relação direta se baseia em uma relação chave primária-chave estrangeira no banco de dados relacional subjacente, mas também pode ser baseada em uma relação lógica que é definida na exibição da fonte de dado. Uma relação de dimensão regular representa a relação entre tabelas de dimensões e uma tabela de fatos em um design de esquema em estrela tradicional. Para obter mais informações sobre relações regulares, consulte [definir uma relação regular e propriedades de relação regular](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Relações de dimensão de referência  
 Uma relação de dimensão de referência entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão é unida indiretamente à tabela de fatos por meio de uma chave em outra tabela de dimensão, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension1.gif "Diagrama lógico, relação de dimensão referenciada")  
  
 Uma relação de dimensão de referência representa a relação entre tabelas de dimensões e uma tabela de fatos em um design de esquema floco de neve. Quando as tabelas de dimensões são conectadas em um esquema floco de neve, você pode definir uma única dimensão usando colunas de várias tabelas ou pode definir dimensões separadas com base nas tabelas de dimensões separadas e, em seguida, definir um link entre elas usando a referência configuração de relação de dimensão. A figura a seguir mostra uma tabela de fatos denominada **InternetSales**e duas tabelas de dimensão chamadas **Customer** e **geography**, em um esquema floco de neve.  
  
 ![Esquema lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdim-schema1.gif "Esquema lógico, relação de dimensão referenciada")  
  
 Você pode criar uma dimensão com a tabela **Customer** como a tabela principal de dimensão e a tabela **geography** incluída como uma tabela relacionada. Uma relação regular é então definida entre a dimensão e o grupo de medidas InternetSales.  
  
 Como alternativa, você pode criar duas dimensões relacionadas ao grupo de medidas InternetSales: uma dimensão baseada na tabela **Customer** e uma dimensão baseada na tabela **geography** . Em seguida, você pode relacionar a dimensão Geografia ao grupo de medidas InternetSales usando uma relação de dimensão de referência usando a dimensão cliente. Nesse caso, quando os fatos no grupo de medidas InternetSales são dimensionados pela dimensão Geografia, os fatos são dimensionados pelo cliente e pela geografia. Se o cubo contiver um segundo grupo de medidas chamado vendas do revendedor, você não poderá dimensionar os fatos no grupo de medidas vendas do revendedor por geografia porque não existe nenhuma relação entre as vendas do revendedor e a geografia.  
  
 Não há nenhum limite para o número de dimensões de referência que podem ser encadeadas em conjunto, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension2.gif "Diagrama lógico, relação de dimensão referenciada")  
  
 Para obter mais informações sobre relações referenciadas, consulte [definir uma relação referenciada e propriedades de relação referenciadas](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Relações de dimensão de fatos  
 Dimensões de fato, frequentemente conhecidas como dimensões de degeneração, são dimensões padrão que são construídas a partir de colunas de atributo em tabelas de fatos em vez de colunas de atributo em tabelas de dimensões. Às vezes, dados dimensionais úteis são armazenados em uma tabela de fatos para reduzir a duplicação. Por exemplo, o diagrama a seguir exibe a tabela de fatos **FactResellerSales** do banco de dados de exemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)].  
  
 ![As colunas na tabela de fatos podem dar suporte a dimensões](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-factdim.gif "As colunas na tabela de fatos podem dar suporte a dimensões")  
  
 A tabela contém informações de atributo não apenas para cada linha de um pedido emitido por um revendedor, mas sobre a própria ordem. Os atributos circulados no diagrama anterior identificam as informações na tabela **FactResellerSales** que podem ser usados como atributos em uma dimensão. Nesse caso, duas informações adicionais, o número de rastreamento da transportadora e o número da ordem de compra emitido pelo revendedor, são representados pelas colunas de atributo CarrierTrackingNumber e CustomerPONumber. Essas informações são interessantes – por exemplo, os usuários definitivamente se interessariam em ver informações agregadas, como o custo total do produto, para todos os pedidos sendo enviados sob um único número de controle. Mas, sem dados de dimensão para esses dois atributos não podem ser organizados ou agregados.  
  
 Teoricamente, você pode criar uma tabela de dimensões que usa as mesmas informações de chave que a tabela FactResellerSales e mover as outras duas colunas de atributo, CarrierTrackingNumber e CustomerPONumber, para essa tabela de dimensão. No entanto, você estaria duplicando uma parte significativa dos dados e adicionando complexidade desnecessária à data warehouse para representar apenas dois atributos como uma dimensão separada.  
  
> [!NOTE]  
>  As dimensões de fato são usadas frequentemente para dar suporte a ações de detalhamento. Para obter mais informações sobre ações, [consulte &#40;ações Analysis Services-dados&#41;multidimensionais](../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  As dimensões de fato devem ser atualizadas incrementalmente após cada atualização para o grupo de medidas que é referenciado pela relação de fatos. Se a dimensão de fatos for uma dimensão ROLAP, o mecanismo de processamento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descartará os caches e processará incrementalmente o grupo de medidas.  
  
 Para obter mais informações sobre as relações de fatos, consulte [definir uma relação de fatos e as propriedades da relação de fatos](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
## <a name="many-to-many-dimension-relationships"></a>Relações de dimensão muitos para muitos  
 Na maioria das dimensões, cada fato se une a apenas um membro de dimensão, e um único membro de dimensão pode ser associado a vários fatos. Na terminologia do banco de dados relacional, isso é chamado de relação um-para-muitos. No entanto, geralmente é útil unir um único fato a vários membros de dimensão. Por exemplo, um cliente bancário pode ter várias contas (verificação, salvamento, cartão de crédito e contas de investimento) e uma conta também pode ter proprietários ou múltiplos. A dimensão do cliente construída com essas relações teria, então, vários membros relacionados a uma única transação de conta.  
  
 ![Relação de esquema lógico/dimensão muitos para muitos](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-many-dimension1.gif "Relação de esquema lógico/dimensão muitos para muitos")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite que você defina uma relação muitos-para-muitos entre uma dimensão e uma tabela de fatos.  
  
> [!NOTE]  
>  Para dar suporte a uma relação de dimensão muitos para muitos, a exibição da fonte de dados deve ter estabelecido uma relação de chave estrangeira entre todas as tabelas envolvidas, conforme mostrado no diagrama anterior. Caso contrário, não será possível selecionar o grupo de medidas intermediário correto ao estabelecer a relação na guia **uso da dimensão** do designer de dimensão.  
  
 Para obter mais informações sobre relações muitos para muitos, consulte [definir uma relação muitos-para-muitos e propriedades de relação muitos-para-muitos](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões &#40;Analysis Services-dados multidimensionais&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
