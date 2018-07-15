---
title: Opções de Atributo Histórico (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7f9b7b2819eec76f3ccc913debea3773cad0b9e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328076"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>Opções de Atributo Histórico (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Opções de Atributo Histórico** para mostrar atributos históricos por datas de início e de término ou para registrar atributos históricos em uma coluna criada especialmente para este propósito.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
