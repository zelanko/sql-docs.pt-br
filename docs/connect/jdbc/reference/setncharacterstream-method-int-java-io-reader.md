---
title: Método setNCharacterStream para o objeto do leitor – int | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7732746b-eda5-469e-8567-e8546c4d81cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db62ff8815a1ac4ca9c27a6da0de720f653ef9c7
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925515"
---
# <a name="setncharacterstream-method-int-javaioreader"></a>Método setNCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o parâmetro designado como o objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                 java.io.Reader value)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *parameterIndex*  
  
 Um **int** que indica o índice do parâmetro.  
  
 *value*  
  
 Um objeto Reader que contém o valor do parâmetro.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setNCharacterStream é especificado pelo método setNCharacterStream na interface java.sql.PreparedStatement.  
  
 Esse método deve ser usado para tipos de dados **NCHAR**, **NVARCHAR**, **NTEXT** e **XML**.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setNCharacterStream &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
