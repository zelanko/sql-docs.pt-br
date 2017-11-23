---
title: CopyRecordOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CopyRecordOptionsEnum
helpviewer_keywords: CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 018ebb888e190946ebac8e4b19b42302e430e3b0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Especifica o comportamento do [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Indica que o *fonte* provedor tenta simular a cópia usando o download e carregar operações se esse método falhar devido a *destino*sendo em um servidor diferente ou é atendida por um diferente provedor de *fonte*. Observe que os diferentes recursos do provedor podem degradar o desempenho ou perda de dados.|  
|**adCopyNonRecursive**|2|Copia a pasta atual, mas nenhum de seus subdiretórios, o destino. A operação de cópia não é recursivos.|  
|**adCopyOverWrite**|1|Substitui o arquivo ou diretório se o *destino* aponta para um arquivo ou diretório existente.|  
|**adCopyUnspecified**|-1|Padrão. Executa a operação de cópia padrão: A operação falhará se o arquivo de destino ou o diretório já existe e a operação copia recursivamente.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
