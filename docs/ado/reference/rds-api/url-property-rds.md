---
title: A propriedade URL (RDS) | Microsoft Docs
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d4093321edfca7d1176c4b5be18ee876888b1a2
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600026"
---
# <a name="url-property-rds"></a>Propriedade URL (RDS)
Indica uma cadeia de caracteres que contém uma URL relativa ou absoluta.  
  
 Você pode definir a **URL** propriedade em tempo de design na [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto de marca ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Servidor*  
 Um **cadeia de caracteres** valor que contém uma URL válida.  
  
 *DataControl*  
 Uma variável de objeto que representa um **DataControl** objeto.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, a URL identifica um arquivo de Active Server Page (. asp) que pode gerar e retornar um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). Portanto, o usuário pode obter um **conjunto de registros** sem precisar invocar do lado do servidor [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) de objeto ou programar um objeto comercial personalizado.  
  
 Se o **URL** propriedade foi definida, [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) enviará as alterações para o local especificado pela URL.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade URL (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


