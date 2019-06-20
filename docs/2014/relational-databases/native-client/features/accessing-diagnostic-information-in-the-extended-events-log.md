---
title: Acessando informações de diagnóstico no log de eventos estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: aaa180c2-5e1a-4534-a125-507c647186ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddb50c8993de72230e97cdde729416258272bb1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046361"
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico nos logs de eventos estendidos
  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o rastreamento do acesso a dados ([Rastreamento do Acesso a Dados](https://go.microsoft.com/fwlink/?LinkId=125805)) foram atualizados para facilitar a obtenção de informações de diagnóstico sobre falhas de conexão do buffer de anéis de conectividade e informações de desempenho de aplicativo do registro de eventos estendidos.  
  
 Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](../../../database-engine/view-event-session-data.md).  
  
> [!NOTE]  
>  Este recurso é destinado somente para finalidades de solucionar problemas e realizar diagnóstico, e pode não ser adequado para auditoria ou propósitos de segurança.  
  
## <a name="remarks"></a>Comentários  
 Para operações de conexão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client enviará uma ID conexão de cliente. Se a conexão falhar, você pode acessar o buffer de anéis de conectividade ([solução de problemas de conectividade no SQL Server 2008 com o Buffer de anéis de conectividade](https://go.microsoft.com/fwlink/?LinkId=207752)) e encontre o `ClientConnectionID` do campo e obter informações de diagnóstico o Falha na conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. (Se uma conexão falhar antes de enviar o pacote anterior ao logon, uma ID conexão de cliente não será gerada.) A ID de conexão de cliente é um GUID de 16 bytes. Você também poderá localizar a ID de conexão de cliente no destino de saída dos eventos estendidos, se a ação de `client_connection_id` for adicionada a eventos em uma sessão de eventos estendida. Você pode habilitar o rastreamento de acesso a dados e executar novamente o comando de conexão e observar o campo `ClientConnectionID` no rastreamento de acesso a dados para uma operação com falha, se precisar de assistência de diagnóstico adicional.  
  
 Se você estiver usando o ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e uma conexão for bem-sucedida, você pode obter o cliente do ID de conexão usando o `SQL_COPT_SS_CLIENT_CONNECTION_ID` do atributo com [SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client também envia uma ID de atividade específica de thread. A ID da atividade será capturada nas sessões de eventos estendidas se as sessões forem iniciadas com a opção de TRACK_CAUSAILITY habilitada. Para problemas de desempenho com uma conexão ativa, você poderá obter a ID de atividade do rastreamento de acesso a dados do cliente (campo `ActivityID`) e, em seguida, localizar a ID de atividade nas saídas dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não o mesmo GUID para a ID de conexão de cliente) anexado a um número de sequência de quatro bytes. O número de sequência representa a ordem de uma solicitação dentro de um thread e indica a ordenação relativa de lote e as instruções RPC para o thread. O `ActivityID` é enviado opcionalmente para instruções de lote do SQL e solicitações do RPC quando o rastreamento de acesso a dados estiver habilitado e o 18º bit na palavra de configuração de rastreamento de acesso a dados estiver ativado (ON).  
  
 Veja a seguir um exemplo que usa o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para iniciar uma sessão de eventos estendida que será armazenada em um buffer de anéis e gravará a ID de atividade enviada de um cliente no RPC e de operações de lote.  
  
```  
create event session MySession on server   
add event connectivity_ring_buffer_recorded,   
add event sql_statement_starting (action (client_connection_id)),   
add event sql_statement_completed (action (client_connection_id)),   
add event rpc_starting (action (client_connection_id)),   
add event rpc_completed (action (client_connection_id))  
add target ring_buffer with (track_causality=on)  
  
```  
  
## <a name="control-file"></a>Arquivo de controle  
 No [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o conteúdo do arquivo de controle do SQL Server Native Client (ctrl.guid.snac11) é:  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x00000000  0   MSDADIAG.ETW  
{2DA81B52-908E-7DB6-EF81-76856BB47C4F}  0xFFFFFFFF  0   SQLNCLI11.1  
```  
  
## <a name="mof-file"></a>Arquivo MOF  
 No [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], o conteúdo do arquivo mof do SQL Server Native Client é:  
  
```  
#pragma classflags("forceupdate")  
#pragma namespace ("\\\\.\\Root\\WMI")  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  MSDADIAG.ETW  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW"),  
 Guid("{8B98D3F3-3CC6-0B9C-6651-9649CCE5C752}"),  
 DisplayName("msdadiag"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace : Bid2Etw_MSDADIAG_ETW  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextA : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSDADIAG.ETW formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSDADIAG_ETW_Trace_TextW : Bid2Etw_MSDADIAG_ETW_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
  
/////////////////////////////////////////////////////////////////////////////  
//  
//  SQLNCLI11.1  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B52-908E-7DB6-EF81-76856BB47C4F}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1"),  
 Guid("{2DA81B53-908E-7DB6-EF81-76856BB47C4F}"),  
 DisplayName("SQLNCLI11.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace : Bid2Etw_SQLNCLI11_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextA : Bid2Etw_SQLNCLI11_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringA"),  
     extension("RString"),  
     read  
    ]  
    object msgStr;  
};  
  
[  
 dynamic: ToInstance,  
 Description("SQLNCLI11.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_SQLNCLI11_1_Trace_TextW : Bid2Etw_SQLNCLI11_1_Trace  
{  
    [  
     WmiDataId(1),  
     Description("Module ID"),  
     read  
    ]  
    uint32 ModID;  
  
    [  
     WmiDataId(2),  
     Description("Text StringW"),  
     extension("RWString"),  
     read  
    ]  
    object msgStr;  
};  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tratando de erros e mensagens](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
