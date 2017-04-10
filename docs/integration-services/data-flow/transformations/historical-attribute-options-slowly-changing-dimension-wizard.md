---
title: "Op&#231;&#245;es de Atributo Hist&#243;rico (Assistente para Dimens&#245;es de Altera&#231;&#227;o Lenta) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.loaddimwizard.histattriboption.f1"
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Op&#231;&#245;es de Atributo Hist&#243;rico (Assistente para Dimens&#245;es de Altera&#231;&#227;o Lenta)
  Use a caixa de diálogo **Opções de Atributo Histórico** para mostrar atributos históricos por datas de início e de término ou para registrar atributos históricos em uma coluna criada especialmente para este propósito.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## Opções  
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
  
## Consulte também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  