---
title: Método position (java.lang.String, long) (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 46d4beec-831a-449f-98b6-322a80cc499a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4dd9e30039b0d5ef429b8e729ce36f7b085e5cfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976458"
---
# <a name="position-method-javalangstring-long-sqlservernclob"></a>Método position (java.lang.String, long) (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera a posição do caractere na qual a subcadeia de caracteres especificada *searchstr* aparece no valor **NClob** representado por esse objeto **NClob** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public long position(java.lang.String searchstr,  
              long start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *searchstr*  
  
 A subcadeia de caracteres pela qual pesquisar.  
  
 *start*  
  
 A posição em que a pesquisa deve ser iniciada; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor retornado  
 A posição em que a subcadeia de caracteres aparece; ou -1 se ela não estiver presente. A primeira posição é 1.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método position é especificado pelo método position na interface java. Sql. NClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Método &#40;de posição SQLServerNClob&#41;](../../../connect/jdbc/reference/position-method-sqlservernclob.md)   
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
