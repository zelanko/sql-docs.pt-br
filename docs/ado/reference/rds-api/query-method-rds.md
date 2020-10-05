---
description: Método Query (RDS)
title: Método de consulta (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: rothja
ms.author: jroth
ms.openlocfilehash: d65da0531e9387e94f4d22c734821779c53b9639
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724434"
---
# <a name="query-method-rds"></a>Método Query (RDS)
Usa uma cadeia de caracteres de consulta SQL válida para retornar um [conjunto de registros](../ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Recordset*  
 Uma variável de objeto que representa um objeto **Recordset** .  
  
 *DataFactory*  
 Uma variável de objeto que representa um objeto [RDSServer. datafactory](./datafactory-object-rdsserver.md) .  
  
 *Conexão*  
 Um valor de **cadeia de caracteres** que contém as informações de conexão do servidor. Isso é semelhante à propriedade [Connect](./connect-property-rds.md) .  
  
 *Consulta*  
 Uma **cadeia de caracteres** que contém a consulta SQL.  
  
## <a name="remarks"></a>Comentários  
 A consulta deve usar o dialeto SQL do servidor de banco de dados. Um status de resultado será retornado se houver um erro com a consulta que foi executada. O método de **consulta** não executa nenhuma verificação de sintaxe na cadeia de caracteres de **consulta** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](./datafactory-object-query-method-and-createobject-method-example-vbscript.md)