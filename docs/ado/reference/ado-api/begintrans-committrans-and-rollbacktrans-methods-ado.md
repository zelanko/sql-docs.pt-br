---
title: BeginTrans, CommitTrans e RollbackTrans métodos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c796cefc03092e944520a6517bc31c585a2dc42
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509908"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>Métodos BeginTrans, CommitTrans e RollbackTrans (ADO)
Esses métodos de transação dentro de processamento de transações de gerenciar um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) da seguinte maneira:  
  
-   **BeginTrans** inicia uma nova transação.  
  
-   **CommitTrans** salva as alterações e termina a transação atual. Ele também pode iniciar uma nova transação.  
  
-   **RollbackTrans** cancela todas as alterações feitas durante a transação atual e termina a transação. Ele também pode iniciar uma nova transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valor retornado  
 **BeginTrans** pode ser chamado como uma função que retorna um **longo** variável que indica o nível de aninhamento da transação.  
  
#### <a name="parameters"></a>Parâmetros  
 *object*  
 Um **Conexão** objeto.  
  
## <a name="connection"></a>Conexão  
 Usar esses métodos com um **Conexão** objeto quando você deseja salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, você subtrair um valor de um e adicione a mesma quantidade às outras. Se uma das atualizações falhar, as contas não serão mais proporcionais. Fazer essas alterações dentro de uma transação aberta garante que todas ou nenhuma das alterações passem pelo.  
  
> [!NOTE]
>  Nem todos os provedores oferecem suporte a transações. Verificar se a propriedade definida pelo provedor "**transação DDL**" aparece na **Conexão** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, que indica que o provedor oferece suporte transações. Se o provedor não oferece suporte a transações, chamar um desses métodos retornará um erro.  
  
 Depois de chamar o **BeginTrans** método, o provedor não precisa mais instantaneamente confirmará as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar o transação.  
  
 Para provedores que dão suporte a transações aninhadas, chamando o **BeginTrans** método dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (a transações aninhadas dentro de uma transação de nível superior), e assim por diante. Chamando **CommitTrans** ou **RollbackTrans** afeta apenas mais recentemente abriu a transação; você deve fechar ou reverter a transação atual antes de resolver todas as transações de nível mais altos.  
  
 Chamar o **CommitTrans** método salva as alterações feitas em uma transação aberta sobre a conexão e termina a transação. Chamar o **RollbackTrans** método reverte todas as alterações feitas em uma transação aberta e termina a transação. Qualquer um dos métodos de chamada quando não há nenhuma transação aberta gera um erro.  
  
 Dependendo dos **Conexão** do objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade, chamar o **CommitTrans** ou **RollbackTrans** métodos podem Inicie automaticamente uma nova transação. Se o **atributos** estiver definida como **adXactCommitRetaining**, o provedor inicia automaticamente uma nova transação após uma **CommitTrans** chamar. Se o **atributos** estiver definida como **adXactAbortRetaining**, o provedor inicia automaticamente uma nova transação após uma **RollbackTrans** chamar.  
  
## <a name="remote-data-service"></a>Serviço de dados remotos  
 O **BeginTrans**, **CommitTrans**, e **RollbackTrans** métodos não estão disponíveis em um cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [BeginTrans, CommitTrans e RollbackTrans exemplo dos métodos (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans e RollbackTrans exemplo dos métodos (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
