---
title: Método setNCharacterStream ao objeto do leitor - int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47c70780ea5528cb55734a718a0e70bb359d35a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setncharacterstream-method-int-javaioreader"></a>Método setNCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *value*  
  
 Um objeto do leitor que contém o valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setNCharacterStream é especificado pelo método setNCharacterStream na interface PreparedStatement.  
  
 Esse método deve ser usado para **NCHAR**, **NVARCHAR**, **NTEXT**, e **XML** tipos de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Método setNCharacterStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
