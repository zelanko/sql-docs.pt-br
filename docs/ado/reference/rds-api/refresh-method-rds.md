---
description: Método Refresh (RDS)
title: Método de atualização (RDS) | Microsoft Docs
ms.technology: connectivity
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
ms.openlocfilehash: 372d4a2506f5ea7d14905ffed0842ca5cf2ce6ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438708"
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Consulta novamente a fonte de dados especificada na propriedade [Connect](../../../ado/reference/rds-api/connect-property-rds.md) e atualiza os resultados da consulta.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Comentários  
 Você deve definir as propriedades de [conectar](../../../ado/reference/rds-api/connect-property-rds.md), [servidor](../../../ado/reference/rds-api/server-property-rds.md)e [SQL](../../../ado/reference/rds-api/sql-property.md) antes de usar o método de **atualização** . Todos os controles associados a dados no formulário associado a um **RDS. O objeto DataControl** refletirá o novo conjunto de registros. Qualquer objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) já existente é liberado e todas as alterações não salvas são descartadas. O método **Refresh** automaticamente transforma o primeiro registro no registro atual.  
  
 É uma boa ideia chamar o método **Refresh** periodicamente quando você trabalha com dados. Se você recuperar dados e deixá-los em um computador cliente por algum tempo, é provável que ele fique desatualizado. É possível que as alterações feitas falhem, pois outra pessoa pode ter alterado o registro e enviado alterações antes de você.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Exemplo do método Refresh (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


