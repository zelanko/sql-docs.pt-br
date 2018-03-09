---
title: "Método SubmitChanges (RDS) | Microsoft Docs"
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c5e6131490f2e1e39b0ab9d038b13af67ec52047
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envia as alterações de localmente em cache e atualizáveis pendentes [registros](../../../ado/reference/ado-api/recordset-object-ado.md) à fonte de dados especificado no [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propriedade ou o [URL](../../../ado/reference/rds-api/url-property-rds.md) propriedade.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *DataFactory*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexão*  
 Um **cadeia de caracteres** valor que representa a conexão criada com o **RDS. DataControl** do objeto [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propriedade.  
  
 *Recordset*  
 Uma variável de objeto que representa um **registros** objeto.  
  
## <a name="remarks"></a>Remarks  
 O [conectar](../../../ado/reference/rds-api/connect-property-rds.md), [servidor](../../../ado/reference/rds-api/server-property-rds.md), e [SQL](../../../ado/reference/rds-api/sql-property.md) propriedades devem ser definidas antes de usar o **SubmitChanges** método com o  **RDS. DataControl** objeto.  
  
 Se você chamar o [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método depois de ter chamado **SubmitChanges** para o mesmo **registros** objeto, o **CancelUpdate** chamada falhar porque as alterações já foram confirmadas.  
  
 Somente os registros alterados são enviados para modificação e todas as alterações tenha êxito ou falham de todas as alterações em conjunto.  
  
 Você pode usar **SubmitChanges** somente com o padrão **RDSServer.DataFactory** objeto. Objetos de negócios personalizada não podem usar esse método.  
  
 Se o **URL** propriedade foi definida, **SubmitChanges** enviar alterações para o local especificado pela URL.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



