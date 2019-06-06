---
title: Propriedade FilterCriterion (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60f66b1ff2fa7ad7424342da6b92e7d44d0e6444
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712706"
---
# <a name="filtercriterion-property-rds"></a>Propriedade FilterCriterion (RDS)
Indica o operador de avaliação para usar no valor do filtro.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 Um **cadeia de caracteres** valor que especifica o operador de avaliação da [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) os registros. Pode ser qualquer um dos seguintes: <, \<=, >, > =, =, ou <>.  
  
## <a name="remarks"></a>Comentários  
 O [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**, e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propriedades fornecem classificando e filtrando a funcionalidade do cache do lado do cliente. A funcionalidade de classificação ordena os registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto as completas [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) é mantido no cache. O [redefina](../../../ado/reference/rds-api/reset-method-rds.md) método executará os critérios e substituir o atual **conjunto de registros** com um atualizável **conjunto de registros**.  
  
 O "! =" operador não é válido para **FilterCriterion**; em vez disso, use "<>".  
  
 Se o filtro e classificação são definidas e se você chamar o **redefinir** método, o conjunto de linhas é filtrado pela primeira vez e, em seguida, ela é classificada. Para classificações crescentes, os valores nulos são na parte superior; para classificações decrescentes, valores nulos estão na parte inferior (em ordem crescente é o comportamento padrão).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection propriedades e exemplo de método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade FilterColumn (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Propriedade FilterValue (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Propriedade SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


