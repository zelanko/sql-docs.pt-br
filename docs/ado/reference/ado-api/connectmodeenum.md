---
description: ConnectModeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 10bc68683f337f5a0bdf6fc5679c4276925a4234
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775845"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica as permissões disponíveis para modificar dados em uma [conexão](./connection-object-ado.md), abrir um [registro](./record-object-ado.md)ou especificar valores para a propriedade [Mode](./mode-property-ado.md) dos objetos **Record** e [Stream](./stream-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica permissões somente leitura.|  
|**adModeReadWrite**|3|Indica permissões de leitura/gravação.|  
|**adModeRecursive**|0x400000|Usado em conjunto com os outros valores de * \* ShareDeny \* * (**adModeShareDenyNone**, **adModeShareDenyWrite**ou **adModeShareDenyRead**) para propagar as restrições de compartilhamento para todos os subregistros do **registro**atual. Ele não afeta se o **registro** não tiver nenhum filho. Um erro de tempo de execução será gerado se for usado somente com **adModeShareDenyNone** . No entanto, ele pode ser usado com **adModeShareDenyNone** quando combinado com outros valores. Por exemplo, você pode usar "**adModeRead** ou **adModeShareDenyNone** ou **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite que outras pessoas abram uma conexão com qualquer permissão. O acesso à leitura/gravação não pode ser negado a outras pessoas.|  
|**adModeShareDenyRead**|4|Impede que outras pessoas abram uma conexão com permissões de leitura.|  
|**adModeShareDenyWrite**|8|Impede que outras pessoas abram uma conexão com permissões de gravação.|  
|**adModeShareExclusive**|12|Impede que outras pessoas abram uma conexão.|  
|**adModeUnknown**|0|Padrão. Indica que as permissões ainda não foram definidas ou não podem ser determinadas.|  
|**adModeWrite**|2|Indica permissões somente gravação.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectMode. READ|  
|AdoEnums. ConnectMode. READWRITE|  
|(Não há equivalente a AdoEnums. ConnectMode. recursivo)|  
|AdoEnums. ConnectMode. SHAREDENYNONE|  
|AdoEnums. ConnectMode. SHAREDENYREAD|  
|AdoEnums. ConnectMode. SHAREDENYWRITE|  
|AdoEnums. ConnectMode. SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode. desconhecido|  
|AdoEnums. ConnectMode. WRITE|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Propriedade Mode (ADO)](./mode-property-ado.md)  
        [Método Open (Registro do ADO)](./open-method-ado-record.md)  
    :::column-end:::
    :::column:::
        [Método Open (Fluxo do ADO)](./open-method-ado-stream.md)  
        [Objeto Stream (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::