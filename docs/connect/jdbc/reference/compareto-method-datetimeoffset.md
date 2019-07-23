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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f70413a7624b9bbd380a664fbf61b9a33f8989b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955512"
---
# <a name="compareto-method-datetimeoffset"></a>Método compareTo (DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Compara este objeto **DateTimeOffset** com outro objeto **DateTimeOffset** com base no tempo em GMT.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Um valor [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) que você deseja comparar com a instância atual.  
  
## <a name="return-value"></a>Valor retornado  
 A tabela a seguir descreve o valor de retorno do método:  
  
|Valor retornado|Descrição|  
|------------------|-----------------|  
|0|Ambos os objetos **DateTimeOffset** representam o mesmo ponto no tempo.|  
|número negativo|Esse objeto **DateTimeOffset** representa um ponto no tempo anterior a *outro*.|  
|número positivo|Esse objeto **DateTimeOffset** representa um ponto no tempo que é posterior a *outro*.|  
  
## <a name="remarks"></a>Remarks  
 Quando dois objetos **DateTimeOffset** tiverem a mesma hora em GMT, não haverá nenhuma organização adicional dos objetos com base no deslocamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
