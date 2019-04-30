---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a5ab00cc6e01b97639ae3f7d353fa2462ef3fd0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309166"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica as permissões disponíveis para modificar dados em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), abrindo uma [registro](../../../ado/reference/ado-api/record-object-ado.md), ou especificando valores para o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade do  **Registro** e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica as permissões somente leitura.|  
|**adModeReadWrite**|3|Indica as permissões de leitura/gravação.|  
|**adModeRecursive**|0x400000|Usado em conjunto com outras *\*ShareDeny\** valores (**adModeShareDenyNone**, **adModeShareDenyWrite**, ou **adModeShareDenyRead**) para propagar as restrições de compartilhamento para todos os registros de subpropriedades do atual **registro**. Ela não terá efeito se a **registro** não tem nenhum filho. Um erro de tempo de execução será gerado se ele é usado com **adModeShareDenyNone** somente. No entanto, ele pode ser usado com **adModeShareDenyNone** quando combinado com outros valores. Por exemplo, você pode usar "**adModeRead** ou **adModeShareDenyNone** ou **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite que outros usuários abrir uma conexão com todas as permissões. O acesso à leitura/gravação não pode ser negado a outras pessoas.|  
|**adModeShareDenyRead**|4|Impede que outras pessoas abram uma conexão com permissões de leitura.|  
|**adModeShareDenyWrite**|8|Impede que outras pessoas abram uma conexão com permissões de gravação.|  
|**adModeShareExclusive**|12|Impede que outras pessoas abram uma conexão.|  
|**adModeUnknown**|0|Padrão. Indica que as permissões ainda não foi definidas ou não podem ser determinadas.|  
|**adModeWrite**|2|Indica as permissões de somente gravação.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
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
