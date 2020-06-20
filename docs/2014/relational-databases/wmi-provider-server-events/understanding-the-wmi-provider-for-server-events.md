---
title: Noções básicas sobre o provedor WMI para eventos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3263fb3e2ca6114f4a84d2e9df4e9189904a729b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013757"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Compreendendo o Provedor WMI para eventos do servidor
  O Provedor WMI para Eventos do Servidor permite usar o WMI para monitorar eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor funciona transformando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um objeto WMI gerenciado. Qualquer evento que possa gerar uma notificação de eventos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser aproveitado pelo WMI usando esse provedor. Além disso, como um aplicativo de gerenciamento que interage com o WMI, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode responder a esses eventos, aumentando o escopo de eventos abordados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em versões anteriores.

 Aplicativos de gerenciamento, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, podem acessar eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usem o Provedor WMI para Eventos de Servidor emitindo instruções de linguagem WQL. O WQL é um subconjunto simplificado da linguagem SQL, com algumas extensões específicas do WMI. Usando o WQL, um aplicativo recupera um tipo de evento em relação a um banco de dados específico ou objeto de banco de dados. O Provedor WMI para Eventos de Servidor converte a consulta em uma notificação de eventos, criando efetivamente uma notificação de eventos no banco de dados de destino. Para obter mais informações sobre como as notificações de eventos funcionam no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [provedor WMI para conceitos de eventos de servidor](https://technet.microsoft.com/library/ms180560.aspx). Os eventos que podem ser consultados são listados no [provedor WMI para classes e propriedades de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).

 Quando ocorre um evento que dispara a notificação de eventos para enviar uma mensagem, a mensagem vai para um serviço de destino predefinido no **msdb** chamado **SQL/Notifications/ProcessWMIEventProviderNotification/v 1.0**. O serviço coloca o evento em uma fila predefinida no **msdb** chamado **WMIEventProviderNotificationQueue**. (O serviço e a fila são criados dinamicamente pelo provedor quando ele se conecta pela primeira vez ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .) Em seguida, o provedor lê os dados de evento dessa fila e os transforma no MOF (Managed Object Format) antes de retorná-los para o aplicativo. A ilustração a seguir mostra este processo.

 ![Diagrama de fluxo do Provedor WMI para Eventos de Servidor](../../../2014/database-engine/dev-guide/media/wmi-provider-functional-spec.gif "Diagrama de fluxo do Provedor WMI para Eventos de Servidor")

 Por exemplo, considere a seguinte Consulta WQL:

```
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS
WHERE DatabaseName = 'AdventureWorks'
```

 Em resposta a essa consulta, o Provedor WMI para Eventos de Servidor cria a notificação de eventos equivalente no banco de dados de destino:

```
USE AdventureWorks ;
GO
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9
    ON DATABASE
    WITH FAN_IN
    FOR DDL_DATABASE_LEVEL_EVENTS
    TO SERVICE
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0', 
        'A7E5521A-1CA6-4741-865D-826F804E5135';
GO
```

 Neste exemplo, `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` é um identificador [!INCLUDE[tsql](../../includes/tsql-md.md)] que é composto do prefixo `SQLWEP_` e um GUID. `SQLWEP` cria um novo GUID para cada identificador. O valor `A7E5521A-1CA6-4741-865D-826F804E5135` na `TO SERVICE` cláusula é o GUID que identifica a instância do agente no banco de dados **msdb** .

 Para obter mais informações sobre como trabalhar com o WQL, consulte [usando o WQL com o provedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).

 Os aplicativos de gerenciamento direcionam o Provedor WMI para Eventos de Servidor para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando-se a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para o DLL do provedor, Sqlwep.dll, e carrega-o na memória. O provedor gerencia um namespace WMI para eventos de servidor para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o formato é: \\ \\ . \\ *root*\Microsoft\SqlServer\ServerEvents raiz \\ *instance_name*, em que *instance_name* usa como padrão o MSSQLSERVER. Para obter mais informações sobre como se conectar a um namespace WMI para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [usando o WQL com o provedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).

 A DLL do provedor, Sqlwep.dll, é carregada apenas uma vez no serviço de host WMI do sistema operacional do servidor, independentemente de quantas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão no servidor.

 Para obter um exemplo de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo de gerenciamento de agente que usa o provedor WMI para eventos de servidor, consulte [exemplo: Criando um alerta de SQL Server Agent usando o provedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms186385.aspx). Para obter um exemplo de um aplicativo de gerenciamento que usa o provedor WMI para eventos de servidor em código gerenciado, consulte [exemplo: usando o provedor de eventos WMI em código gerenciado](https://technet.microsoft.com/library/ms179315.aspx). Mais informações também estão disponíveis sobre o WMI no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK do.

## <a name="see-also"></a>Consulte Também
 [Provedor WMI para conceitos de eventos de servidor](https://technet.microsoft.com/library/ms180560.aspx)


