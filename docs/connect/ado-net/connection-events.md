---
title: Eventos de conexão
description: Os eventos de conexão recuperam mensagens informativas de uma fonte de dados e determinam se o estado delas foi alterado.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e81c541055305c056e8e90174b46bf8e4df4b34b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126340"
---
# <a name="connection-events"></a>Eventos de conexão

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O Provedor de Dados do Microsoft SqlClient para SQL Server tem objetos **Connection** com dois eventos que você pode usar para recuperar mensagens informativas de uma fonte de dados ou para determinar se o estado de **Connection** foi alterado. A tabela a seguir descreve os eventos do objeto **Connection**.

|Evento|Descrição|  
|-----------|-----------------|  
|**InfoMessage**|Ocorre quando uma mensagem informativa é retornada de uma fonte de dados. As mensagens informativas são as mensagens de uma fonte de dados que não resultam em uma exceção sendo lançada.|  
|**StateChange**|Ocorre quando o estado de **Connection** é alterado.|  

## <a name="working-with-the-infomessage-event"></a>Trabalhando com o evento InfoMessage

Você pode recuperar avisos e mensagens informativas de uma fonte de dados do SQL Server usando o evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. Os erros retornados da fonte de dados com um nível de severidade de 11 a 16 geram uma exceção. No entanto, o evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> pode ser usado para obter as mensagens da fonte de dados que não estão associadas a um erro. No caso do Microsoft SQL Server, qualquer erro com uma severidade de 10 ou menos é considerado uma mensagem informativa e podem ser capturado usando o evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage>. Para saber mais, leia o artigo [Severidade dos erros do Mecanismo de Banco de Dados](/sql/relational-databases/errors-events/database-engine-error-severities).

O evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> recebe um objeto <xref:Microsoft.Data.SqlClient.SqlInfoMessageEventArgs> que contém, em sua propriedade **Errors**, uma coleção das mensagens da fonte de dados. Você pode consultar os objetos **Error** nessa coleção para ver o número do erro e o texto da mensagem, assim como a origem do erro. O Provedor de Dados do Microsoft SqlClient para SQL Server também inclui detalhes sobre o banco de dados, o procedimento armazenado e o número de linha de que a mensagem é proveniente.

### <a name="example"></a>Exemplo

O exemplo de código a seguir mostra como adicionar um manipulador de eventos para o evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage>.

[!code-csharp[SqlConnection_._InfoMessage#1](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#1)]

## <a name="handling-errors-as-infomessages"></a>Tratando erros como InfoMessages

O evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> acionará normalmente apenas para mensagens informativas e de aviso que são enviadas do servidor. No entanto, quando ocorre um erro real, a execução do método **ExecuteNonQuery** ou **ExecuteReader** que iniciou a operação do servidor é interrompida e uma exceção é gerada.

Se você quiser continuar a processar o restante das instruções em um comando independentemente de qualquer erro gerado pelo servidor, defina a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> do <xref:Microsoft.Data.SqlClient.SqlConnection> como `true`. Isso faz a conexão acionar o evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage> para erros em vez de gerar uma exceção e interromper o processamento. O aplicativo cliente pode, em seguida, manipular esse evento e responder às condições de erro.

> [!NOTE]
> Um erro com um nível de severidade de 17 ou acima disso faz o servidor parar de processar o comando e deve ser tratado como uma exceção. Nesse caso, uma exceção é gerada independentemente de como o erro é tratado no evento <xref:Microsoft.Data.SqlClient.SqlConnection.InfoMessage>.

## <a name="working-with-the-statechange-event"></a>Trabalhando com o evento StateChange

O evento **StateChange** ocorre quando o estado de um objeto **Connection** é alterado. O evento **StateChange** recebe <xref:System.Data.StateChangeEventArgs>, que permite determinar a alteração no estado de **Connection** usando as propriedades **OriginalState** e **CurrentState**. A propriedade **OriginalState** é uma enumeração <xref:System.Data.ConnectionState> que indica o estado de **Connection** antes da alteração. **CurrentState** é uma enumeração <xref:System.Data.ConnectionState> que indica o estado de **Connection** após a alteração.

O exemplo de código a seguir usa o evento **StateChange** para gravar uma mensagem para o console quando o estado de **Connection** muda.

[!code-csharp[SqlConnection_._StateChange#2](~/../sqlclient/doc/samples/SqlConnection_InfoMessage_StateChange.cs#2)]

## <a name="see-also"></a>Confira também

- [Conectando a uma Fonte de Dados](connecting-to-data-source.md)
