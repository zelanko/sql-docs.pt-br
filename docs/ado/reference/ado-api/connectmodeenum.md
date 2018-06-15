---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94b89e379d85002fc58deb36a1b95d1b7457d4c8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277085"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica as permissões disponíveis para modificar dados em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), abrindo um [registro](../../../ado/reference/ado-api/record-object-ado.md), ou especificar valores para o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade o  **Registro** e [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica as permissões somente leitura.|  
|**adModeReadWrite**|3|Indica as permissões de leitura/gravação.|  
|**adModeRecursive**|0x400000|Usado em conjunto com outras *\*ShareDeny\** valores (**adModeShareDenyNone**, **adModeShareDenyWrite**, ou **adModeShareDenyRead**) para propagar as restrições de compartilhamento para todos os registros de subtipo do atual **registro**. Ela não terá efeito se a **registro** não tem nenhum filho. Um erro de tempo de execução será gerado se ele é usado com **adModeShareDenyNone** somente. No entanto, ele pode ser usado com **adModeShareDenyNone** quando combinado com outros valores. Por exemplo, você pode usar "**adModeRead** ou **adModeShareDenyNone** ou **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite que outros usuários abrir uma conexão com as permissões. O acesso à leitura/gravação não pode ser negado a outras pessoas.|  
|**adModeShareDenyRead**|4|Impede que outras pessoas abram uma conexão com permissões de leitura.|  
|**adModeShareDenyWrite**|8|Impede que outras pessoas abram uma conexão com permissões de gravação.|  
|**adModeShareExclusive**|12|Impede que outras pessoas abram uma conexão.|  
|**adModeUnknown**|0|Padrão. Indica que as permissões ainda não foi definidas ou não podem ser determinadas.|  
|**adModeWrite**|2|Indica as permissões de somente gravação.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(Não há nenhum equivalente de AdoEnums.ConnectMode.RECURSIVE)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Propriedade Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Método Open (Registro do ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Método Open (Fluxo do ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
