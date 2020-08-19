---
description: MoveRecordOptionsEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 03728baab7882597cfba29d2f566d73ac98f9300
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443138"
---
# <a name="moverecordoptionsenum"></a>MoveRecordOptionsEnum
Especifica o comportamento do método [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) do objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adMoveUnspecified**|-1|Padrão. Executa a operação de movimentação padrão: a operação falhará se o arquivo ou diretório de destino já existir, e a operação atualizará os links de hipertexto.|  
|**adMoveOverWrite**|1|Substitui o arquivo ou diretório de destino, mesmo que ele já exista.|  
|**adMoveDontUpdateLinks**|2|Modifica o comportamento padrão do método **MoveRecord** ao não atualizar os links de hipertexto do **registro**de origem. O comportamento padrão depende dos recursos do provedor. Mover links de atualizações de operação se o provedor for compatível. Se o provedor não puder corrigir links ou se esse valor não for especificado, a movimentação terá sucesso mesmo quando os links não tiverem sido corrigidos.|  
|**adMoveAllowEmulation**|4|Solicita que o provedor tente simular a movimentação (usando operações de download, carregamento e exclusão). Se a tentativa de mover o **registro** falhar porque a URL de destino está em um servidor diferente ou foi atendida por um provedor diferente da origem, isso pode causar maior latência ou perda de dados, devido a diferentes recursos do provedor ao mover recursos entre provedores.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
