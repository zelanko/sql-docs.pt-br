---
title: Método compareTo (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac80b43813106f1de991da5114b2473871222a68
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923575"
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara este objeto **DateTimeOffset** com outro objeto **DateTimeOffset** com base no tempo em GMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>parâmetros  
 Um valor [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) que você deseja comparar com a instância atual.  
  
## <a name="return-value"></a>Valor retornado  
 A tabela a seguir descreve o valor de retorno do método:  
  
|Valor retornado|DESCRIÇÃO|  
|------------------|-----------------|  
|0|Os dois objetos **DateTimeOffset** representam o mesmo momento.|  
|número negativo|Esse objeto **DateTimeOffset** representa um momento anterior a *outro*.|  
|número positivo|Esse objeto **DateTimeOffset** representa um momento posterior a *outro*.|  
  
## <a name="remarks"></a>Comentários  
 Quando dois objetos **DateTimeOffset** tiverem a mesma hora em GMT, não haverá nenhuma organização adicional dos objetos com base no deslocamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
