---
description: Classe SQLServerException
title: Classe SQLServerException | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b096f1b41cc817b216cea9ff3618e7731abd5003
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450477"
---
# <a name="sqlserverexception-class"></a>Classe SQLServerException
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa uma execução malsucedida ou incompleta de uma instrução SQL.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.sql.SQLException  
  
 **Implementa:** java.io.Serializable  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Comentários  
 A classe SQLServerException manipula códigos de estado SQL 92 e XOPEN. Eles podem ser trocados usando uma propriedade de conexão especificada pelo usuário. As exceções são gravadas em qualquer arquivo de log aberto que foi especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
