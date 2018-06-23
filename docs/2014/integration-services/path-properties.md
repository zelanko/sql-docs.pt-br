---
title: Propriedades de caminho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- paths [Integration Services], properties
ms.assetid: 89b1e347-9579-4f6b-af74-c6519ea08eea
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7d8a30fac3cdf6bb28df5b7c2a2e811b3e604a22
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012937"
---
# <a name="path-properties"></a>Propriedades do caminho
  Os objetos de fluxo de dados no modelo de objeto do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] têm propriedades comuns e personalizadas ao nível de componente, entradas e saídas e colunas de entrada e saída. Muitas propriedades têm valores somente leitura, atribuídos em tempo de execução pelo mecanismo de fluxo de dados.  
  
 Esse tópico lista e descreve as propriedades personalizadas dos caminhos que conectam objetos do fluxo de dados.  
  
## <a name="path-properties"></a>Propriedades do caminho  
 No modelo de objeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], um caminho que conecta componentes no fluxo de dados implementa a interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 A tabela a seguir descreve as propriedades configuráveis dos caminhos em um fluxo de dados. O mecanismo de fluxo de dados também atribui valores a propriedades somente leitura adicionais que não são listadas aqui.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Inteiro (enumeração)|Um valor que indica se uma anotação deve ser exibida com o caminho na superfície do designer. Os valores possíveis são `AsNeeded`, `SourceName`, `PathName`, e `Never`. O valor padrão é `AsNeeded`.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|A entrada associada ao caminho.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|A saída associada ao caminho.|  
  
## <a name="see-also"></a>Consulte também  
 [Caminhos do Integration Services](data-flow/integration-services-paths.md)   
 [Propriedades comuns](../../2014/integration-services/common-properties.md)   
 [Propriedades personalizadas da transformação](data-flow/transformations/transformation-custom-properties.md)   
 [Propriedades de fluxo de dados que podem ser definidas usando expressões](../../2014/integration-services/data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  