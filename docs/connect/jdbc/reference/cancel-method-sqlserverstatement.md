---
title: Método cancel (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b19ff8669843e93dc7c220e3e6b48cbd5bab7d06
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923713"
---
# <a name="cancel-method-sqlserverstatement"></a>Método cancel (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cancela a instrução SQL que está sendo executada pelo objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) em questão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método cancel é especificado pelo método cancel na interface java.sql.Statement.  
  
 Ao executar uma instrução que produz um único conjunto de resultados grande, apenas de encaminhamento, somente leitura, você pode estar interessado apenas em algum conjunto inicial de linhas no conjunto de resultados retornado. Nesse caso, o aplicativo pode chamar o método [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) do objeto de instrução associado antes de fechar o conjunto de resultados, para minimizar o tempo de processamento necessário para descartar as linhas desnecessárias restantes. Ao decidir se essa técnica será usada ou não, é recomendável considerar a compensação entre o tempo de processamento que seria economizado e o tempo e a viagem de ida e volta adicional ao servidor, necessários para cancelar a execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
