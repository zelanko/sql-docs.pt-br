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
ms.openlocfilehash: ec3b57b08460b834868581ac8872ac3c78a38bbe
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727767"
---
# <a name="dimension-relationships"></a>Relações de dimensão
  O uso de dimensões define as relações entre uma dimensão de cubo e os grupos de medidas em um cubo. Uma dimensão de cubo é uma instância de uma dimensão de banco de dados usada em um cubo específico. Um cubo pode ter, e frequentemente tem, dimensões de cubo que não estão diretamente relacionadas ao grupo de medidas, mas que podem estar indiretamente relacionadas ao grupo de medidas por meio de outra dimensão ou grupo de medidas. Quando você adiciona um grupo de medidas ou dimensões de banco de dados a um cubo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta determinar uso da dimensão examinando relações entre as tabelas de dimensões e tabelas de fatos na exibição de fonte de dados do cubo e por meio do exame as relações entre atributos em dimensões. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] define as configurações de uso de dimensão automaticamente para as relações que pode detectar.  
  
 Uma relação entre uma dimensão e um grupo de medidas consiste na dimensão e tabelas de fatos participantes da relação e um atributo de granularidade que especifica a granularidade da dimensão em um determinado grupo de medidas.  
  
## <a name="regular-dimension-relationships"></a>Relações regulares de dimensão   
 Uma relação regular de dimensão entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão está associada diretamente à tabela de fatos. Essa relação direta se baseia em uma relação de chave estrangeira de chave primária no banco de dados relacional subjacente, mas também pode se basear em uma relação lógica que é definida na exibição da fonte de dados. Uma relação de dimensão regular representa a relação entre tabelas de dimensão e uma tabela de fatos em um projeto de esquema em estrela tradicional. Para obter mais informações sobre as relações regulares, consulte [definir uma relação Regular e as propriedades da relação](../multidimensional-models/define-a-regular-relationship-and-regular-relationship-properties.md).  
  
## <a name="reference-dimension-relationships"></a>Relações de dimensão de referência  
 Uma relação de dimensão de referência entre uma dimensão de cubo e um grupo de medidas existe quando a coluna de chave da dimensão está associada indiretamente à tabela de fatos por meio de uma chave em outras tabelas de dimensões, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, a relação de dimensão referenciada](../../../2014/analysis-services/dev-guide/media/as-refdimension1.gif "diagrama lógico, a relação de dimensão referenciada")  
  
 Uma relação de dimensão de referência representa a relação entre tabelas de dimensão e uma tabela de fatos em um projeto de esquema de floco de neve. Quando tabelas de dimensões estão conectadas em um esquema de floco de neve, você pode definir uma única dimensão usando colunas de várias tabelas ou pode definir dimensões separadas com base em tabelas de dimensões separadas e, então, definir um link entre elas usando a configuração de relação de dimensão de referência. A figura a seguir mostra uma tabela de fatos chamada **InternetSales**, e duas tabelas de dimensões chamadas **Customer** e **geografia**, em um esquema floco de neve.  
  
 ![Esquema lógico, a relação de dimensão referenciada](../../../2014/analysis-services/dev-guide/media/as-refdim-schema1.gif "esquema lógico, a relação de dimensão referenciada")  
  
 Você pode criar uma dimensão com o **Customer** tabela como tabela principal da dimensão e o **geografia** tabela incluída como uma tabela relacionada. Uma relação regular é, então, definida entre a dimensão e o grupo de medidas VendasInternet.  
  
 Como alternativa, você pode criar duas dimensões relacionadas ao grupo de medidas Vendasinternet: uma dimensão com base nas **Customer** tabela e uma dimensão com base no **geografia** tabela. Você pode então relacionar a dimensão Geografia com o grupo de medidas VendasInternet, usando uma relação de dimensão de referência usando a dimensão Cliente. Nesse caso, quando os fatos no grupo de medidas VendasInternet forem dimensionados pela dimensão Geografia, os fatos serão dimensionados por cliente e por geografia. Se o cubo contiver um segundo grupo de medidas chamado Vendas do Revendedor, você não poderá dimensionar os fatos no grupo de medidas Vendas do Revendedor por Geografia, pois não há relação entre Vendas do Revendedor e Geografia.  
  
 Não há limite para o número de dimensões de referência que podem ser conectadas juntas, conforme mostrado na ilustração a seguir.  
  
 ![Diagrama lógico, a relação de dimensão referenciada](../../../2014/analysis-services/dev-guide/media/as-refdimension2.gif "diagrama lógico, a relação de dimensão referenciada")  
  
 Para obter mais informações sobre as relações referenciadas, consulte [definir uma relação referenciada e propriedades de relação de referência](../multidimensional-models/define-a-referenced-relationship-and-referenced-relationship-properties.md).  
  
