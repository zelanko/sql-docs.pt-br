---
title: Propriedade Mode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fc2a9dffe5dc22c1dadfa075b91d8a6b26215de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863673"
---
# <a name="mode-property-ado"></a>Propriedade Mode (ADO)
Indica as permissões disponíveis para modificar dados em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md), ou [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor. O valor padrão para um **Conexão** é **adModeUnknown**. O valor padrão para um **registro** objeto é **adModeRead**. O valor padrão para um **Stream** associado a uma fonte subjacente (aberta com uma URL como a origem ou como o padrão **Stream** de um **registro**) é  **adModeRead**. O valor padrão para um **Stream** não está associada com uma subjacente (instanciada na memória) de origem é **adModeUnknown**.  
  
## <a name="remarks"></a>Comentários  
 Use o **modo** propriedade para definir ou retornar as permissões de acesso em uso pelo provedor sobre a conexão atual. Você pode definir as **modo** propriedade apenas quando o **Conexão** objeto está fechado.  
  
 Para um **Stream** do objeto, se o modo de acesso não for especificado, ela é herdada da fonte usada para abrir o **Stream** objeto. Por exemplo, se um **Stream** é aberta a partir um **registro** objeto, por padrão, ele é aberto no mesmo modo como o **registro**.  
  
 Essa propriedade é leitura/gravação, enquanto o objeto está fechado e somente leitura, enquanto o objeto está aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **Conexão** objeto, o **modo** propriedade só pode ser definida como **adModeUnknown**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [IsolationLevel e exemplo de propriedades de modo (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel e modo propriedades (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
