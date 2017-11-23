---
title: "Feche o método (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords: Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d0df46efa689fa14f178f878887722dda179a2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="close-method-ado"></a>Feche o método (ADO)
Fecha um objeto e todos os objetos dependentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Use o **fechar** método para fechar um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md), um [registro](../../../ado/reference/ado-api/record-object-ado.md), um [registros](../../../ado/reference/ado-api/recordset-object-ado.md), ou um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto para liberar os recursos do sistema associados. Fechar um objeto não o remove da memória; Você pode alterar suas configurações de propriedade e abri-lo novamente mais tarde. Para eliminar completamente um objeto de memória, feche o objeto e, em seguida, defina a variável de objeto para *nada* (no Visual Basic).  
  
## <a name="connection"></a>Conexão  
 Usando o **fechar** método para fechar um **Conexão** objeto também fecha qualquer ativo **registros** objetos associados com a conexão. Um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto associado a **Conexão** objeto que você está fechando será mantido, mas não será associado com um **Conexão** objeto; isto é, seu [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade será definida como **nada**. Além disso, o **comando** do objeto [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção será limpo de qualquer parâmetro definido pelo provedor.  
  
 Posteriormente, você pode chamar o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método para restabelecer a conexão para a mesma ou de outra fonte de dados. Enquanto o **Conexão** objeto é fechado, chamar os métodos que exigem uma conexão aberta para a fonte de dados gera um erro.  
  
 Fechar um **Conexão** objeto enquanto há abertos **Recordset** objetos de conexão reverte todas as alterações pendentes em todos o **Recordset** objetos. Fechar explicitamente um **Conexão** objeto (chamando o **fechar** método) enquanto uma transação está em andamento gera um erro. Se um **Conexão** objeto fica fora do escopo, enquanto uma transação está em andamento, ADO automaticamente reverte a transação.  
  
## <a name="recordset-record-stream"></a>Conjunto de registros, registro, fluxo  
 Usando o **fechar** método para fechar um **registros**, **registro**, ou **fluxo** objeto libera os dados associados e qualquer acesso exclusivo Você pode ter tido aos dados por meio deste objeto específico. Posteriormente, você pode chamar o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) atributos de método para reabrir o objeto com o mesmo, ou modificado,.  
  
 Enquanto um **registros** objeto é fechado, chamar os métodos que exigem um cursor dinâmico gera um erro.  
  
 Se uma edição está em andamento no modo de atualização imediata, chamando o **fechar** método gera um erro; em vez disso, chame o [atualizar](../../../ado/reference/ado-api/update-method.md) ou [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primeiro. Se você fechar o **registros** do objeto no modo de atualização em lotes, todas as alterações desde a última [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) chamada são perdidas.  
  
 Se você usar o [Clone](../../../ado/reference/ado-api/clone-method-ado.md) método para criar cópias de uma abertas **registros** do objeto, fechando o original ou um clone não afeta qualquer uma das outras cópias.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos de abertura e fechamento (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Exemplo dos métodos de abertura e fechamento (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Exemplo dos métodos de abertura e fechamento (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
