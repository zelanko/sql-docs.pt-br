---
title: "Ressincronizar método | Microsoft Docs"
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
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 392dd82f2b6412c537a86cc68331cffc852069b8
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="resync-method"></a>Sincronizar de método
Atualiza os dados no atual [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina quantos registros o **Resync** método afetará. O valor padrão é **adAffectAll**. Esse valor não está disponível com o **Resync** método o **campos** coleção de um **registro** objeto.  
  
 *ResyncValues*  
 Opcional. Um [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) valor que especifica se valores subjacentes são substituídos. O valor padrão é **adResyncAllValues**.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o **Resync** método ressincronizar registros no atual **registros** com o banco de dados subjacente. Isso é útil se você estiver usando um cursor estático ou de somente avanço, mas você deseja ver as alterações no banco de dados subjacente.  
  
 Se você definir o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**, **Resync** só está disponível para não somente leitura **registros** objetos.  
  
 Ao contrário a [Requery](../../../ado/reference/ado-api/requery-method.md) método, o **Resync** método não será executada novamente o **Recordset** comando base do objeto. Novos registros no banco de dados subjacente não estarão visíveis.  
  
 Se a tentativa de sincronizar novamente falhar devido a um conflito com os dados subjacentes (por exemplo, um registro foi excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção e um erro de tempo de execução ocorre. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade (**adFilterConflictingRecords**) e o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [comando Resync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) propriedades dinâmicas são definidas e o **registros** é o resultado da execução de uma operação de junção em várias tabelas e, em seguida, o  **Ressincronizar** método executará o comando fornecido no **comando Resync** propriedade apenas na tabela nomeada no **tabela exclusiva** propriedade.  
  
## <a name="fields"></a>Campos  
 Use o **Resync** método para sincronizar novamente os valores da **campos** coleção de um **registro** objeto com a fonte de dados subjacente. O [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade não é afetada por este método.  
  
 Se *ResyncValues* é definido como **adResyncAllValues** (o valor padrão), o [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [valor](../../../ado/reference/ado-api/value-property-ado.md), e [ OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) propriedades de [campo](../../../ado/reference/ado-api/field-object.md) objetos na coleção são sincronizados. Se *ResyncValues* é definido como **adResyncUnderlyingValues**, somente o **UnderlyingValue** propriedade está sincronizada.  
  
 O valor da **Status** propriedade para cada **campo** objeto no momento da chamada também afeta o comportamento de **Resync**. Para **campo** objetos que têm **Status** valores de **adFieldPendingUnknown** ou **adFieldPendingInsert**, **Resync**  não tem nenhum efeito. Para **Status** valores de **adFieldPendingChange** ou **adFieldPendingDelete**, **Resync** sincroniza valores de dados para os campos que ainda existem na fonte de dados.  
  
 **Ressincronizar** não modificará **Status** valores de **campo** objetos a menos que ocorra um erro quando **Resync** é chamado. Por exemplo, se o campo não existir, o provedor retornará adequados **Status** valor para o **campo** objeto, como **adFieldDoesNotExist**. Retornado **Status** valores podem ser combinados logicamente dentro do valor da **Status** propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Sincronizar de exemplo do método (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Sincronizar de exemplo do método (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)

