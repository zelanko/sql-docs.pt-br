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
ms.openlocfilehash: 8a1d153d1433a377bb488366111b75a986365132
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919939"
---
# <a name="close-method-ado"></a>Método Close (ADO)
Fecha um objeto aberto e quaisquer objetos dependentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Use o método **Close** para fechar uma [conexão](../../../ado/reference/ado-api/connection-object-ado.md), um [registro](../../../ado/reference/ado-api/record-object-ado.md), um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)ou um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) para liberar todos os recursos do sistema associados. Fechar um objeto não o Remove da memória; Você pode alterar suas configurações de propriedade e abri-las novamente mais tarde. Para eliminar completamente um objeto da memória, feche o objeto e defina a variável de objeto como *Nothing* (em Visual Basic).  
  
## <a name="connection"></a>Conexão  
 O uso do método **Close** para fechar um objeto de **conexão** também fecha todos os objetos **Recordset** ativos associados à conexão. Um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) associado ao objeto de **conexão** que você está fechando continuará, mas ele não será mais associado a um objeto de **conexão** ; ou seja, sua propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) será definida como **Nothing**. Além disso, a coleção de [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) do objeto **Command** será apagada de quaisquer parâmetros definidos pelo provedor.  
  
 Posteriormente, você pode chamar o método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) para restabelecer a conexão com a mesma fonte de dados ou outra. Enquanto o objeto de **conexão** é fechado, chamar os métodos que exigem uma conexão aberta com a fonte de dados gera um erro.  
  
 Fechar um objeto de **conexão** enquanto houver objetos Open **Recordset** na conexão reverterá todas as alterações pendentes em todos os objetos **Recordset** . Fechar explicitamente um objeto de **conexão** (chamar o método **Close** ) enquanto uma transação está em andamento gera um erro. Se um objeto de **conexão** ficar fora do escopo enquanto uma transação estiver em andamento, o ADO reverterá automaticamente a transação.  
  
## <a name="recordset-record-stream"></a>Conjunto de registros, registro, fluxo  
 O uso do método **Close** para fechar um **conjunto de registros**, um **registro**ou um objeto de **fluxo** libera os dados associados e qualquer acesso exclusivo que você tenha tido nos dados por meio desse objeto em particular. Posteriormente, você pode chamar o método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) para reabrir o objeto com os mesmos atributos, ou modificados.  
  
 Enquanto um objeto **Recordset** é fechado, chamar quaisquer métodos que exigem um cursor ao vivo gera um erro.  
  
 Se uma edição estiver em andamento enquanto estiver no modo de atualização imediata, chamar o método **Close** gerará um erro; em vez disso, chame o método [Update](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) primeiro. Se você fechar o objeto **Recordset** no modo de atualização do lote, todas as alterações desde a última chamada [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) serão perdidas.  
  
 Se você usar o método [clone](../../../ado/reference/ado-api/clone-method-ado.md) para criar cópias de um objeto Open **Recordset** , fechar o original ou um clone não afetará nenhuma das outras cópias.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
