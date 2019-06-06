---
title: Processamento de transações | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 032677452fa80502d37383af8172ff9475dea363
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704818"
---
# <a name="transaction-processing"></a>Processamento de transações
Um *transação* delimita o início e o final de uma série de operações de acesso de dados executado em uma conexão. Sujeita aos recursos transacionais de sua fonte de dados, o **Conexão** objeto também permite que você criar e gerenciar transações. Por exemplo, usando o Microsoft OLE DB Provider para SQL Server para acessar um banco de dados no Microsoft SQL Server, você pode criar várias transações aninhadas para os comandos que você execute.  
  
 ADO garante que alterações em uma fonte de dados resultantes de operações em uma transação ocorrem juntos com êxito ou não.  
  
 Se você cancelar a transação ou uma de suas operações falhar, o resultado será como se nenhuma das operações na transação ocorreu. A fonte de dados permanecerá como era antes do início da transação.  
  
 O ADO oferece os seguintes métodos para controlar transações: **BeginTrans**, **CommitTrans**, e **RollbackTrans**. Usar esses métodos com um **Conexão** objeto quando você deseja salvar ou cancelar uma série de alterações feitas nos dados de origem como uma única unidade. Por exemplo, para transferir dinheiro entre contas, você subtrair um valor de um e adicione a mesma quantidade às outras. Se uma das atualizações falhar, as contas não serão mais proporcionais. Fazer essas alterações dentro de uma transação aberta garante que todas ou nenhuma das alterações passem pelo.  
  
> [!NOTE]
>  Nem todos os provedores oferecem suporte a transações. Verificar se a propriedade definida pelo provedor "**transação DDL**" aparece na **Conexão** do objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção, que indica que o provedor oferece suporte transações. Se o provedor não oferece suporte a transações, chamar um desses métodos retornará um erro.  
  
 Depois de chamar o **BeginTrans** método, o provedor não precisa mais instantaneamente confirmará as alterações feitas até que você chame **CommitTrans** ou **RollbackTrans** para encerrar o transação.  
  
 Chamar o **CommitTrans** método salva as alterações feitas em uma transação aberta sobre a conexão e termina a transação. Chamar o **RollbackTrans** método reverte todas as alterações feitas em uma transação aberta e termina a transação. Qualquer um dos métodos de chamada quando não há nenhuma transação aberta gera um erro.  
  
 Dependendo os **Conexão** do objeto [atributos](../../../ado/reference/ado-api/attributes-property-ado.md) propriedade, chamar o **CommitTrans** ou **RollbackTrans** método pode Inicie automaticamente uma nova transação. Se o **atributos** estiver definida como **adXactCommitRetaining**, o provedor inicia automaticamente uma nova transação após uma **CommitTrans** chamar. Se o **atributos** estiver definida como **adXactAbortRetaining**, o provedor inicia automaticamente uma nova transação após uma **RollbackTrans** chamar.  
  
## <a name="transaction-isolation-level"></a>Nível de Isolamento de Transação  
 Use o **IsolationLevel** propriedade para definir o nível de isolamento de uma transação em um **Conexão** objeto. A configuração não terá efeito até a próxima vez que você chamar o [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) método. Se o nível de isolamento que é solicitar estiver indisponível, o provedor pode retornar o próximo nível maior de isolamento. Consulte a **IsolationLevel** propriedade na referência do programador do ADO para obter mais detalhes sobre os valores válidos.  
  
## <a name="nested-transactions"></a>Transações aninhadas  
 Para provedores que dão suporte a transações aninhadas, chamando o **BeginTrans** método dentro de uma transação aberta inicia uma nova transação aninhada. O valor de retorno indica o nível de aninhamento: um valor de retorno de "1" indica que você abriu uma transação de nível superior (ou seja, a transação não está aninhada dentro de outra transação), "2" indica que você abriu uma transação de segundo nível (a transações aninhadas dentro de uma transação de nível superior), e assim por diante. Chamando **CommitTrans** ou **RollbackTrans** afeta apenas mais recentemente abriu a transação; você deve fechar ou reverter a transação atual antes de resolver todas as transações de nível mais altos.
