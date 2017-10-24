---
title: "Redefinir o método (RDS) | Microsoft Docs"
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
- Reset method [ADO]
ms.assetid: 3957197a-f543-4d6b-9e11-67a77c2063b7
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 753a34ee7600ace3c5236df2c206a60255cc1a6f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="reset-method-rds"></a>Método Reset (RDS)
Executa a classificação ou o filtro em um cliente **registros** com base nas propriedades de classificação e filtro especificadas.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Reset(value)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *value*  
 Opcional. Um **booliano** valor que é **True** (padrão), se você deseja filtrar o conjunto de linhas "filtrado" atual. **False** indica que você filtrar o conjunto de linhas original, removendo qualquer opção de filtro anterior.  
  
## <a name="remarks"></a>Comentários  
 O [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propriedades fornecem a classificação e filtragem de funcionalidade no cache do lado do cliente. A funcionalidade de classificação ordena os registros por valores de uma coluna. A funcionalidade de filtragem exibe um subconjunto de registros com base em um critério de localização, enquanto o completo [registros](../../../ado/reference/ado-api/recordset-object-ado.md) é mantido no cache. O **redefinir** método executará os critérios e substitua atual **registros** com um atualizável **registros**.  
  
 Se houver alterações nos dados originais que não tenham sido enviadas, o **redefinir** método irá falhar. Primeiro, use o [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) método para salvar as alterações em uma leitura/gravação **registros**e, em seguida, use o **redefinir** método para classificar ou filtrar os registros.  
  
 Se você quiser executar mais de um filtro em seu conjunto de linhas, você pode usar opcional *booliano* argumento com o **redefinir** método. O exemplo a seguir mostra como fazer isso:  
  
```  
ADC.SQL = "Select au_lname from authors"  
ADC.Refresh    ' Get the new rowset.  
  
ADC.FilterColumn = "au_lname"  
ADC.FilterCriterion = "<"  
ADC.FilterValue = "'M'"  
ADC.Reset         ' Rowset now has all Last Names < "M".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'F'"  
' Passing True is not necessary, because it is the   
' default filter on the current "filtered" rowset.  
ADC.Reset(TRUE)     ' Rowset now has all Last   
                    ' Names < "M" and > "F".  
  
ADC.FilterCriterion = ">"  
ADC.FilterValue = "'T'"  
' Filter on the original rowset, throwing out the  
' previous filter options.  
ADC.Reset(FALSE)   ' Rowset now has all Last Names > "T".  
```  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn e propriedades SortDirection e exemplo de método de redefinição (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)




