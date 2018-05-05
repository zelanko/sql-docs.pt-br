---
title: Método getMoreResults (int) | Microsoft Docs
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
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75609ec8f24674dd7ff9d1a6724cbc458be47f84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getmoreresults-method-int"></a>Método getMoreResults (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move para o próximo resultado deste [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto e lida com qualquer resultado aberto definir objetos de acordo com as instruções especificadas pelo modo fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Modo*  
  
 Um **int** que indica como tratar objetos do conjunto de resultados abertos no momento. Deve ser uma das constantes a seguir:  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (sem suporte do JDBC Driver)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Valor de retorno  
 **True** se o resultado retornado é um conjunto de resultados. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getMoreResults é especificado pelo método getMoreResults na interface Java.SQL. Statement.  
  
 Se o método getMoreResults é chamado antes de resultados são recuperados, ele se comporta conforme especificado pelo *modo* argumento e move para o próximo resultado.  
  
> [!NOTE]  
>  O JDBC Driver não oferece suporte ao uso da constante KEEP_CURRENT_RESULT. Se ela for usada, uma exceção será lançada.  
  
## <a name="see-also"></a>Consulte também  
 [Método getMoreResults &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
