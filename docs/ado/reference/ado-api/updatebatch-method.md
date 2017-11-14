---
title: "Método UpdateBatch | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57c85b6ed83792e2e489eb91dab59bd0da598939
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="updatebatch-method"></a>Método UpdateBatch
Grava todas as atualizações em lotes pendentes no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valor que indica quantos registros o **UpdateBatch** método afetará.  
  
 *PreserveStatus*  
 Opcional. Um **booliano** valor que especifica se as alterações locais, conforme indicado pelo [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade devem ser confirmadas. Se esse valor é definido como **True**, o **Status** propriedade de cada registro permanecerá inalterada depois que a atualização seja concluída.  
  
## <a name="remarks"></a>Comentários  
 Use o **UpdateBatch** método ao modificar um **registros** objeto no modo de atualização em lotes para transmitir todas as alterações feitas em um **Recordset** objeto no banco de dados subjacente.  
  
 Se o **registros** objeto oferece suporte a atualização em lotes, você pode armazenar em cache várias alterações para um ou mais registros localmente até que você chame o **UpdateBatch** método. Se você estiver editando o registro atual ou adicionar um novo registro, quando você chama o **UpdateBatch** método ADO automaticamente chamará o [atualização](../../../ado/reference/ado-api/update-method.md) método para salvar as alterações pendentes para o registro atual antes de transmitir as alterações em lotes para o provedor. Você deve usar o lote com um conjunto de chaves ou um cursor estático somente a atualização.  
  
> [!NOTE]
>  Especificando **adAffectGroup** como o valor para esse parâmetro resultará em um erro quando não há nenhum registro visível no atual **registros** (como um filtro para que nenhum registro correspondente).  
  
 Se a tentativa de transmitir as alterações falhar por algum ou todos os registros devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos para o [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção e um Erro de tempo de execução. Use o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade (**adFilterAffectedRecords**) e o [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) propriedade para localizar registros com conflitos.  
  
 Para cancelar todas as atualizações em lotes, use o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) método.  
  
 Se o [tabela exclusiva](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [atualização Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propriedades dinâmicas são definidas e o **registros** é o resultado da execução de uma operação de junção em várias tabelas, o execução do **UpdateBatch** método implicitamente é seguido a [Resync](../../../ado/reference/ado-api/resync-method.md) método, dependendo das configurações do [atualização Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) propriedade.  
  
 A ordem na qual as atualizações individuais de um lote são executadas na fonte de dados não é necessariamente o mesmo que a ordem na qual eles foram realizados no local **registros**. Ordem de atualização depende do provedor. Leve isso em conta ao codificar as atualizações que estão relacionadas uns aos outros, como restrições de chave estrangeira em uma inserção ou atualização.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de métodos de CancelBatch (VB) e UpdateBatch](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch e exemplo dos métodos CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Propriedade LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Método Update](../../../ado/reference/ado-api/update-method.md)

