---
title: Método setResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5b4490ac15558a0f6268a3d400d197367d028b9d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796744"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>Método setResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) como **String full** ou **adaptive** que não diferencia maiúsculas de minúsculas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *value*  
  
 Uma **String** que contém o modo de buffer de resposta. O modo válido pode ser uma das cadeias de caracteres sem diferenciação de maiúsculas e minúsculas a seguir: **full** ou **adaptive**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 **adaptive** especifica o armazenamento do mínimo possível de dados em buffer, quando necessário.  
  
 **full** especifica a leitura do resultado inteiro no servidor em tempo de execução.  
  
 adaptável é o valor padrão no JDBC Driver versão 2.0 e 3.0. completo era o padrão anterior ao JDBC Driver versão 2.0.  
  
 O método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) permite substituir a conexão **responseBuffering**, propriedade **String**, para o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) atual. Para obter mais informações sobre como usar a modo de buffer de resposta, consulte [Using Adaptive Buffering](../../../connect/jdbc/using-adaptive-buffering.md).  
  
 Se o aplicativo especificar um valor de parâmetro inválido para o método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md), um [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) será lançado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [Usando buffer adaptável](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
