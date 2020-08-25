---
description: Propriedade FilterValue (RDS)
title: Propriedade FilterValue (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a609f9b87ce94251cc5d0c3d79e82f4abe2e7df
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768195"
---
# <a name="filtervalue-property-rds"></a>Propriedade FilterValue (RDS)
Indica o valor com o qual filtrar os registros.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *Cadeia de caracteres*  
 Um valor de **cadeia de caracteres** que representa um valor de dados com o qual filtrar registros (por exemplo, `'Programmer'` ou `125` ).  
  
## <a name="remarks"></a>Comentários  
 As propriedades [SortColumn](./sortcolumn-property-rds.md), [SortDirection](./sortdirection-property-rds.md), **FilterValue**, [FilterCriterion](./filtercriterion-property-rds.md)e [FilterColumn](./filtercolumn-property-rds.md) fornecem funcionalidade de classificação e filtragem no cache do lado do cliente. A funcionalidade de classificação ordena registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto o [conjunto de registros](../ado-api/recordset-object-ado.md) completo é mantido no cache. O método [Reset](./reset-method-rds.md) executará os critérios e substituirá o **conjunto** de registros atual por um **conjunto de registros**atualizável.  
  
 Valores nulos resultam em um erro de tipo incompatível.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection e Método Reset (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade FilterColumn (RDS)](./filtercolumn-property-rds.md)   
 [Propriedade FilterCriterion (RDS)](./filtercriterion-property-rds.md)   
 [Propriedade SortColumn (RDS)](./sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](./sortdirection-property-rds.md)