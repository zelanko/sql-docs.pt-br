---
title: Propriedade Mode (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ee4463749e231b6ecd48a1fa24af1a72b3766ef
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="mode-property-ado"></a>Propriedade Mode (ADO)
Indica as permissões disponíveis para modificar dados em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md), ou [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor. O valor padrão para um **Conexão** é **adModeUnknown**. O valor padrão para um **registro** objeto **adModeRead**. O valor padrão para um **fluxo** associado a uma fonte subjacente (aberta com uma URL como a origem ou o padrão **fluxo** de um **registro**) é ** adModeRead**. O valor padrão para um **fluxo** não associados a uma subjacente (instanciada na memória) de origem é **adModeUnknown**.  
  
## <a name="remarks"></a>Comentários  
 Use o **modo** propriedade para definir ou retornar as permissões de acesso em uso pelo provedor sobre a conexão atual. Você pode definir o **modo** propriedade apenas quando o **Conexão** objeto está fechado.  
  
 Para uma **fluxo** do objeto, se o modo de acesso não for especificado, ele é herdado da fonte usada para abrir o **fluxo** objeto. Por exemplo, se um **fluxo** é aberto a partir um **registro** objeto, por padrão, ele é aberto no mesmo modo como o **registro**.  
  
 Essa propriedade é leitura/gravação enquanto o objeto está fechado e somente leitura, enquanto o objeto está aberto.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **Conexão** objeto, o **modo** propriedade só pode ser definida como **adModeUnknown**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de modo (VB) e IsolationLevel](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Exemplo de propriedades de modo (VC + +) e IsolationLevel](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   

