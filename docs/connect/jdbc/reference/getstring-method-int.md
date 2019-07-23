---
title: Método GetString (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3fce8bf-8d6e-476f-aa6d-992daa79b899
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2160e7214b3ad60d2c8629d55bd79de8a5b15905
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979496"
---
# <a name="getstring-method-int"></a>Método getString (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como uma **String** na linguagem de programação Java, considerando o índice do parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getString(int index)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *index*  
  
 Um **int** que indica o índice do parâmetro.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor de **String**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getString é especificado pelo método getString na interface java.sql.CallableStatement.  
  
 Todas as colunas no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem ser retornadas como uma cadeia de caracteres. Isso significa que uma representação da cadeia de caracteres de todos os tipos baseados em número e em caractere, e uma representação da cadeia de caracteres hexadecimais de colunas binárias, como binary, varbinary, varbinary(max), image, timestamp e uniqueidentifier, podem ser retornadas.  
  
 Os tipos que diferenciam locais, como money, smallmoney, datetime, smalldatetime, float, real, decimal e numeric, retornarão o formato toString() canônico para o valor subjacente do tipo.  
  
 Os tipos definidos pelo usuário são retornados como valores de cadeia de caracteres hexadecimais.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getString &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
