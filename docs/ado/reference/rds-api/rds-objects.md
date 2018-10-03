---
title: Objetos RDS | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- objects [ADO], RDS
- RDS objects [ADO]
ms.assetid: f2ac8b3b-f968-41c4-a504-7aee3538b7c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 378b0f593159a93f580338d5088dfd512f82af06
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601854"
---
# <a name="rds-objects"></a>Objetos RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
|||  
|-|-|  
|[DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Associa uma consulta de dados **conjunto de registros** para um ou mais controles (por exemplo, uma caixa de texto, controle de grade ou caixa de combinação) para exibir o **Recordset** dados em uma página da Web.<br /><br /> O **DataControl** objeto é seguro para script.|  
|[DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Implementa métodos que fornecem acesso a dados para leitura/gravação especificada fontes de dados para aplicativos do lado do cliente.<br /><br /> O **DataFactory** objeto não é seguro para script.|  
|[DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)|Cria os proxies do lado do cliente a objetos comerciais personalizados localizados na camada intermediária.<br /><br /> O **DataSpace** objeto é seguro para script.|  
|[Interface IRDSService (RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)|Expõe o [InvokeService (RDS)](../../../ado/reference/rds-api/invokeservice-rds.md) método, que é usado para retornar um ponteiro para a interface solicitada em uma versão mais robustos do objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API RDS](../../../ado/reference/rds-api/rds-api-reference.md)


