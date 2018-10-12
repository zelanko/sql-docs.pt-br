---
title: Método refreshRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19bd400492ba8ce8547f48b83b2f94544bd28a2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812614"
---
# <a name="refreshrow-method-sqlserverresultset"></a>Método refreshRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a linha atual com seu valor mais recente no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método refreshRow é especificado pelo método refreshRow na interface do resultset.  
  
 Esse método não pode ser chamado quando o cursor estiver na linha de inserção.  
  
 Esse método fornece uma maneira de um aplicativo informar explicitamente ao driver JDBC que as linhas do banco de dados devem ser buscadas novamente. Um aplicativo pode precisar chamar esse método quando o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] está armazenando em cache ou fazendo uma pré-busca do valor mais recente de uma linha no banco de dados. O driver JDBC poderá realmente atualizar várias linhas ao mesmo tempo se o tamanho da busca for maior que um.  
  
 É feita pré-busca de todos os valores dependendo do nível de isolamento da transação e da sensibilidade do cursor. A chamada desse método depois da chamada de um método updater, mas antes da chamada do método [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) faz com que as atualizações feitas na linha sejam perdidas. Chamar este método com frequência provavelmente reduzirá o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
