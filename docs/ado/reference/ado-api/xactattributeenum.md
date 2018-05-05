---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
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
ms.openlocfilehash: 33b3ac42f0e0e175e2dc2571c77f6dbaa962922f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
