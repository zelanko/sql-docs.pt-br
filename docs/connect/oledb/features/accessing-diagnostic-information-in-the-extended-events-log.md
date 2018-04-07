---
title: Acessar informações de diagnóstico no Log de eventos estendidos | Microsoft Docs
description: O rastreamento do Driver do OLE DB para SQL Server e acessar informações de diagnóstico no log de eventos estendidos
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.openlocfilehash: ea81e8bc007b9afd526901bcd60827238f5356e4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="accessing-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico nos logs de eventos estendidos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], OLE DB Driver para SQL Server e os dados de rastreamento de acesso ([rastreamento de acesso a dados](http://go.microsoft.com/fwlink/?LinkId=125805)) foram atualizados para tornar mais fácil de obter informações de diagnóstico sobre falhas de conexão do buffer de anéis de conectividade e as informações de desempenho do aplicativo do log de eventos estendidos.  
  
 Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](../../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md). 

  
> [!NOTE]  
>  Este recurso é destinado somente para finalidades de solucionar problemas e realizar diagnóstico, e pode não ser adequado para auditoria ou propósitos de segurança.  
  
## <a name="remarks"></a>Remarks  
 Para operações de conexão OLE DB Driver para SQL Server enviará um cliente ID de conexão. Se a conexão falhar, você poderá acessar o buffer de anéis de conectividade ([Solução de problemas de conectividade no SQL Server 2008 com o Buffer de Anéis de Conectividade](http://go.microsoft.com/fwlink/?LinkId=207752)) e localizar o campo **ClientConnectionID** e poderá obter informações de diagnóstico sobre a falha de conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. (Se uma conexão falhar antes de enviar o pacote anterior ao logon, uma ID conexão de cliente não será gerada.) A ID de conexão de cliente é um GUID de 16 bytes. Você também poderá localizar a ID de conexão de cliente no destino de saída dos eventos estendidos, se a ação de **client_connection_id** for adicionada a eventos em uma sessão de eventos estendida. Você pode habilitar o rastreamento de acesso a dados e executar novamente o comando de conexão e observar o campo **ClientConnectionID** no rastreamento de acesso a dados para uma operação com falha, se precisar de assistência de diagnóstico adicional.  
   
  
 OLE DB Driver para SQL Server também envia uma ID de atividade específica do thread. A ID da atividade será capturada nas sessões de eventos estendidas se as sessões forem iniciadas com a opção de TRACK_CAUSAILITY habilitada. Para problemas de desempenho com uma conexão ativa, você poderá obter a ID de atividade do rastreamento de acesso a dados do cliente (campo**ActivityID** ) e, em seguida, localizar a ID de atividade nas saídas dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não o mesmo GUID para a ID de conexão de cliente) anexado a um número de sequência de quatro bytes. O número de sequência representa a ordem de uma solicitação dentro de um thread e indica a ordenação relativa de lote e as instruções RPC para o thread. O **ActivityID** é enviado opcionalmente para instruções de lote do SQL e solicitações do RPC quando o rastreamento de acesso a dados estiver habilitado e o 18º bit na palavra de configuração de rastreamento de acesso a dados estiver ativado (ON).  
  
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
 O conteúdo do OLE DB Driver para o arquivo de controle do SQL Server (ctrl.guid) é:  
  
```  
{8B98D3F2-3CC6-0B9C-6651-9649CCE5C752}  0x630ff  0   MSDADIAG.ETW
{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}  0x630ff  0   MSOLEDBSQL.1  
```  
  
## <a name="mof-file"></a>Arquivo MOF  
 O conteúdo do OLE DB Driver para o arquivo mof de SQL Server é:  
  
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
//  MSOLEDBSQL.1  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59C-D3E8-9684-AEAC-B214EFD91B31}"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1 : EventTrace  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1"),  
 Guid("{EE7FB59D-D3E8-9684-AEAC-B214EFD91B31}"),  
 DisplayName("MSOLEDBSQL.1"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace : Bid2Etw_MSOLEDBSQL_1  
{  
};  
  
[  
 dynamic: ToInstance,  
 Description("MSOLEDBSQL.1 formatted output (A)"),  
 EventType(17),  
 EventTypeName("TextA"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextA : Bid2Etw_MSOLEDBSQL_1_Trace  
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
 Description("MSOLEDBSQL.1 formatted output (W)"),  
 EventType(18),  
 EventTypeName("TextW"),  
 locale("MS\\0x409")  
]  
class Bid2Etw_MSOLEDBSQL_1_Trace_TextW : Bid2Etw_MSOLEDBSQL_1_Trace  
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
 [Tratando erros](../../oledb/ole-db-errors/errors.md)  
  
  
