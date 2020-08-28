---
description: Propriedade URL (RDS)
title: Propriedade de URL (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: rothja
ms.author: jroth
ms.openlocfilehash: d9223d61d7ca2a6463bcd21dd52a0c3aabc51bc5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980907"
---
# <a name="url-property-rds"></a>Propriedade URL (RDS)
Indica uma cadeia de caracteres que contém uma URL relativa ou absoluta.  
  
 Você pode definir a propriedade **URL** em tempo de design na marca de objeto do objeto [DataControl](./datacontrol-object-rds.md) ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Servidor*  
 Um valor de **cadeia de caracteres** que contém uma URL válida.  
  
 *DataControl*  
 Uma variável de objeto que representa um objeto **DataControl** .  
  
## <a name="remarks"></a>Comentários  
 Normalmente, a URL identifica um arquivo de página Active Server (. asp) que pode produzir e retornar um [conjunto de registros](../ado-api/recordset-object-ado.md). Portanto, o usuário pode obter um **conjunto de registros** sem precisar invocar o objeto [DataFactory](./datafactory-object-rdsserver.md) do servidor ou programar um objeto comercial personalizado.  
  
 Se a propriedade de **URL** tiver sido definida, [SubmitChanges](./submitchanges-method-rds.md) enviará as alterações para o local especificado pela URL.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade URL (VBScript)](./url-property-example-vbscript.md)