---
title: Método setBinaryStream (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d4dd274fd77de831f2ea7484cc759ab4cb771d7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928834"
---
# <a name="setbinarystream-method-sqlserverblob"></a>Método setBinaryStream (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo que pode ser usado para gravar no valor do BLOB.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Pos*  
  
 A posição em que a gravação deve ser iniciada no valor BLOB)  
  
## <a name="return-value"></a>Valor retornado  
 Um fluxo de saída.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setBinaryStream é especificado pelo método setBinaryStream na interface java.sql.Blob.  
  
 Os dados no BLOB são substituídos pelo fluxo de saída iniciando na posição especificada e podem ultrapassar o comprimento inicial do BLOB. A especificação de um valor posição+1 acrescentará bytes. A transmissão de um valor posição+2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
