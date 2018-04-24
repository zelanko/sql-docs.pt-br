---
title: CopyRecordOptionsEnum | Microsoft Docs
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
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5a571e4c68ccaa40ab14ccc6714b53e16937cfc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Especifica o comportamento do [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Indica que o *fonte* provedor tenta simular a cópia usando o download e carregar operações se esse método falhar devido a *destino*sendo em um servidor diferente ou é atendida por um diferente provedor de *fonte*. Observe que os diferentes recursos do provedor podem degradar o desempenho ou perda de dados.|  
|**adCopyNonRecursive**|2|Copia a pasta atual, mas nenhum de seus subdiretórios, o destino. A operação de cópia não é recursivos.|  
|**adCopyOverWrite**|1|Substitui o arquivo ou diretório se o *destino* aponta para um arquivo ou diretório existente.|  
|**adCopyUnspecified**|-1|Padrão. Executa a operação de cópia padrão: A operação falhará se o arquivo de destino ou o diretório já existe e a operação copia recursivamente.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
