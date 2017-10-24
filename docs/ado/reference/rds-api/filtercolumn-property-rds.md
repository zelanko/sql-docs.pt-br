---
title: Propriedade FilterColumn (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- FilterColumn property [ADO]
ms.assetid: 0a5473e8-8ce6-4518-83fb-4920b827e285
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdbb6928ed7d4e1de956ff05e36723b907cda282
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="filtercolumn-property-rds"></a>Propriedade FilterColumn (RDS)
Indica a coluna na qual avaliar os critérios de filtro.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.FilterColumn = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Cadeia de caracteres*  
 Um **cadeia de caracteres** valor que especifica a coluna na qual avaliar os critérios de filtro. Os critérios de filtro são especificados no [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md) propriedade.  
  
## <a name="remarks"></a>Comentários  
 O [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), e **FilterColumn**propriedades fornecem a classificação e filtragem de funcionalidade no cache do lado do cliente. A funcionalidade de classificação ordena os registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto o completo [registros](../../../ado/reference/ado-api/recordset-object-ado.md) é mantido no cache. O [redefinir](../../../ado/reference/rds-api/reset-method-rds.md) método executará os critérios e substitua atual **registros** com um atualizável **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn e propriedades SortDirection e exemplo de método de redefinição (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade FilterCriterion (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [Propriedade FilterValue (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Propriedade SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)



