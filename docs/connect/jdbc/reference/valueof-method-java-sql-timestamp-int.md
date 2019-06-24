---
title: Método valueOf (timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b3d2eb2934474b51aacddebc72230330c86bfeb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797855"
---
# <a name="valueof-method-javasqltimestamp-int"></a>Método valueOf (java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto **DateTimeOffset** que representa um momento determinado em um deslocamento específico do GMT dados um valor java.sql.Timestamp e um valor indicando o deslocamento em minutos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timestamp*  
  
 Um valorjava.sql.Timestamp.  
  
 *minutesOffset*  
  
 O deslocamento em minutos.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto DateTimeOffset que representa o momento determinado fornecido pelo objeto timestamp no deslocamento especificado, minutos, de GMT.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
