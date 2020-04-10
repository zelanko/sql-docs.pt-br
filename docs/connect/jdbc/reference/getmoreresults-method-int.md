---
title: Método getMoreResults (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db242def83e840e3518aa4036a66f823585f80b2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906132"
---
# <a name="getmoreresults-method-int"></a>Método getMoreResults (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move para o próximo resultado do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) e trata todos os objetos do conjunto de resultados abertos no momento de acordo com as instruções especificadas pelo modo fornecido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *mode*  
  
 Um **int** que indica como tratar objetos do conjunto de resultados abertos no momento. Deve ser uma das constantes a seguir:  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (sem suporte do JDBC Driver)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Valor retornado  
 **true** se o resultado retornado for um conjunto de resultados. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getMoreResults é especificado pelo método getMoreResults na interface do java.sql.Statement.  
  
 Se o método getMoreResults for chamado antes da recuperação dos resultados, ele se comportará conforme especificado pelo argumento *mode* e passará para o próximo resultado.  
  
> [!NOTE]  
>  O JDBC Driver não oferece suporte ao uso da constante KEEP_CURRENT_RESULT. Se ela for usada, uma exceção será lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getMoreResults &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
