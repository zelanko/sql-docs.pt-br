---
title: BeginTrans, CommitTrans e métodos RollbackTrans (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0d1f3a607ed6b39100b5de5c2d166bc428fbae7f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-ado"></a>BeginTrans, CommitTrans e métodos RollbackTrans (ADO)
Esses métodos de transação dentro de processamento de transações de gerenciar um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto da seguinte maneira:  
  
-   **BeginTrans** inicia uma nova transação.  
  
-   **CommitTrans** salva as alterações e termina a transação atual. Ele também pode iniciar uma nova transação.  
  
-   **RollbackTrans** cancela as alterações feitas durante a transação atual e termina a transação. Ele também pode iniciar uma nova transação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
level = object.BeginTrans()  
object.BeginTrans  
object.CommitTrans  
object.RollbackTrans  
```  
  
## <a name="return-value"></a>Valor de retorno  
 **BeginTrans** pode ser chamado como uma função que retorna um **longo** variável que indica o nível de aninhamento da transação.  
  
#### <a name="parameters"></a>Parâmetros  
 *objeto*  
 Um **Conexão** objeto.  
  
## <a name="connection"></a>Conexão  
 Use esses métodos com um **Conexão** objeto quando você deseja salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, subtrair um valor de uma e adicionar o mesmo valor para o outro. Se a atualização falhar, as contas não serão mais proporcionais. Fazer essas alterações dentro de uma transação aberta garante que todas ou nenhuma alteração percorrer.  
  
> [!NOTE]
>  Nem todos os provedores oferecem suporte a transações. Verifique a propriedade definido pelo provedor "**transações DDL**" aparece no **Conexão** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, indicando que o provedor oferece suporte transações. Se o provedor não oferece suporte a transações, chamar um dos métodos a seguir retornará um erro.  
  
 Depois de chamar o **BeginTrans** método, o provedor não instantaneamente confirmará as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar o transação.  
  
 Para provedores que dão suporte a transações aninhadas, chamando o **BeginTrans** método dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (uma transações aninhadas dentro de uma transação de nível superior), e assim por diante. Chamando **CommitTrans** ou **RollbackTrans** afeta apenas mais abriu recentemente a transação; você deve fechar ou reverter a transação atual antes de resolver quaisquer transações de nível superior.  
  
 Chamando o **CommitTrans** método salva as alterações feitas em uma transação aberta sobre a conexão e termina a transação. Chamando o **RollbackTrans** método reverte todas as alterações feitas em uma transação aberta e termina a transação. O método de chamada quando não houver nenhuma transação aberta gera um erro.  
  
 Dependendo do **Conexão** do objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade, chamar o **CommitTrans** ou **RollbackTrans** métodos podem Inicie automaticamente uma nova transação. Se o **atributos** está definida como **adXactCommitRetaining**, o provedor automaticamente inicia uma nova transação após um **CommitTrans** chamar. Se o **atributos** está definida como **adXactAbortRetaining**, o provedor automaticamente inicia uma nova transação após um **RollbackTrans** chamar.  
  
## <a name="remote-data-service"></a>Serviço de dados remotos  
 O **BeginTrans**, **CommitTrans**, e **RollbackTrans** métodos não estão disponíveis em um cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [BeginTrans, CommitTrans e exemplo de métodos RollbackTrans (VB)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [BeginTrans, CommitTrans e exemplo dos métodos RollbackTrans (VC + +)](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-example-vc.md)   
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
