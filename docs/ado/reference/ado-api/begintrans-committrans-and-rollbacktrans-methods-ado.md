---
description: Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)
title: Métodos BeginTrans, CommitTrans e RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_RollbackTrans
- Connection15::CommitTrans
- Connection15::raw_CommitTrans
- Connection15::raw_BeginTrans
- Connection15::BeginTrans
- Connection15::RollbackTrans
helpviewer_keywords:
- BeginTrans method [ADO]
- CommitTrans method [ADO]
- RollbackTrans method [ADO]
ms.assetid: d4683472-4120-4236-8640-fa9ae289e23e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02c19026d519cf5c115dedfbe4c4dcdbf89cd37b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975927"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)
Esses métodos de transação gerenciam o processamento de transações em um objeto de [conexão](./connection-object-ado.md) da seguinte maneira:  
  
-   **BeginTrans** Inicia uma nova transação.  
  
-   **CommitTrans** Salva as alterações e encerra a transação atual. Ele também pode iniciar uma nova transação.  
  
-   **RollbackTrans** Cancela as alterações feitas durante a transação atual e encerra a transação. Ele também pode iniciar uma nova transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valor retornado  
 **BeginTrans** pode ser chamado como uma função que retorna uma variável **longa** indicando o nível de aninhamento da transação.  
  
#### <a name="parameters"></a>Parâmetros  
 *object*  
 Um objeto de **conexão** .  
  
## <a name="connection"></a>Conexão  
 Use esses métodos com um objeto de **conexão** quando desejar salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, você subtrai um valor de um e adiciona o mesmo valor ao outro. Se a atualização falhar, as contas não serão mais equilibradas. Fazer essas alterações em uma transação aberta garante que todas ou nenhuma das alterações sejam passadas.  
  
> [!NOTE]
>  Nem todos os provedores dão suporte a transações. Verifique se a propriedade definida pelo provedor "**DDL de transação**" aparece na coleção de [Propriedades](./properties-collection-ado.md) do objeto de **conexão** , indicando que o provedor oferece suporte a transações. Se o provedor não oferecer suporte a transações, chamar um desses métodos retornará um erro.  
  
 Depois de chamar o método **BeginTrans** , o provedor não confirmará mais instantaneamente as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar a transação.  
  
 Para provedores que dão suporte a transações aninhadas, chamar o método **BeginTrans** dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (uma transação aninhada em uma transação de nível superior) e assim por diante. Chamar **CommitTrans** ou **RollbackTrans** afeta apenas a transação aberta mais recentemente; Você deve fechar ou reverter a transação atual antes de poder resolver qualquer transação de nível superior.  
  
 Chamar o método **CommitTrans** salva as alterações feitas em uma transação aberta na conexão e encerra a transação. Chamar o método **RollbackTrans** reverte as alterações feitas em uma transação aberta e encerra a transação. Chamar um dos métodos quando não há uma transação aberta gera um erro.  
  
 Dependendo da propriedade de [atributos](./attributes-property-ado.md) do objeto de **conexão** , chamar os métodos **CommitTrans** ou **RollbackTrans** pode iniciar automaticamente uma nova transação. Se a propriedade **Attributes** for definida como **adXactCommitRetaining**, o provedor iniciará automaticamente uma nova transação após uma chamada de **CommitTrans** . Se a propriedade **Attributes** for definida como **adXactAbortRetaining**, o provedor iniciará automaticamente uma nova transação após uma chamada **RollbackTrans** .  
  
## <a name="remote-data-service"></a>Serviço de Dados Remotos  
 Os métodos **BeginTrans**, **CommitTrans**e **RollbackTrans** não estão disponíveis em um objeto de **conexão** do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos BeginTrans, CommitTrans e RollbackTrans (VB)](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [Exemplo dos métodos BeginTrans, CommitTrans e RollbackTrans (VC + +)](./begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Propriedade Attributes (ADO)](./attributes-property-ado.md)