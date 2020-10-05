---
description: Método Refresh (RDS)
title: Método de atualização (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e6fb32744d64f99beac6c414f1b82581b9fadcb
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724268"
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Consulta novamente a fonte de dados especificada na propriedade [Connect](./connect-property-rds.md) e atualiza os resultados da consulta.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Comentários  
 Você deve definir as propriedades de [conectar](./connect-property-rds.md), [servidor](./server-property-rds.md)e [SQL](./sql-property.md) antes de usar o método de **atualização** . Todos os controles associados a dados no formulário associado a um **RDS. O objeto DataControl** refletirá o novo conjunto de registros. Qualquer objeto [Recordset](../ado-api/recordset-object-ado.md) já existente é liberado e todas as alterações não salvas são descartadas. O método **Refresh** automaticamente transforma o primeiro registro no registro atual.  
  
 É uma boa ideia chamar o método **Refresh** periodicamente quando você trabalha com dados. Se você recuperar dados e deixá-los em um computador cliente por algum tempo, é provável que ele fique desatualizado. É possível que as alterações feitas falhem, pois outra pessoa pode ter alterado o registro e enviado alterações antes de você.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Refresh (VB)](../ado-api/refresh-method-example-vb.md)   
 [Exemplo do método Refresh (VBScript)](./refresh-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](./cancelupdate-method-rds.md)   
 [Método Refresh (ADO)](../ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)