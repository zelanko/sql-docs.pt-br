---
title: Método GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4df52f5ebc2fee80017f284c78cb49e4cb36667b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278795"
---
# <a name="getrows-method-ado"></a>Método GetRows (ADO)
Recupera vários registros de uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto em uma matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um **Variant** cujo valor é uma matriz bidimensional.  
  
#### <a name="parameters"></a>Parâmetros  
 *Linhas*  
 Opcional. Um [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) valor que indica o número de registros a serem recuperados. O padrão é **adGetRowsRest**.  
  
 *Iniciar*  
 Opcional. Um **cadeia de caracteres** valor ou **Variant** que é avaliada para o indicador para o registro do que o **GetRows** comece a operação. Você também pode usar um [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
 *Fields*  
 Opcional. Um **Variant** que representa um único nome de campo ou a posição ordinal ou uma matriz de nomes de campo ou números de posição ordinal. ADO retorna apenas os dados nesses campos.  
  
## <a name="remarks"></a>Remarks  
 Use o **GetRows** método para copiar os registros de um **registros** em uma matriz bidimensional. O primeiro subscrito identifica o campo e o segundo identifica o número do registro. O *matriz* variável é dimensionada automaticamente para o correto quando o tamanho de **GetRows** método retorna os dados.  
  
 Se você não especificar um valor para o *linhas* argumento, o **GetRows** método automaticamente recupera todos os registros de **Recordset** objeto. Se você solicitar registros que não estão disponíveis, **GetRows** retorna somente o número de registros disponíveis.  
  
 Se o **registros** objeto dá suporte a indicadores, você pode especificar em qual registro o **GetRows** método deve começar a recuperação de dados, passando o valor do registro [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)propriedade o *iniciar* argumento.  
  
 Se você quiser restringir os campos que o **GetRows** chamada retorna, você pode passar um único campo nome/número ou uma matriz de nomes de campo/números no *campos* argumento.  
  
 Depois de chamar **GetRows**, o próximo registro não lido torna-se o registro atual, ou o [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) está definida como **True** se não houver nenhuma mais registros.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Exemplo do método GetRows (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
