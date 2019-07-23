---
title: GET_TRANSMISSION_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STATUS_TSQL
- TRANSMISSION
- TRANSMISSION_TSQL
- GET_TRANSMISSION_STATUS
- STATUS
- GET_TRANSMISSION_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], transmission status
- Service Broker errors, transmission status
- transmission status information
- status information [SQL Server], conversations
- GET_TRANSMISSION_STATUS statement
ms.assetid: 621805d5-49ed-4764-b3cb-2ae4a3bf797e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6928832c352740774aeb1711c9d064c92731585b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132061"
---
# <a name="gettransmissionstatus-transact-sql"></a>GET_TRANSMISSION_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o status da última transmissão para um lado de uma conversa.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GET_TRANSMISSION_STATUS ( conversation_handle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *conversation_id*  
 É o identificador de conversa para a conversa. Esse parâmetro é do tipo **uniqueidentifier**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 Retorna uma cadeia de caracteres que descreve o status da última tentativa de transmissão para a conversa especificada. Retorna uma cadeia de caracteres vazia se a última tentativa de transmissão tiver êxito, se nenhuma tentativa de transmissão for feita ou se *conversation_handle* não existir.  
  
 As informações retornadas por essa função são as mesmas exibidas na coluna last_transmission_error da exibição de gerenciamento sys.transmission_queue. Entretanto, essa função pode ser usada para localizar o status de transmissão para conversas que atualmente não tenham mensagens na fila de transmissão.  
  
> [!NOTE]  
>  GET_TRANSMISSION_STATUS não fornece informações para mensagens que não tenham um ponto de extremidade de conversa na instância atual. Isto é, nenhuma informação está disponível para as mensagens a serem encaminhadas.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir relata o status de transmissão para a conversa com o identificador de conversa `58ef1d2d-c405-42eb-a762-23ff320bddf0`.  
  
```  
SELECT Status =  
    GET_TRANSMISSION_STATUS('58ef1d2d-c405-42eb-a762-23ff320bddf0') ;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
 ```
 Status  
 ------------------------------- 
 The Service Broker protocol transport is disabled or not configured.
 ```  
  
 Nesse caso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é configurado para permitir que o [!INCLUDE[ssSB](../../includes/sssb-md.md)] se comunique pela rede.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
