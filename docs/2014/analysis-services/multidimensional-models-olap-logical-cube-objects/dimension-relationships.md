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
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887934"
---
# <a name="dimension-relationships"></a>Relações de dimensão
  O uso de dimensões define as relações entre uma dimensão de cubo e os grupos de medidas em um cubo. Uma dimensão de cubo é uma instância de uma dimensão de banco de dados usada em um cubo específico. Um cubo pode ter, e frequentemente tem, dimensões de cubo que não estão diretamente relacionadas ao grupo de medidas, mas que podem estar indiretamente relacionadas ao grupo de medidas por meio de outra dimensão ou grupo de medidas. Quando você adiciona uma dimensão de banco de dados ou grupo de medidas [!INCLUDE[msCoName](../../includes/msconame-md.md)] a um cubo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o tenta determinar o uso da dimensão examinando as relações entre as tabelas de dimensões e as tabelas de fatos na exibição da fonte de dados do cubo e examinando as relações entre atributos em dimensões. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] define as configurações de uso de dimensão automaticamente para as relações que pode detectar.  
  
 Uma relação entre uma dimensão e um grupo de medidas consiste na dimensão e tabelas de fatos participantes da relação e um atributo de granularidade que especifica a granularidade da dimensão em um determinado grupo de medidas.  
  
