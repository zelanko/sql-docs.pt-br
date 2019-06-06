---
title: Método Resync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 251c2f67861dd996ac78efc9a8e599d7ec191072
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711559"
---
# <a name="resync-method"></a>Método Resync
Atualiza os dados no atual [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, ou [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção de um [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto do banco de dados subjacente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Uma [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que determina quantos registros o **ressincronizar** método afetará. O valor padrão é **adAffectAll**. Esse valor não está disponível com o **ressincronizar** método o **campos** coleção de um **registro** objeto.  
  
 *ResyncValues*  
 Opcional. Um [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) valor que especifica se os valores subjacentes são substituídos. O valor padrão é **adResyncAllValues**.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="recordset"></a>Conjunto de registros  
 Use o **ressincronizar** método ressincronizar registros no atual **Recordset** com o banco de dados subjacente. Isso é útil se você estiver usando um cursor estático ou de somente avanço, mas você deseja ver todas as alterações no banco de dados subjacente.  
  
 Se você definir a [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**, **ressincronizar** só está disponível para não somente leitura **Recordset** objetos.  
  
 Ao contrário o [Requery](../../../ado/reference/ado-api/requery-method.md) método, o **ressincronizar** método não será executada novamente o **Recordset** comando subjacente do objeto. Novos registros no banco de dados subjacente não será visíveis.  
  
 Se a tentativa de sincronizar novamente falhar devido a um conflito com os dados subjacentes (por exemplo, um registro tiver sido excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção e um erro de tempo de execução ocorre. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade (**adFilterConflictingRecords**) e o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [comando ressincronizar](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) as propriedades dinâmicas são definidas e o **Recordset** é o resultado da execução de uma operação de junção em várias tabelas e, em seguida, o  **Ressincronizar** método executará o comando fornecido em de **comando ressincronizar** propriedade somente na tabela nomeada no **tabela exclusiva** propriedade.  
  
## <a name="fields"></a>Campos  
 Use o **ressincronizar** método para sincronizar novamente os valores da **campos** coleção de um **registro** objeto com a fonte de dados subjacente. O [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade não é afetada por esse método.  
  
 Se *ResyncValues* é definido como **adResyncAllValues** (o valor padrão), o [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [valor](../../../ado/reference/ado-api/value-property-ado.md), e [ Exemplo de OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) propriedades de [campo](../../../ado/reference/ado-api/field-object.md) objetos na coleção são sincronizados. Se *ResyncValues* é definido como **adResyncUnderlyingValues**, somente o **UnderlyingValue** propriedade está sincronizada.  
  
 O valor da **Status** propriedade para cada **campo** objeto no momento da chamada também afeta o comportamento de **ressincronizar**. Para **campo** objetos que têm **Status** valores de **adFieldPendingUnknown** ou **adFieldPendingInsert**, **de ressincronização**  não tem nenhum efeito. Para **Status** valores de **adFieldPendingChange** ou **adFieldPendingDelete**, **ressincronizar** sincroniza valores de dados para campos que ainda existem na fonte de dados.  
  
 **Ressincronizar** não modificará **Status** valores de **campo** objetos, a menos que ocorra um erro quando **ressincronizar** é chamado. Por exemplo, se o campo não existir, o provedor retornará apropriado **Status** valor para o **campo** objeto, como **adFieldDoesNotExist**. Retornado **Status** valores podem ser combinados logicamente dentro do valor da **Status** propriedade.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Coleção Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Ressincronização de exemplo do método (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Ressincronização de exemplo do método (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
