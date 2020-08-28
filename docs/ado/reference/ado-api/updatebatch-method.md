---
description: Método UpdateBatch
title: Método UpdateBatch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 648e6f8e64d4001851afb3838c901ab2b1172108
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987997"
---
# <a name="updatebatch-method"></a>Método UpdateBatch
Grava todas as atualizações de lote pendentes no disco.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *AffectRecords*  
 Opcional. Um valor [AffectEnum](./affectenum.md) que indica quantos registros o método **UpdateBatch** afetará.  
  
 *PreserveStatus*  
 Opcional. Um valor **booliano** que especifica se as alterações locais, conforme indicado pela propriedade [status](./status-property-ado-recordset.md) , devem ser confirmadas. Se esse valor for definido como **true**, a propriedade **status** de cada registro permanecerá inalterada depois que a atualização for concluída.  
  
## <a name="remarks"></a>Comentários  
 Use o método **UpdateBatch** ao modificar um objeto **Recordset** no modo de atualização do lote para transmitir todas as alterações feitas em um objeto **Recordset** para o banco de dados subjacente.  
  
 Se o objeto **Recordset** oferecer suporte à atualização em lotes, você poderá armazenar em cache várias alterações em um ou mais registros localmente até chamar o método **UpdateBatch** . Se você estiver editando o registro atual ou adicionando um novo registro ao chamar o método **UpdateBatch** , o ADO chamará automaticamente o método [Update](./update-method.md) para salvar as alterações pendentes no registro atual antes de transmitir as alterações em lote para o provedor. Você deve usar a atualização em lotes somente com um conjunto de chaves ou cursor estático.  
  
> [!NOTE]
>  Especificar **adAffectGroup** como o valor desse parâmetro resultará em um erro quando não houver nenhum registro visível no **conjunto de registros** atual (como um filtro para o qual nenhum registro corresponde).  
  
 Se a tentativa de transmitir alterações falhar para qualquer ou todos os registros devido a um conflito com os dados subjacentes (por exemplo, um registro já foi excluído por outro usuário), o provedor retornará avisos à coleção de [erros](./errors-collection-ado.md) e ocorrerá um erro em tempo de execução. Use a propriedade [Filter](./filter-property.md) (**adFilterAffectedRecords**) e a propriedade [status](./status-property-ado-recordset.md) para localizar registros com conflitos.  
  
 Para cancelar todas as atualizações de lote pendentes, use o método [CancelBatch](./cancelbatch-method-ado.md) .  
  
 Se a [tabela exclusiva](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e a atualização de propriedades dinâmicas de [ressincronização](./update-resync-property-dynamic-ado.md) forem definidas e o **conjunto de registros** for o resultado da execução de uma operação de junção em várias tabelas, a execução do método **UpdateBatch** será implicitamente seguida pelo método de [ressincronização](./resync-method.md) , dependendo das configurações da propriedade [Atualizar ressincronização](./update-resync-property-dynamic-ado.md) .  
  
 A ordem na qual as atualizações individuais de um lote são executadas na fonte de dados não é necessariamente a mesma ordem na qual elas foram executadas no **conjunto de registros**local. A ordem de atualização depende do provedor. Leve isso em conta ao codificar atualizações relacionadas entre si, como restrições de chave estrangeira em uma inserção ou atualização.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos UpdateBatch e CancelBatch (VB)](./updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Exemplo dos métodos UpdateBatch e CancelBatch (VC + +)](./updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Método CancelBatch (ADO)](./cancelbatch-method-ado.md)   
 [Método Clear (ADO)](./clear-method-ado.md)   
 [Propriedade LockType (ADO)](./locktype-property-ado.md)   
 [Método Update](./update-method.md)