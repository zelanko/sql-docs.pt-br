---
title: Método Refresh (RDS) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ba03aa3be2b644dfbd554528824162a75bc30a2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47691044"
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Repete a consulta a fonte de dados especificada na [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propriedade e atualizações, os resultados da consulta.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 Você deve definir a [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), e [SQL](../../../ado/reference/rds-api/sql-property.md) propriedades antes de usar o **atualizar** método. Todos os controles ligados a dados no formulário associado com um **RDS. DataControl** objeto refletirão o novo conjunto de registros. Qualquer pré-existentes [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto é liberado, e as alterações não salvas serão descartadas. O **Refresh** método automaticamente torna o primeiro registro o registro atual.  
  
 É uma boa ideia chamar o **Refresh** método periodicamente quando você trabalha com dados. Se você recupera dados e, em seguida, deixe-a em um computador cliente por algum tempo, é provável ficar desatualizado. É possível que as alterações que você fizer falhará, porque outra pessoa pode ter alterado o registro e enviado as alterações antes de você.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método exemplo Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [(VBScript) de exemplo do método Refresh](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


