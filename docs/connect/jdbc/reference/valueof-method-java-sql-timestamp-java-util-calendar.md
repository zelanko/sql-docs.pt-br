---
title: Método valueOf (java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11d8f8e346fdb0f07770feec815e5aa5fe88355f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68001590"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>Método valueOf (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto **DateTimeOffset** que representa um momento determinado em um deslocamento específico do GMT dados um valor java.sql.Timestamp e um valor java.util.Calendar indicando o deslocamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *timestamp*  
  
 Um valorjava.sql.Timestamp.  
  
 *calendário*  
  
 O valor de deslocamento.  Os componentes de data e hora de *calendar* serão definidos de acordo com o valor de *timestamp*.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto DateTimeOffset que representa o momento determinado fornecido pelo objeto java.sql.Timestamp no fuso horário fornecido do objeto java.util.Calendar.  
  
## <a name="remarks"></a>Comentários  
 Esse método também define o objeto java.util.Calendar como o ponto no tempo fornecido pelo objeto java.sql.Timestamp.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
