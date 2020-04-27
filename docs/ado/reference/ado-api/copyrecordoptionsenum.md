---
title: CopyRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CopyRecordOptionsEnum
helpviewer_keywords:
- CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6692125b7323bedc7a416e51555c373ef850ce0a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67919378"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Especifica o comportamento do método [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Indica que o provedor de *origem* tenta simular a cópia usando operações de download e upload se esse método falhar devido ao *destino*estar em um servidor diferente ou for atendido por um provedor diferente da *origem*. Observe que diferentes recursos de provedor podem dificultar o desempenho ou perder dados.|  
|**adCopyNonRecursive**|2|Copia o diretório atual, mas nenhum de seus subdiretórios, para o destino. A operação de cópia não é recursiva.|  
|**adCopyOverWrite**|1|Substitui o arquivo ou diretório se o *destino* apontar para um arquivo ou diretório existente.|  
|**adCopyUnspecified**|-1|Padrão. Executa a operação de cópia padrão: a operação falhará se o arquivo ou diretório de destino já existir e a operação for copiada recursivamente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
