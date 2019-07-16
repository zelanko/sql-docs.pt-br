---
title: Propriedade SortColumn (RDS) | Microsoft Docs
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5a9c3f9f50968f3b5e8085052917397bcd90226
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963400"
---
# <a name="sortcolumn-property-rds"></a>Propriedade SortColumn (RDS)
Indica por qual coluna para classificar os registros.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Cadeia de caracteres*  
 Um **cadeia de caracteres** valor que representa o nome ou alias da coluna pela qual classificar os registros.  
  
## <a name="remarks"></a>Comentários  
 O **SortColumn**, [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propriedades fornecem classificando e filtrando a funcionalidade do cache do lado do cliente. A funcionalidade de classificação ordena os registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em critérios de localização, enquanto as completas [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) é mantido no cache. O [redefina](../../../ado/reference/rds-api/reset-method-rds.md) método executará os critérios e substituir o atual **conjunto de registros** com um atualizável **conjunto de registros**.  
  
 Para classificar em uma **Recordset**, primeiro você deve salvar todas as alterações pendentes. Se você estiver usando o **RDS. DataControl**, você pode usar o [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) método. Por exemplo, se seu **RDS. DataControl** é chamado ADC1, seu código seria `ADC1.SubmitChanges`. Se você estiver usando o ADO **conjunto de registros**, você pode usar seu [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Usando o **UpdateBatch** é o método recomendado para **conjunto de registros** objetos criados com o [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método. Por exemplo, seu código pode ser `myRS.UpdateBatch` ou `ADC1.Recordset.UpdateBatch`.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn e SortDirection propriedades e exemplo de método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propriedade de classificação](../../../ado/reference/ado-api/sort-property.md)   
 [Propriedade SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





