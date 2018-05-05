---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d2548bdec658e11980189fdfaae1c60594f71d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica os atributos de transação de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Executa anulações de retenção chamando [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores oferecem suporte a esse comportamento.|  
|**adXactCommitRetaining**|131072|Executa a retenção confirmações chamando [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores oferecem suporte a esse comportamento.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
