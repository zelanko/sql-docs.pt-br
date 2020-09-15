---
description: Método valueOf (java.sql.Timestamp, int)
title: Método valueOf (java.sql.Timestamp, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9797c5109b34897aca747d091949975eefc3727
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396122"
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
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um objeto DateTimeOffset que representa o momento determinado fornecido pelo objeto java.sql.Timestamp em um deslocamento específico, em minutos, do GMT.  
  
## <a name="see-also"></a>Consulte Também  
 [Classe DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [Membros DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
