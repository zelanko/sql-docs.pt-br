---
description: Método SubmitChanges (RDS)
title: Método SubmitChanges (RDS) | Microsoft Docs
ms.technology: ado
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
ms.openlocfilehash: 69a76648c676af5c6420cffde930ac76c096276d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724170"
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envia alterações pendentes do [conjunto de registros](../ado-api/recordset-object-ado.md) armazenado em cache e atualizável localmente para a fonte de dados especificada na propriedade [Connect](./connect-property-rds.md) ou a propriedade [URL](./url-property-rds.md) .  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *DataFactory*  
 Uma variável de objeto que representa um objeto [RDSServer. datafactory](./datafactory-object-rdsserver.md) .  
  
 *Conexão*  
 Um valor de **cadeia de caracteres** que representa a conexão criada com o **RDS. ** Propriedade [Connect](./connect-property-rds.md) do objeto DataControl.  
  
 *Recordset*  
 Uma variável de objeto que representa um objeto **Recordset** .  
  
## <a name="remarks"></a>Comentários  
 As propriedades [Connect](./connect-property-rds.md), [Server](./server-property-rds.md)e [SQL](./sql-property.md) devem ser definidas antes que você possa usar o método **SubmitChanges** com o **RDS. Objeto DataControl** .  
  
 Se você chamar o método [CancelUpdate](./cancelupdate-method-rds.md) depois de ter chamado **SubmitChanges** para o mesmo objeto **Recordset** , a chamada **CancelUpdate** falhará porque as alterações já foram confirmadas.  
  
 Somente os registros alterados são enviados para modificação e todas as alterações são bem sucedidas ou todas as alterações falham juntas.  
  
 Você pode usar **SubmitChanges** somente com o objeto **RDSServer. datafactory** padrão. Os objetos comerciais personalizados não podem usar esse método.  
  
 Se a propriedade de **URL** tiver sido definida, **SubmitChanges** enviará as alterações para o local especificado pela URL.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método SubmitChanges (VBScript)](./submitchanges-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](./cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](./refresh-method-rds.md)