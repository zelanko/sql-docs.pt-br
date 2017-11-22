---
title: "Processamento de transações | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a2afb43e83ebc2ed765c04fa15f070597009457
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="transaction-processing"></a>Processamento de transações
Um *transação* delimita o início e término de uma série de operações de acesso de dados executado em uma conexão. Sujeitos aos recursos transacionais de sua fonte de dados, o **Conexão** objeto também permite criar e gerenciar transações. Por exemplo, usando o Microsoft OLE DB Provider para SQL Server para acessar um banco de dados do Microsoft SQL Server, você pode criar várias transações aninhadas para os comandos que você executar.  
  
 ADO garante que ocorrerem alterações em uma fonte de dados resultantes de operações em uma transação juntos com êxito ou não.  
  
 Se você cancelar a transação, ou se uma das suas operações falhar, o resultado será como se nenhuma das operações na transação ocorreu. A fonte de dados permanecerá como era antes da transação foi iniciada.  
  
 O ADO oferece os seguintes métodos para controlar transações: **BeginTrans**, **CommitTrans**, e **RollbackTrans**. Use esses métodos com um **Conexão** objeto quando você deseja salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, subtrair um valor de uma e adicionar o mesmo valor para o outro. Se a atualização falhar, as contas não serão mais proporcionais. Fazer essas alterações dentro de uma transação aberta garante que todas ou nenhuma alteração percorrer.  
  
> [!NOTE]
>  Nem todos os provedores oferecem suporte a transações. Verifique a propriedade definido pelo provedor "**transações DDL**" aparece no **Conexão** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, indicando que o provedor oferece suporte transações. Se o provedor não oferece suporte a transações, chamar um dos métodos a seguir retornará um erro.  
  
 Depois de chamar o **BeginTrans** método, o provedor não instantaneamente confirmará as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar o transação.  
  
 Chamando o **CommitTrans** método salva as alterações feitas em uma transação aberta sobre a conexão e termina a transação. Chamando o **RollbackTrans** método reverte todas as alterações feitas em uma transação aberta e termina a transação. O método de chamada quando não houver nenhuma transação aberta gera um erro.  
  
 Dependendo do **Conexão** do objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade, chamar o **CommitTrans** ou **RollbackTrans** método pode Inicie automaticamente uma nova transação. Se o **atributos** está definida como **adXactCommitRetaining**, o provedor automaticamente inicia uma nova transação após um **CommitTrans** chamar. Se o **atributos** está definida como **adXactAbortRetaining**, o provedor automaticamente inicia uma nova transação após um **RollbackTrans** chamar.  
  
## <a name="transaction-isolation-level"></a>Nível de isolamento da transação  
 Use o **IsolationLevel** propriedade para definir o nível de isolamento de uma transação em uma **Conexão** objeto. A configuração não terá efeito até a próxima vez que você chamar o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se o nível de isolamento que solicitar estiver disponível, o provedor pode retornar o próximo maior nível de isolamento. Consulte o **IsolationLevel** propriedade na referência do programador do ADO para obter mais detalhes sobre os valores válidos.  
  
## <a name="nested-transactions"></a>Transações aninhadas  
 Para provedores que dão suporte a transações aninhadas, chamando o **BeginTrans** método dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (uma transações aninhadas dentro de uma transação de nível superior), e assim por diante. Chamando **CommitTrans** ou **RollbackTrans** afeta apenas mais abriu recentemente a transação; você deve fechar ou reverter a transação atual antes de resolver quaisquer transações de nível superior.
