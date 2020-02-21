---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d4c67c2-a3c8-4a26-a159-89c5d63fda0b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6b8f6239fbc229af009fc9745b0f19ed27e7ee1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979057"
---
# <a name="gettime-method-javalangstring-javautilcalendar"></a>Método getTime (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do parâmetro designado como um objeto java.sql.Time na linguagem de programação Java, considerando o nome do parâmetro, usando o objeto Calendar fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sCol*  
  
 Uma **String** que contém o nome do parâmetro.  
  
 *cal*  
  
 Um objeto Calendar.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Time.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getTime é especificado pelo método getTime na interface java.sql.CallableStatement.  
  
 Confira o gráfico intitulado "Conversões de método getter" em [Noções básicas sobre conversões de tipo de dados](../../../connect/jdbc/understanding-data-type-conversions.md) para ver quais tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem ser recuperados com esse método.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Classe SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
