---
title: Método getPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4350bb6f3d6213548b298b45052ca009e8f99cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getpacketsize-method-sqlserverdatasource"></a>Método getPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o tamanho de pacote de rede atual usado para se comunicar com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], especificado em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que contém o tamanho de pacote de rede atual.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade packetSize não for definida, o método getPacketSize retorna o valor padrão de 8000.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
