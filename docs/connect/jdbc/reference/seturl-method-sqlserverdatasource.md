---
description: Método setURL (SQLServerDataSource)
title: Método setURL (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea70100-ac98-4625-8748-ef7cc0b111ea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e27df8b938cee4503a2078d597b12eb880f52c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467112"
---
# <a name="seturl-method-sqlserverdatasource"></a>Método setURL (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define a URL usada para se conectar à fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *url*  
  
 Uma **String** que contém a URL.  
  
## <a name="remarks"></a>Comentários  
 Por motivos de segurança, você não deve incluir a senha na URL fornecida ao método setURL. Isso porque os Servidores de Aplicativos Java de terceiros muito frequentemente exibirão o valor definido para a propriedade URL em suas respectivas interfaces de usuário da configuração da fonte de dados. Em vez disso, use o método [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) para definir o valor da senha. Os Servidores de Aplicativos Java não exibirão uma senha que é definida em suas respectivas fontes de dados na interface de usuário da configuração.  
  
> [!NOTE]  
>  Se o método setURL não for chamado antes do método [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md), getURL retornará o valor padrão de "jdbc:sqlserver://".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
