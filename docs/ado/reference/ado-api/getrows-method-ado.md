---
title: Exemplo do método GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65d346cb9394613a92f95f7466e429b10c54b1a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616955"
---
# <a name="getrows-method-ado"></a>Método GetRows (ADO)
Recupera vários registros de uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto em uma matriz.  
  
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
 Opcional. Um **cadeia de caracteres** valor ou **Variant** que é avaliada para o indicador para o registro do que o **GetRows** deve começar a operação. Você também pode usar um [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
 *Fields*  
 Opcional. Um **Variant** que representa um nome de campo único ou posição ordinal ou uma matriz de nomes de campo ou números de posição ordinal. ADO retorna apenas os dados nesses campos.  
  
## <a name="remarks"></a>Comentários  
 Use o **GetRows** método para copiar os registros de uma **conjunto de registros** em uma matriz bidimensional. O primeiro subscrito identifica o campo e o segundo identifica o número do registro. O *matriz* variável é dimensionada automaticamente para a correta de tamanho quando o **GetRows** método retorna os dados.  
  
 Se você não especificar um valor para o *linhas* argumento, o **GetRows** método recupera todos os registros automaticamente o **Recordset** objeto. Se você solicitar mais registros que estão disponíveis, **GetRows** retorna somente o número de registros disponíveis.  
  
 Se o **conjunto de registros** objeto dá suporte a indicadores, você pode especificar em qual registro o **GetRows** método deve começar a recuperação de dados, passando o valor desse registro [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md)propriedade de *iniciar* argumento.  
  
 Se você quiser restringir os campos que o **GetRows** chamada retornar, você pode passar um único campo nome/número ou uma matriz de nomes de campo/números na *campos* argumento.  
  
 Depois de chamar **GetRows**, o próximo registro não lido torna-se o registro atual, ou o [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) estiver definida como **verdadeiro** se não há mais registros.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Exemplo do método GetRows (VC++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
