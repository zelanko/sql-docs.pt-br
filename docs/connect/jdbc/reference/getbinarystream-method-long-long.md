---
description: Método getBinaryStream (long, long)
title: Método getBinaryStream (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a641fb117fe1dc091aa04f6343f69dac70d95c22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437198"
---
# <a name="getbinarystream-method-long-long"></a>Método getBinaryStream (long, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um objeto de fluxo de entrada que contém um valor BLOB parcial usando a posição inicial e o comprimento especificados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 O deslocamento para o primeiro byte do valor parcial ser recuperado.  
  
 *length*  
  
 O comprimento em bytes do valor parcial a ser recuperado.  
  
## <a name="return-value"></a>Valor de retorno  
 Um fluxo de entrada que contém os dados do BLOB.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBinaryStream é especificado pelo método the getBinaryStream na interface java.sql.Blob.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
