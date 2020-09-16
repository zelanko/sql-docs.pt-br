---
description: Classe SQLServerStatement
title: Classe SQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c794edb2b0f2c62177b6591881c8886e36590bd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462578"
---
# <a name="sqlserverstatement-class"></a>Classe SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa a implementação básica da funcionalidade de instrução JDBC.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Comentários  
 A classe SQLServerStatement também fornece vários métodos de implementação de classe base para a instrução preparada JDBC e instruções que podem ser chamadas. A função básica da classe SQLServerStatement é executar instruções SQL e retornar contagens de atualização e conjuntos de resultados para o aplicativo do usuário.  
  
 Essa classe dá suporte ao desencapsulamento da classe SQLServerStatement, da interface ISQLServerStatement e da interface java.sql.Statement. Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
