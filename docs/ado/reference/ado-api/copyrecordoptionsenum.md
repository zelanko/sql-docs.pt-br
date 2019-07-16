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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919378"
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Especifica o comportamento do [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Indica que o *fonte* provedor tenta simular a cópia usando o download e carregar as operações se esse método falhar devido a *destino*sendo em um servidor diferente ou é atendida por uma diferente provedor de *fonte*. Observe que os diferentes recursos do provedor podem degradar o desempenho ou perda de dados.|  
|**adCopyNonRecursive**|2|Copia o diretório atual, mas nenhum de seus subdiretórios, para o destino. A operação de cópia não é recursiva.|  
|**adCopyOverWrite**|1|Substitui o arquivo ou diretório se o *destino* aponta para um arquivo ou diretório existente.|  
|**adCopyUnspecified**|-1|Padrão. Executa a operação de cópia padrão: A operação falhará se o arquivo de destino ou diretório já existir e a operação copia recursivamente.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
