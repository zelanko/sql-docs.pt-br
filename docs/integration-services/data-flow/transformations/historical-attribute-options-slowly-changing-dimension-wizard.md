---
title: Opções de Atributo Histórico (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dcf6e290bf12600dee4b6483ca305507a5888973
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>Opções de Atributo Histórico (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Opções de Atributo Histórico** para mostrar atributos históricos por datas de início e de término ou para registrar atributos históricos em uma coluna criada especialmente para este propósito.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Use uma única coluna para mostrar os registros atual e expirado**  
 Se você optar por usar uma única coluna para registrar o status de atributos históricos, estarão disponíveis as seguintes opções:  
  
|Opção|Description|  
|------------|-----------------|  
|**Coluna para indicar o registro atual**|Selecione uma coluna na qual indicar o registro atual.|  
|**Valor atual**|Use **Verdadeiro** ou **Atual** para mostrar se o registro é atual.|  
|**Valor de expiração**|Use **Falso** ou **Expirado** para mostrar se o registro é um valor histórico.|  
  
 **Use as datas de início e de término para identificar os registros atual e expirado**  
 A tabela de dimensão desta opção deve incluir uma coluna de data. Se você optar por mostrar atributos históricos por datas de início e de término, estarão disponíveis as seguintes opções:  
  
|Opção|Description|  
|------------|-----------------|  
|**Coluna da data de início**|Selecione a coluna na tabela de dimensões que conterá a data de início.|  
|**Coluna da data de término**|Selecione a coluna na tabela de dimensões que conterá a data de término.|  
|**Variável para definir valores de data**|Selecione uma variável de data na lista.|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
