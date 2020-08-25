---
description: Método CancelUpdate (RDS)
title: Método CancelUpdate (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CancelUpdate method [RDS]
ms.assetid: 76d8a6e9-bc6c-4ea0-8e7a-2bae5ed06650
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b0234a240d863f52d33fe1eb230bcfc11eadf06
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768745"
---
# <a name="cancelupdate-method-rds"></a>Método CancelUpdate (RDS)
Cancela as alterações feitas na linha atual ou nova de um objeto [Recordset](../ado-api/recordset-object-ado.md) .  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.CancelUpdate  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Comentários  
 O serviço de cursor para OLE DB mantém uma cópia dos valores originais e um cache de alterações. Quando você chama **CancelUpdate**, o cache de alterações é redefinido para vazio e todos os controles vinculados são atualizados com os dados originais.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CancelUpdate (VBScript)](./cancelupdate-method-example-vbscript.md)   
 [Botões de comando do catálogo de endereços](../../guide/remote-data-service/address-book-command-buttons.md)   
 [Método Cancel (ADO)](../ado-api/cancel-method-ado.md)   
 [Método Cancel (RDS)](./cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [Método de atualização (RDS)](./refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)