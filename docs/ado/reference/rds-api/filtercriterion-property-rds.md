---
description: Propriedade FilterCriterion (RDS)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1b13b3f3dcdaa2bdd45dabedd5310dc4cdd3db86
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768215"
---
# <a name="filtercriterion-property-rds"></a>Propriedade FilterCriterion (RDS)
Indica o operador de avaliação a ser usado no valor do filtro.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *Cadeia de caracteres*  
 Um valor de **cadeia de caracteres** que especifica o operador de avaliação dos [filtros](./filtervalue-property-rds.md) para os registros. Pode ser qualquer um dos seguintes: <, \<=, > , >=, = ou <>.  
  
## <a name="remarks"></a>Comentários  
 As propriedades [SortColumn](./sortcolumn-property-rds.md), [SortDirection](./sortdirection-property-rds.md), [FilterValue](./filtervalue-property-rds.md), **FilterCriterion**e [FilterColumn](./filtercolumn-property-rds.md) fornecem funcionalidade de classificação e filtragem no cache do lado do cliente. A funcionalidade de classificação ordena registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto o [conjunto de registros](../ado-api/recordset-object-ado.md) completo é mantido no cache. O método [Reset](./reset-method-rds.md) executará os critérios e substituirá o **conjunto** de registros atual por um **conjunto de registros**atualizável.  
  
 O operador "! =" não é válido para **FilterCriterion**; em vez disso, use "<>".  
  
 Se ambas as propriedades Filter e Sort estiverem definidas e você chamar o método **Reset** , o conjunto de linhas será filtrado primeiro e, em seguida, será classificado. Para classificações crescentes, os valores nulos estão na parte superior; para classificações decrescentes, os valores nulos estão na parte inferior (o comportamento padrão é crescente).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection e Método Reset (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade FilterColumn (RDS)](./filtercolumn-property-rds.md)   
 [Propriedade FilterValue (RDS)](./filtervalue-property-rds.md)   
 [Propriedade SortColumn (RDS)](./sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](./sortdirection-property-rds.md)