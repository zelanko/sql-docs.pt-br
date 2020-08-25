---
description: CursorTypeEnum
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e0d37d5aad3f27a61cf3ae7c8dad9b27149e09b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775465"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Especifica o tipo de cursor usado em um objeto [Recordset](./recordset-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Usa um cursor dinâmico. Adições, alterações e exclusões por outros usuários estão visíveis e todos os tipos de movimento por meio do **conjunto de registros** são permitidos, exceto para indicadores, se o provedor não oferecer suporte a eles.|  
|**adOpenForwardOnly**|0|Padrão. Usa um cursor de somente avanço. Idêntico a um cursor estático, exceto que você só pode rolar para frente pelos registros. Isso melhora o desempenho quando você precisa fazer apenas uma passagem por um **conjunto de registros**.|  
|**adOpenKeyset**|1|Usa um cursor de conjunto de chaves. Como um cursor dinâmico, exceto que você não pode ver registros que outros usuários adicionam, embora os registros excluídos por outros usuários sejam inacessíveis do seu **conjunto de registros**. As alterações de dados por outros usuários ainda estão visíveis.|  
|**adOpenStatic**|3|Usa um cursor estático, que é uma cópia estática de um conjunto de registros que você pode usar para localizar dados ou gerar relatórios. Adições, alterações ou exclusões por outros usuários não estão visíveis.|  
|**adOpenUnspecified**|-1|Não especifica o tipo de cursor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. CursorType. dinâmico|  
|AdoEnums. CursorType. FORWARDONLY|  
|AdoEnums. CursorType. conjunto de chaves|  
|AdoEnums. CursorType. STATIC|  
|AdoEnums. CursorType. não especificado|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade CursorType (ADO)](./cursortype-property-ado.md)