## <a name="regular-dimension-relationships"></a>Relações regulares de dimensão  
 Uma relação regular de dimensão entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão está associada diretamente à tabela de fatos. Essa relação direta se baseia em uma relação chave primária-chave estrangeira no banco de dados relacional subjacente, mas também pode ser baseada em uma relação lógica que é definida na exibição da fonte de dado. Uma relação de dimensão regular representa a relação entre tabelas de dimensão e uma tabela de fatos em um projeto de esquema em estrela tradicional. Para obter mais informações sobre relações regulares, consulte [definir uma relação regular e propriedades de relação regular](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Relações de dimensão de referência  
 Uma relação de dimensão de referência entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão está associada indiretamente à tabela de fatos por meio de uma chave em outras tabelas de dimensões, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension1.gif "Diagrama lógico, relação de dimensão referenciada")  
  
 Uma relação de dimensão de referência representa a relação entre tabelas de dimensão e uma tabela de fatos em um projeto de esquema de floco de neve. Quando tabelas de dimensões estão conectadas em um esquema de floco de neve, você pode definir uma única dimensão usando colunas de várias tabelas ou pode definir dimensões separadas com base em tabelas de dimensões separadas e, então, definir um link entre elas usando a configuração de relação de dimensão de referência. A figura a seguir mostra uma tabela de fatos denominada **InternetSales**e duas tabelas de dimensão chamadas **Customer** e geography, em um esquema floco de neve.  
  
 ![Esquema lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdim-schema1.gif "Esquema lógico, relação de dimensão referenciada")  
  
 Você pode criar uma dimensão com a tabela **Customer** como a tabela principal de dimensão e a tabela geography incluída como uma tabela relacionada. Uma relação regular é, então, definida entre a dimensão e o grupo de medidas VendasInternet.  
  
 Como alternativa, você pode criar duas dimensões relacionadas ao grupo de medidas InternetSales: uma dimensão baseada na tabela **Customer** e uma dimensão baseada na tabela geography. Você pode então relacionar a dimensão Geografia com o grupo de medidas VendasInternet, usando uma relação de dimensão de referência usando a dimensão Cliente. Nesse caso, quando os fatos no grupo de medidas VendasInternet forem dimensionados pela dimensão Geografia, os fatos serão dimensionados por cliente e por geografia. Se o cubo contiver um segundo grupo de medidas chamado Vendas do Revendedor, você não poderá dimensionar os fatos no grupo de medidas Vendas do Revendedor por Geografia, pois não há relação entre Vendas do Revendedor e Geografia.  
  
 Não há limite para o número de dimensões de referência que podem ser conectadas juntas, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, relação de dimensão referenciada](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-refdimension2.gif "Diagrama lógico, relação de dimensão referenciada")  
  
 Para obter mais informações sobre relações referenciadas, consulte [definir uma relação referenciada e propriedades de relação referenciadas](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Relações de dimensão de fato  
 Dimensões de fato, frequentemente referenciadas como dimensões de degeneração, são dimensões padrão criadas a partir de colunas de atributo em tabelas de fatos, em vez serem criadas pelas colunas de atributo em tabelas de dimensões. Às vezes são armazenados dados dimensionais úteis em uma tabela de fatos para reduzir duplicação. Por exemplo, o diagrama a seguir exibe a tabela de fatos **FactResellerSales** do [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] banco de dados de exemplo.  
  
 As ![colunas na tabela de fatos podem dar suporte a dimensões](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-factdim.gif "colunas na tabela de fatos podem dar suporte a dimensões")  
  
 A tabela contém informações de atributo não apenas para cada linha de um pedido emitido por um revendedor, mas o próprio pedido. Os atributos circulados no diagrama anterior identificam as informações na tabela **FactResellerSales** que podem ser usados como atributos em uma dimensão. Nesse caso, duas informações adicionais, o número de rastreamento da transportadora e o número da ordem de compra emitido pelo revendedor, conforme representado pelas colunas de atributo CarrierTrackingNumber e CustomerPONumber. Essas informações são interessantes – por exemplo, os usuários definitivamente se interessariam em ver informações agregadas, como o custo total do produto, para todos os pedidos sendo enviados sob um único número de controle. Mas, sem dados de dimensão esses dois atributos não podem ser organizados ou ser agregados.  
  
 Na teoria, você pode criar uma tabela de dimensões que usa as mesmas informações de chave que a tabela FactResellerSales e mover as outras duas colunas de atributo, CarrierTrackingNumber e CustomerPONumber, para essa tabela de dimensões. Entretanto, você pode estar duplicando uma parte significativa dos dados e adicionando complexidade desnecessária para o data warehouse, para representar apenas dois atributos como uma dimensão separada.  
  
> [!NOTE]  
>  As dimensões de fato são, frequentemente, usadas para oferecer suporte a ações de análise. Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  As dimensões de fato devem ser atualizadas incrementalmente após cada atualização do grupo de medidas referenciada pela relação de fato. Se a dimensão de fato for uma dimensão ROLAP, o mecanismo de processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descartará qualquer cache e processará incrementalmente o grupo de medidas.  
  
 Para obter mais informações sobre as relações de fatos, consulte [definir uma relação de fatos e as propriedades da relação de fatos](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
## <a name="many-to-many-dimension-relationships"></a>Relações de dimensão muitos para muitos  
 Na maioria das dimensões, cada fato é associado a um e apenas um membro de dimensão e um simples membro de dimensão pode ser associado a vários fatos. Na terminologia de banco de dados relacional, isso é referenciado como uma relação de um para muitos. Porém, é frequentemente útil associar um único fato a vários membros de dimensão. Por exemplo, um cliente de um banco pode ter várias contas (corrente, poupança, cartão de crédito e investimentos) e uma conta também pode ter titulares conjuntos ou vários titulares. A dimensão Cliente criada a partir dessas relações pode ter então vários membros relacionados a uma única transação de conta.  
  
 ![Relação de esquema lógico/dimensão muitos para muitos](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-many-dimension1.gif "Relação de esquema lógico/dimensão muitos para muitos")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite definir uma relação muitos-para-muitos entre uma dimensão e uma tabela de fatos.  
  
> [!NOTE]  
>  Para oferecer suporte a uma relação de dimensão muitos para muitos, a exibição da fonte de dados deve ter uma relação de chave estrangeira definida entre todas as tabelas envolvidas, conforme mostrado no diagrama anterior. Caso contrário, não será possível selecionar o grupo de medidas intermediário correto ao estabelecer a relação na guia **uso da dimensão** do designer de dimensão.  
  
 Para obter mais informações sobre relações muitos para muitos, consulte [definir uma relação muitos-para-muitos e propriedades de relação muitos-para-muitos](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
