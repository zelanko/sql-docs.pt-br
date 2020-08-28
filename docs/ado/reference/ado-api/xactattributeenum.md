---
description: XactAttributeEnum
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bb2a1391e813fd80c394bd685eff07e06015dd5b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987687"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Especifica os atributos de transação de um objeto de [conexão](./connection-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Executa anulações de retenção chamando [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores dão suporte a esse comportamento.|  
|**adXactCommitRetaining**|131072|Executa as confirmações de retenção chamando o [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) para iniciar automaticamente uma nova transação. Nem todos os provedores dão suporte a esse comportamento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Attributes (ADO)](./attributes-property-ado.md)