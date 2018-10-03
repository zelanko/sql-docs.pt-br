---
title: Método Close (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f43e59ed38dfde8091cb851f75a133c60874a6af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644684"
---
# <a name="close-method-ado"></a>Método Close (ADO)
Fecha um objeto aberto e todos os objetos dependentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Use o **feche** método para fechar um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), um [registro](../../../ado/reference/ado-api/record-object-ado.md), um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), ou um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto para liberar quaisquer recursos do sistema associados. Um objeto de fechamento não o remove da memória; Você pode alterar suas configurações de propriedade e abri-lo novamente mais tarde. Para eliminar completamente um objeto da memória, feche o objeto e, em seguida, defina a variável de objeto para *nada* (no Visual Basic).  
  
## <a name="connection"></a>Conexão  
 Usando o **feche** método para fechar um **Conexão** objeto também fecha qualquer ativo **Recordset** objetos associados com a conexão. Um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto associado a **Conexão** objeto você está fechando será mantido, mas não será associado com um **Conexão** objeto; ou seja, sua [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade será definida como **nada**. Além disso, o **comando** do objeto [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção será removida de quaisquer parâmetros definidos pelo provedor.  
  
 Posteriormente, você pode chamar o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método para restabelecer a conexão à mesma ou outra fonte de dados. Enquanto o **Conexão** objeto está fechado, chamar métodos que exigem uma conexão aberta para a fonte de dados gera um erro.  
  
 Fechando um **Conexão** objeto enquanto há aberto **conjunto de registros** objetos sobre a conexão reverte todas as alterações pendentes em todos os **conjunto de registros** objetos. Fechar explicitamente um **Conexão** objeto (chamando o **fechar** método) enquanto uma transação está em andamento gera um erro. Se um **Conexão** objeto sai do escopo, enquanto uma transação está em andamento, ADO automaticamente reverterá a transação.  
  
## <a name="recordset-record-stream"></a>Conjunto de registros, registro, Stream  
 Usando o **feche** método para fechar um **conjunto de registros**, **registro**, ou **Stream** objeto libera os dados associados e qualquer acesso exclusivo Você pode ter tido aos dados através deste objeto específico. Posteriormente, você pode chamar o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) atributos de método para reabrir o objeto com o mesmo, ou modificado,.  
  
 Enquanto um **Recordset** objeto está fechado, chamar métodos que exigem um cursor dinâmico gera um erro.  
  
 Se uma edição está em andamento enquanto estiver no modo de atualização imediata, chamando o **feche** método gera um erro; em vez disso, chame o [atualizar](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primeiro. Se você fechar o **conjunto de registros** do objeto no modo de atualização em lotes, todas as alterações desde a última [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) chamada são perdidas.  
  
 Se você usar o [Clone](../../../ado/reference/ado-api/clone-method-ado.md) método para criar cópias de um aberto **conjunto de registros** do objeto, o original ou um clone de fechamento não afeta nenhuma das outras cópias.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
