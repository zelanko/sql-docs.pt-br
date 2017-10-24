---
title: Distributed Replay Requirements | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6fffee7d-891f-4d9d-b2c3-dd19855a1c2c
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a014a2de0f3f8540845eb703910890458bc99eca
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="distributed-replay-requirements"></a>Requisitos do Distributed Replay
  Antes de usar o recurso Distributed Replay do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , considere os requisitos de produto destacados neste tópico.  
  
## <a name="input-trace-requirements"></a>Requisitos de rastreamento de entrada  
 Para repetir dados de rastreamento com êxito, ele deve atender os requisitos de versão e formato e conter os eventos e as colunas necessárias.  
  
### <a name="input-trace-versions"></a>Versões de rastreamento de entrada  
 O Distributed Replay oferece suporte a dados de rastreamento de entrada que são coletados nas seguintes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
### <a name="input-trace-formats"></a>Formatos de rastreamento de entrada  
 Os dados de rastreamento de entrada podem estar em qualquer um dos seguintes formatos:  
  
-   Um único arquivo de rastreamento que tem a extensão `.trc` .  
  
-   Um conjunto de arquivos de rastreamento de substituição que siga a convenção de nomenclatura de substituição de arquivo, por exemplo: `<TraceFile>.trc`, `<TraceFile>_1.trc`, `<TraceFile>_2.trc`, `<TraceFile>_3.trc`... `<TraceFile>_n.trc`.  
  
### <a name="input-trace-events-and-columns"></a>Eventos e colunas de rastreamento de entrada  
 Os dados de rastreamento de entrada devem conter eventos e colunas específicos a serem reproduzidos pelo Distributed Replay. O modelo **TSQL_Replay** no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] contém todas as colunas e eventos necessários, além de informações extras. Para obter mais informações sobre esse modelo, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
> [!WARNING]  
>  Se você não usar o modelo **TSQL_Replay** para capturar os dados de rastreamento de entrada, ou se os requisitos de rastreamento de entrada não forem atendidos, talvez você receba resultados de reprodução inesperados.  
  
 Também é possível criar um modelo de rastreamento personalizado e usá-lo para reproduzir eventos com o Distributed Replay, desde que ele contenha os seguintes eventos:  
  
-   Audit Login  
  
-   Audit Logout  
  
-   ExistingConnection  
  
-   RPC Output Parameter  
  
-   RPC:Completed  
  
-   RPC:Starting  
  
-   SQL:BatchCompleted  
  
-   SQL:BatchStarting  
  
 Se você estiver repetindo cursores de servidor, os seguintes eventos também são necessários:  
  
-   CursorClose  
  
-   CursorExecute  
  
-   CursorOpen  
  
-   CursorPrepare  
  
-   CursorUnprepare  
  
 Se você estiver repetindo instruções SQL preparadas de servidor, os seguintes eventos também são necessários:  
  
-   Exec Prepared SQL  
  
-   Prepare SQL  
  
 Todos os dados de rastreamento de entrada devem conter as seguintes colunas:  
  
-   Event Class  
  
-   EventSequence  
  
-   TextData  
  
-   Nome do Aplicativo  
  
-   LoginName  
  
-   DatabaseName  
  
-   ID do banco de dados  
  
-   HostName  
  
-   Binary Data  
  
-   SPID  
  
-   Start Time  
  
-   EndTime  
  
-   IsSystem  
  
## <a name="supported-input-trace-and-target-server-combinations"></a>Rastreamento de entrada e combinações de servidor de destino com suporte  
 A tabela a seguir lista as versões com suporte dos dados de rastreamento e, para cada uma, as versões com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que os dados podem ser repetidos.  
  
|Versão de dados de rastreamento de entrada|Versões com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instância do servidor de destino|  
|---------------------------------|------------------------------------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
  
## <a name="operating-system-requirements"></a>Requisitos do sistema operacional  
 Os sistemas operacionais com suporte para a execução da ferramenta de administração e o controlador e os serviços cliente são os mesmos que sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre quais sistemas operacionais têm suporte na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 Os recursos do Distributed Replay têm suporte em sistemas operacionais x86 e x64. Para sistemas operacionais x64, somente há suporte para Windows no modo Windows (WOW).  
  
## <a name="installation-limitations"></a>Limitações de instalação  
 Qualquer computador pode ter apenas uma única instância de cada recurso do Distributed Replay instalado. A tabela a seguir lista a quantidade de instalações de cada recurso permitida em um único ambiente do Distributed Replay.  
  
|Recurso Distributed Replay|Máximo de instalações por ambiente de repetição|  
|--------------------------------|--------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|1|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|16 (computadores físicos ou virtuais)|  
|Ferramenta de administração|Ilimitado|  
  
> [!NOTE]  
>  Embora só uma instância da ferramenta de administração possa ser instalada em um único computador, você pode iniciar várias instâncias dessa ferramenta. Os comandos emitidos de várias ferramentas de administração são resolvidos na ordem em que são recebidos.  
  
## <a name="data-access-provider"></a>Provedor de dados do sistema  
 O Distributed Replay tem suporte apenas para o provedor de acesso a dados ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="target-server-preparation-requirements"></a>Requisitos de preparação do servidor de destino  
 Nós recomendamos que o servidor de destino seja localizado em um ambiente de teste. Para repetir dados de rastreamento em uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da que foi originalmente registrada, verifique se as seguintes ações foram executadas no servidor de destino:  
  
-   Todos os logons e usuários contidos nos dados de rastreamento devem estar presentes no mesmo banco de dados no servidor de destino.  
  
-   Todos os logos e usuários no servidor de destino devem ter as mesmas permissões que tinham no servidor original.  
  
-   As IDs do banco de dados no destino devem, idealmente, ser idênticas àquela na origem. No entanto, se essas permissões não forem iguais, a correspondência poderá ser executada com base no **DatabaseName** se estiver presente no rastreamento.  
  
-   O banco de dados padrão de cada logon contido nos dados de rastreamento deve estar configurado (no servidor de destino) para o respectivo banco de dados de destino do logon. Por exemplo, os dados de rastreamento a serem repetidos contêm atividade para o logon, **Pedro**, no banco de dados **Pedro_Db** na instância original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, no servidor de destino, o banco de dados padrão do logon **Pedro**deve estar configurado para o banco de dados que corresponde a **Pedro_Db** (mesmo que o nome do banco de dados seja diferente). Para configurar o banco de dados padrão do logon, use o procedimento armazenado de sistema `sp_defaultdb` .  
  
 A repetição de eventos associados com logons faltantes ou incorretos resulta em erros de repetição, mas a operação de repetição continua.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Segurança do Distributed Replay](../../tools/distributed-replay/distributed-replay-security.md)   
 [Instalar o Distributed Replay – Visão geral](../../tools/distributed-replay/install-distributed-replay-overview.md)  
  
  

