---
title: Método position (java.sql.Blob, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (java.sql.Blob.long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebd005e5-f6c5-4789-87f9-d2fdacd35060
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fd642677405adf98cce23826775a0cab45221a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923189"
---
# <a name="position-method-javasqlblob-long"></a>Método position (java.sql.Blob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna a posição de um padrão especificado no BLOB com base no padrão fornecido e no índice inicial.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(java.sql.Blob pattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pattern*  
  
 O padrão a ser pesquisado.  
  
 *start*  
  
 O índice inicial no qual pesquisar.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **long** da posição em que o padrão foi localizado ou -1 se não foi localizado.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método position é especificado pelo método position na interface java.sql.Blob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método position &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
