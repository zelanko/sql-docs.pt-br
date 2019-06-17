---
title: Consulta de método (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 92247a31eeb5f3e70b54edfaff33ae15340b9df1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712425"
---
# <a name="query-method-rds"></a>Método Query (RDS)
Usa uma cadeia de caracteres de consulta SQL válida para retornar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Recordset*  
 Uma variável de objeto que representa um **Recordset** objeto.  
  
 *DataFactory*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexão*  
 Um **cadeia de caracteres** valor que contém as informações de conexão do servidor. Isso é semelhante a [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propriedade.  
  
 *Consulta*  
 Um **cadeia de caracteres** que contém a consulta SQL.  
  
## <a name="remarks"></a>Comentários  
 A consulta deve usar o dialeto SQL do servidor de banco de dados. Um status de resultado é retornado se não houver um erro com a consulta que foi executado. O **consulta** método não realiza qualquer sintaxe verificando o **consulta** cadeia de caracteres.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