## <a name="fact-dimension-relationships"></a>Relações de dimensão de fato  
 Dimensões de fato, frequentemente referenciadas como dimensões de degeneração, são dimensões padrão criadas a partir de colunas de atributo em tabelas de fatos, em vez serem criadas pelas colunas de atributo em tabelas de dimensões. Às vezes são armazenados dados dimensionais úteis em uma tabela de fatos para reduzir duplicação. Por exemplo, o diagrama a seguir exibe a **FactResellerSales** tabela de fatos, da [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] banco de dados de exemplo.  
  
 ![Colunas de fato tabela pode dar suporte a dimensões](../../../2014/analysis-services/dev-guide/media/as-factdim.gif "colunas na verdade tabela pode dar suporte a dimensões")  
  
 A tabela contém informações de atributo não apenas para cada linha de um pedido emitido por um revendedor, mas o próprio pedido. Os atributos circulados no diagrama anterior identificam as informações na **FactResellerSales** tabela que pode ser usada como atributos em uma dimensão. Nesse caso, duas informações adicionais, o número de rastreamento da transportadora e o número da ordem de compra emitido pelo revendedor, conforme representado pelas colunas de atributo CarrierTrackingNumber e CustomerPONumber. Essas informações são interessantes – por exemplo, os usuários podem estar interessados em visualizar informações agregadas, como o total de custos, para todos os pedidos sendo enviados sob um único número de rastreamento do produto. Mas, sem dados de dimensão esses dois atributos não podem ser organizados ou ser agregados.  
  
 Na teoria, você pode criar uma tabela de dimensões que usa as mesmas informações de chave que a tabela FactResellerSales e mover as outras duas colunas de atributo, CarrierTrackingNumber e CustomerPONumber, para essa tabela de dimensões. Entretanto, você pode estar duplicando uma parte significativa dos dados e adicionando complexidade desnecessária para o data warehouse, para representar apenas dois atributos como uma dimensão separada.  
  
> [!NOTE]  
>  As dimensões de fato são, frequentemente, usadas para oferecer suporte a ações de análise. Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  As dimensões de fato devem ser atualizadas incrementalmente após cada atualização do grupo de medidas referenciada pela relação de fato. Se a dimensão de fato for uma dimensão ROLAP, o mecanismo de processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] descartará qualquer cache e processará incrementalmente o grupo de medidas.  
  
 Para obter mais informações sobre relações de fatos, consulte [definir uma relação de fatos e as propriedades da relação fatos](../multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
## <a name="many-to-many-dimension-relationships"></a>Relações de dimensão muitos para muitos  
 Na maioria das dimensões, cada fato é associado a um e apenas um membro de dimensão e um simples membro de dimensão pode ser associado a vários fatos. Na terminologia de banco de dados relacional, isso é referenciado como uma relação de um para muitos. Porém, é frequentemente útil associar um único fato a vários membros de dimensão. Por exemplo, um cliente de um banco pode ter várias contas (corrente, poupança, cartão de crédito e investimentos) e uma conta também pode ter titulares conjuntos ou vários titulares. A dimensão Cliente criada a partir dessas relações pode ter então vários membros relacionados a uma única transação de conta.  
  
 ![Relação de dimensão lógicas esquema/muitos-para-muitos](../../../2014/analysis-services/dev-guide/media/as-many-dimension1.gif "relacionamento da dimensão lógicas esquema/muitos-para-muitos")  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite que você defina uma relação muitos-para-muitos entre uma dimensão e uma tabela de fatos.  
  
> [!NOTE]  
>  Para oferecer suporte a uma relação de dimensão muitos para muitos, a exibição da fonte de dados deve ter uma relação de chave estrangeira definida entre todas as tabelas envolvidas, conforme mostrado no diagrama anterior. Caso contrário, não será possível selecionar o grupo de medidas intermediário correto ao estabelecer a relação na **uso da dimensão** guia do Designer de dimensão.  
  
 Para obter mais informações sobre relações muitos-para-muitos, consulte [definem um muitos-para-muitos relação e muitos-para-muitos e propriedades de relação](../multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dimensões &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
