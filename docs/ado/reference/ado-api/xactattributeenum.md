---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5bf3c4b8a7cbbee1e384c08746f32d6a7e550ddd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710141"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica os atributos de transação de um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Executa as anulações de retenção chamando [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores dão suporte a esse comportamento.|  
|**adXactCommitRetaining**|131072|Executa a retenção de confirmações chamando [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores dão suporte a esse comportamento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
