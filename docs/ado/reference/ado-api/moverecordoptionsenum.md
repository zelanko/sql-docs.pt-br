---
title: MoveRecordOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MoveRecordOptionsEnum
helpviewer_keywords:
- MoveRecordOptionsEnum enumeration [ADO]
ms.assetid: f53c2ce4-1021-4a45-92b8-775e8bebad99
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8119b553ba7d85b9a3e1cabc49975967a0a751af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719191"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica o comportamento do [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Padrão. Executa a operação de movimentação padrão: A operação falhará se o arquivo de destino ou diretório já existe e a operação atualiza os links de hipertexto.|  
|**adMoveOverWrite**|1|Substitui o arquivo de destino ou diretório, mesmo se ele já existe.|  
|**adMoveDontUpdateLinks**|2|Modifica o comportamento padrão do **MoveRecord** método por não atualizar os links de hipertexto da fonte de **registro**. O comportamento padrão depende de recursos do provedor. Operação de movimentação atualiza links se o provedor for compatível com. Se o provedor não pode corrigir os links ou se esse valor não for especificado, em seguida, a movimentação for bem-sucedida, mesmo quando links não foram corrigidos.|  
|**adMoveAllowEmulation**|4|Solicita que o provedor tenta simular a movimentação (usando as operações de exclusão, upload e download). Se a tentativa de mover o **registro** falha porque a URL de destino está em um servidor diferente ou atendido por um provedor diferente que a fonte, isso pode causar maior latência ou perda de dados, devido aos recursos de provedor diferente quando Mover recursos entre os provedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
