---
title: "Consulta de método (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53647d80b2e6110e5af084e6a3f983381ced1690
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="query-method-rds"></a>Método Query (RDS)
Usa uma cadeia de caracteres de consulta SQL válida para retornar um [registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Conjunto de registros*  
 Uma variável de objeto que representa um **registros** objeto.  
  
 *DataFactory*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexão*  
 Um **cadeia de caracteres** valor que contém as informações de conexão do servidor. Isso é semelhante de [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propriedade.  
  
 *Consulta*  
 Um **cadeia de caracteres** que contém a consulta SQL.  
  
## <a name="remarks"></a>Comentários  
 A consulta deve usar o dialeto SQL do servidor de banco de dados. Um status de resultado é retornado se não houver um erro com a consulta que foi executado. O **consulta** método não executa qualquer verificação de sintaxe de **consulta** cadeia de caracteres.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)



