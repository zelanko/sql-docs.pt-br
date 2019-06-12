---
title: Método getPacketSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPacketSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2e9f01a-2e51-47e5-90bf-43c62d1be74d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ef02cfaf54499aa3ac6219b32ff154a258733614
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765650"
---
# <a name="getpacketsize-method-sqlserverdatasource"></a>Método getPacketSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o tamanho do pacote de rede atual usado para se comunicar com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especificado em bytes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getPacketSize()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que contém o tamanho do pacote de rede atual.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade packetSize não for definida, o método getPacketSize retornará o valor padrão de 8000.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
