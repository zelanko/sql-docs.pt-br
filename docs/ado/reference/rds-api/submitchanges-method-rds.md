---
title: Método SubmitChanges (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a11adb93f3de8f0887eefe964f1c85836ccc43e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750581"
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envia alterações pendentes do [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) armazenado em cache e atualizável localmente para a fonte de dados especificada na propriedade [Connect](../../../ado/reference/rds-api/connect-property-rds.md) ou a propriedade [URL](../../../ado/reference/rds-api/url-property-rds.md) .  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *DataFactory*  
 Uma variável de objeto que representa um objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *Conexão*  
 Um valor de **cadeia de caracteres** que representa a conexão criada com o **RDS. **Propriedade [Connect](../../../ado/reference/rds-api/connect-property-rds.md) do objeto DataControl.  
  
 *Recordset*  
 Uma variável de objeto que representa um objeto **Recordset** .  
  
## <a name="remarks"></a>Comentários  
 As propriedades [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)e [SQL](../../../ado/reference/rds-api/sql-property.md) devem ser definidas antes que você possa usar o método **SubmitChanges** com o **RDS. Objeto DataControl** .  
  
 Se você chamar o método [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) depois de ter chamado **SubmitChanges** para o mesmo objeto **Recordset** , a chamada **CancelUpdate** falhará porque as alterações já foram confirmadas.  
  
 Somente os registros alterados são enviados para modificação e todas as alterações são bem sucedidas ou todas as alterações falham juntas.  
  
 Você pode usar **SubmitChanges** somente com o objeto **RDSServer. datafactory** padrão. Os objetos comerciais personalizados não podem usar esse método.  
  
 Se a propriedade de **URL** tiver sido definida, **SubmitChanges** enviará as alterações para o local especificado pela URL.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



