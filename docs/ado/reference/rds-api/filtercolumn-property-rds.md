---
description: Propriedade FilterColumn (RDS)
title: Propriedade FilterColumn (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterColumn property [ADO]
ms.assetid: 0a5473e8-8ce6-4518-83fb-4920b827e285
author: rothja
ms.author: jroth
ms.openlocfilehash: f4fa38c64a353f6250bc400bf5ed7fc6bf46b95c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722223"
---
# <a name="filtercolumn-property-rds"></a>Propriedade FilterColumn (RDS)
Indica a coluna na qual os critérios de filtro são avaliados.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.FilterColumn = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *Cadeia de caracteres*  
 Um valor de **cadeia de caracteres** que especifica a coluna na qual avaliar os critérios de filtro. Os critérios de filtro são especificados na propriedade [FilterCriterion](./filtercriterion-property-rds.md) .  
  
## <a name="remarks"></a>Comentários  
 As propriedades [SortColumn](./sortcolumn-property-rds.md), [SortDirection](./sortdirection-property-rds.md), [FilterValue](./filtervalue-property-rds.md), [FilterCriterion](./filtercriterion-property-rds.md)e **FilterColumn** fornecem funcionalidade de classificação e filtragem no cache do lado do cliente. A funcionalidade de classificação ordena registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto o [conjunto de registros](../ado-api/recordset-object-ado.md) completo é mantido no cache. O método [Reset](./reset-method-rds.md) executará os critérios e substituirá o **conjunto** de registros atual por um **conjunto de registros**atualizável.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection e Método Reset (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade FilterCriterion (RDS)](./filtercriterion-property-rds.md)   
 [Propriedade FilterValue (RDS)](./filtervalue-property-rds.md)   
 [Propriedade SortColumn (RDS)](./sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](./sortdirection-property-rds.md)