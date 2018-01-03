---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: XactAttributeEnum
helpviewer_keywords: XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 27f9e93ee75b4efcf427bbf7a69737180f7141b2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica os atributos de transação de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
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
