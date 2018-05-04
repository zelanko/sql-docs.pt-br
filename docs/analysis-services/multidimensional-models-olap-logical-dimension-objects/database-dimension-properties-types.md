---
title: Tipos de dimensão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c36b8c16acb2521c2472b1f4398cb68ea89952d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="database-dimension-properties---types"></a>Propriedades de dimensão do banco de dados - tipos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  O **tipo** configuração da propriedade fornece informações sobre o conteúdo de uma dimensão para aplicativos cliente e servidor. Em alguns casos, o **tipo** configuração somente fornece orientação para aplicativos cliente e é opcional. Em outros casos, como **contas** ou **tempo** dimensões, o **tipo** configurações de propriedade para a dimensão e seus atributos determinam comportamentos específicos baseados em servidor e pode ser necessário para implementar determinados comportamentos no cubo. Por exemplo, o **tipo** propriedade de uma dimensão pode ser definida como **contas** para indicar a aplicativos cliente que a dimensão padrão contém atributos de conta. Para obter mais informações sobre o tempo, a conta e a dimensão de moeda, consulte [criar uma dimensão de tipo de data](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [criar uma conta de Finanças de dimensão de tipo de pai-filho](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), e [criar uma moeda tipo de dimensão](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 A configuração padrão para o tipo de dimensão é **Regular**, que não faz nenhuma suposição sobre o conteúdo da dimensão. Essa é a configuração padrão para todas as dimensões quando você define inicialmente uma dimensão a menos que você especifique **tempo** ao definir a dimensão usando o Assistente para dimensões. Você também deve deixar **Regular** como o tipo de dimensão se o Assistente para dimensões não lista um tipo apropriado para o tipo de dimensão.  
  
## <a name="available-dimension-types"></a>Tipos de dimensão disponíveis  
 A tabela a seguir descreve os tipos de dimensão disponíveis no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Tipo de dimensão|Description|  
|--------------------|-----------------|  
|Regular|Uma dimensão cujo tipo não foi definido como um tipo de dimensão especial.|  
|Hora|Uma dimensão cujos atributos representam períodos, como anos, semestres, trimestres, meses e dias.|  
|Organização|Uma dimensão cujos atributos representam informações organizacionais, como funcionários ou subsidiárias.|  
|Geografia|Uma dimensão cujos atributos representam informações geográficas, como cidades ou códigos postais.|  
|BillOfMaterials|Uma dimensão cujos atributos representam informações de estoque ou manufatura, como listas de peças para produtos.|  
|Contas|Uma dimensão cujos atributos representam um plano de contas para fins de geração de relatórios financeiros.|  
|Customers|Uma dimensão cujos atributos representam informações do cliente ou de contato.|  
|Products|Uma dimensão cujos atributos representam informações de produto.|  
|Cenário|Uma dimensão cujos atributos representam informações de planejamento ou de análise estratégica.|  
|Quantitative|Uma dimensão cujos atributos representam informações quantitativas.|  
|Utilitário|Uma dimensão cujos atributos representam informações diversas.|  
|Moeda|Este tipo de dimensão contém dados e metadados de moeda.|  
|Rates|Uma dimensão cujos atributos representam informações de taxa de moeda.|  
|Canal|Uma dimensão cujos atributos representam informações de canal.|  
|Promoção|Uma dimensão cujos atributos representam informações de promoções de marketing.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma dimensão usando uma tabela existente](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensões & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
