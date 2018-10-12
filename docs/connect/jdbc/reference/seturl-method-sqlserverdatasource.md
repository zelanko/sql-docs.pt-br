---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 29e1b67caaf566f04cf01c7c93a5e8d2445c31ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633944"
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
  
## <a name="remarks"></a>Remarks  
 Por motivos de segurança, você não deve incluir a senha na URL fornecida ao método setURL. Isso porque os Servidores de Aplicativos Java de terceiros muito frequentemente exibirão o valor definido para a propriedade URL em suas respectivas interfaces de usuário da configuração da fonte de dados. Em vez disso, use o método [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) para definir o valor da senha. Os Servidores de Aplicativos Java não exibirão uma senha que é definida em suas respectivas fontes de dados na interface de usuário da configuração.  
  
> [!NOTE]  
>  Se o método setURL não for chamado antes do método [getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md), getURL retornará o valor padrão de "jdbc:sqlserver://".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
