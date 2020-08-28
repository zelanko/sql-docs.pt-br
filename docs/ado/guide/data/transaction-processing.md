---
description: Processamento de transações
title: Processamento de transações | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ADO]
- data updates [ADO], transaction processing
- updating data [ADO], transaction processing
- nested transactions [ADO]
ms.assetid: 74ab6706-e2dc-42cb-af77-dbc58a9cf4ce
author: rothja
ms.author: jroth
ms.openlocfilehash: bde1338e56f4685359f8d1260b36c39a24455083
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979327"
---
# <a name="transaction-processing"></a>Processamento de transações
Uma *transação* delimita o início e o fim de uma série de operações de acesso a dados executadas em uma conexão. Sujeito aos recursos transacionais de sua fonte de dados, o objeto de **conexão** também permite que você crie e gerencie transações. Por exemplo, usando o provedor de OLE DB da Microsoft para SQL Server acessar um banco de dados no Microsoft SQL Server, você pode criar várias transações aninhadas para os comandos que executar.  
  
 O ADO garante que as alterações em uma fonte de dados resultante de operações em uma transação ocorram com êxito juntos ou não.  
  
 Se você cancelar a transação ou se uma de suas operações falhar, o resultado será como se nenhuma das operações na transação tiver ocorrido. A fonte de dados permanecerá como era antes do início da transação.  
  
 O ADO fornece os seguintes métodos para controlar transações: **BeginTrans**, **CommitTrans**e **RollbackTrans**. Use esses métodos com um objeto de **conexão** quando desejar salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, você subtrai um valor de um e adiciona o mesmo valor ao outro. Se a atualização falhar, as contas não serão mais equilibradas. Fazer essas alterações em uma transação aberta garante que todas ou nenhuma das alterações sejam passadas.  
  
> [!NOTE]
>  Nem todos os provedores dão suporte a transações. Verifique se a propriedade definida pelo provedor "**DDL de transação**" aparece na coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto de **conexão** , indicando que o provedor oferece suporte a transações. Se o provedor não oferecer suporte a transações, chamar um desses métodos retornará um erro.  
  
 Depois de chamar o método **BeginTrans** , o provedor não confirmará mais instantaneamente as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar a transação.  
  
 Chamar o método **CommitTrans** salva as alterações feitas em uma transação aberta na conexão e encerra a transação. Chamar o método **RollbackTrans** reverte as alterações feitas em uma transação aberta e encerra a transação. Chamar um dos métodos quando não há uma transação aberta gera um erro.  
  
 Dependendo da propriedade de [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) do objeto de **conexão** , chamar o método **CommitTrans** ou **RollbackTrans** pode iniciar automaticamente uma nova transação. Se a propriedade **Attributes** for definida como **adXactCommitRetaining**, o provedor iniciará automaticamente uma nova transação após uma chamada de **CommitTrans** . Se a propriedade **Attributes** for definida como **adXactAbortRetaining**, o provedor iniciará automaticamente uma nova transação após uma chamada **RollbackTrans** .  
  
## <a name="transaction-isolation-level"></a>Nível de Isolamento de Transação  
 Use a propriedade **IsolationLevel** para definir o nível de isolamento de uma transação em um objeto de **conexão** . A configuração não entrará em vigor até a próxima vez que você chamar o método [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) . Se o nível de isolamento solicitado não estiver disponível, o provedor poderá retornar o próximo nível de isolamento maior. Consulte a propriedade **IsolationLevel** na referência do programador de ADO para obter mais detalhes sobre valores válidos.  
  
## <a name="nested-transactions"></a>Transações aninhadas  
 Para provedores que dão suporte a transações aninhadas, chamar o método **BeginTrans** dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (uma transação aninhada em uma transação de nível superior) e assim por diante. Chamar **CommitTrans** ou **RollbackTrans** afeta apenas a transação aberta mais recentemente; Você deve fechar ou reverter a transação atual antes de poder resolver qualquer transação de nível superior.
