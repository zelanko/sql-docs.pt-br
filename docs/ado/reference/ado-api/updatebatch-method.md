---
title: Método UpdateBatch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e39b7094b4b4543b60431f847ed792f18ace31f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47683614"
---
# <a name="updatebatch-method"></a>Método UpdateBatch
Grava todas as atualizações em lotes pendentes no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Uma [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que indica quantos registros o **UpdateBatch** método afetará.  
  
 *PreserveStatus*  
 Opcional. Um **Boolean** valor que especifica se as alterações locais, conforme indicado pelo [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade, deve ser confirmada. Se esse valor é definido como **verdadeira**, o **Status** propriedade de cada registro permanecerá inalterada depois que a atualização for concluída.  
  
## <a name="remarks"></a>Comentários  
 Use o **UpdateBatch** método ao modificar um **conjunto de registros** objeto no modo de atualização em lotes para transmitir todas as alterações feitas em um **Recordset** objeto no banco de dados subjacente.  
  
 Se o **conjunto de registros** objeto dá suporte à atualização em lotes, você pode armazenar em cache várias alterações para um ou mais registros localmente até que você chame a **UpdateBatch** método. Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o **UpdateBatch** método, ADO chamará automaticamente a [atualização](../../../ado/reference/ado-api/update-method.md) método para salvar todas as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor. Você deve usar o lote de atualização com um conjunto de chaves ou apenas o cursor estático.  
  
> [!NOTE]
>  Especificando **adAffectGroup** como o valor para esse parâmetro resulta em um erro quando não há registros visíveis atual **Recordset** (como um filtro para os quais não há registros correspondem).  
  
 Se a tentativa para transmitir as alterações falhar por qualquer ou todos os registros devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção e um Erro de tempo de execução ocorre. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade (**adFilterAffectedRecords**) e o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
 Para cancelar todas as atualizações em lotes, use o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [atualização ressincronizar](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propriedades dinâmicas são definidas e o **conjunto de registros** é o resultado da execução de uma operação de junção em várias tabelas, em seguida, a execução do **UpdateBatch** método implicitamente é seguido pela [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método, dependendo das configurações da [atualização ressincronizar](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propriedade.  
  
 A ordem na qual as atualizações individuais de um lote são executadas na fonte de dados não é necessariamente o mesmo que a ordem na qual eles foram realizados no local **conjunto de registros**. Ordem de atualização depende do provedor. Leve isso em conta ao codificar as atualizações que estão relacionadas uns aos outros, como restrições de chave estrangeiras em uma inserção ou atualização.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de UpdateBatch e CancelBatch exemplo dos métodos (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Exemplo de UpdateBatch e CancelBatch exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)
