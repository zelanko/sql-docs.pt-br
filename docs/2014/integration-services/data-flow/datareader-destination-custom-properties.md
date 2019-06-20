---
title: Propriedades personalizadas do destino DataReader | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 948ebbc696048915662caaa24b791e6258c459be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827624"
---
# <a name="datareader-destination-custom-properties"></a>Propriedades personalizadas do destino DataReader
  O destino DataReader tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino DataReader. Todas as propriedades, exceto `DataReader`, são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|DataReader|Cadeia de caracteres|O nome da classe do destino DataReader.|  
|FailOnTimeout|Booliano|Indica se deve haver falha na ocorrência de `ReadTimeout`. O valor padrão dessa propriedade é **False**.|  
|ReadTimeout|Integer|O número de milissegundos antes de um tempo limite. O valor padrão dessa propriedade é 30000 (30 segundos).|  
  
 A entrada e as colunas de entrada do destino DataReader não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [DataReader Destination](datareader-destination.md).  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades comuns](../common-properties.md)  
  
  
