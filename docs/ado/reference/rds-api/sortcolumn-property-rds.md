---
description: Propriedade SortColumn (RDS)
title: Propriedade SortColumn (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: rothja
ms.author: jroth
ms.openlocfilehash: 62187b1643c315099d40d0bdd878699fcfc0065c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724223"
---
# <a name="sortcolumn-property-rds"></a>Propriedade SortColumn (RDS)
Indica por qual coluna classificar os registros.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. Objeto DataControl](./datacontrol-object-rds.md) .  
  
 *Cadeia de caracteres*  
 Um valor de **cadeia de caracteres** que representa o nome ou alias da coluna pela qual classificar os registros.  
  
## <a name="remarks"></a>Comentários  
 As propriedades **SortColumn**, [SortDirection](./sortdirection-property-rds.md), [FilterValue](./filtervalue-property-rds.md), [FilterCriterion](./filtercriterion-property-rds.md)e [FilterColumn](./filtercolumn-property-rds.md) fornecem funcionalidade de classificação e filtragem no cache do lado do cliente. A funcionalidade de classificação ordena registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto o [conjunto de registros](../ado-api/recordset-object-ado.md) completo é mantido no cache. O método [Reset](./reset-method-rds.md) executará os critérios e substituirá o **conjunto** de registros atual por um **conjunto de registros**atualizável.  
  
 Para classificar em um **conjunto de registros**, você deve primeiro salvar as alterações pendentes. Se você estiver usando o **RDS. DataControl**, você pode usar o método [SubmitChanges](./submitchanges-method-rds.md) . Por exemplo, se o seu **RDS. O DataControl** é chamado de ADC1, o seu código seria `ADC1.SubmitChanges` . Se você estiver usando um **conjunto de registros**ADO, poderá usar seu método [UpdateBatch](../ado-api/updatebatch-method.md) . O uso de **UpdateBatch** é o método recomendado para objetos **Recordset** criados com o método [createrecordset](./createrecordset-method-rds.md) . Por exemplo, seu código pode ser `myRS.UpdateBatch` ou `ADC1.Recordset.UpdateBatch` .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection e Método Reset (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade de classificação](../ado-api/sort-property.md)   
 [Propriedade SortDirection (RDS)](./sortdirection-property-rds.md)