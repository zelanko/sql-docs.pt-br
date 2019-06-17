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
manager: jroth
ms.openlocfilehash: 3e2d977647153ab74299a6b6f002ec33d3003558
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802541"
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>Método valueOf (java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cria um objeto **DateTimeOffset** que representa um momento determinado em um deslocamento específico do GMT dados um valor java.sql.Timestamp e um valor java.util.Calendar indicando o deslocamento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *timestamp*  
  
 Um valorjava.sql.Timestamp.  
  
 *calendário*  
  
 O valor de deslocamento.  Os componentes de data e hora do *calendário* será definido de acordo com as *timestamp* valor.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um objeto DateTimeOffset que representa o momento determinado fornecido pelo objeto em um fuso horário do objeto de determinado java.util.Calendar timestamp.  
  
## <a name="remarks"></a>Remarks  
 Esse método também define o objeto java.util.Calendar para o ponto de momento determinado fornecido pelo objeto timestamp.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
