---
title: Usando o WQL com o provedor WMI para eventos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 16bf7df8d4c20db8f2598259af296824df3eeade
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182076"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Usando o WQL com o Provedor WMI para eventos de servidor
  Os aplicativos de gerenciamento acessam eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o Provedor WMI para eventos de servidor emitindo instruções WQL. O WQL é um subconjunto simplificado da linguagem SQL, com algumas extensões específicas do WMI. Ao usar o WQL, um aplicativo recupera um tipo de evento em uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um banco de dados ou um objeto de banco de dados (o único objeto com suporte no momento é o de fila). O provedor WMI para eventos de servidor converte a consulta em uma notificação de eventos é criada no banco de dados destino para notificações de eventos no escopo do banco de dados ou no escopo do objeto, ou na **mestre** banco de dados para eventos no escopo do servidor notificações.  
  
 Por exemplo, considere a seguinte consulta WQL:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 A partir dessa consulta, o Provedor WMI tenta gerar o equivalente dessa notificação de eventos no servidor de destino:  
  
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
  
 O argumento na cláusula `FROM` da consulta WQL (`DDL_DATABASE_LEVEL_EVENTS`) pode ser qualquer evento válido no qual uma notificação de eventos pode ser criada. Os argumentos nas cláusulas `SELECT` e `WHERE` podem especificar qualquer propriedade de evento associada com um evento ou seu evento pai. Para obter uma lista de propriedades de evento e eventos válidos, consulte [as notificações de eventos (mecanismo de banco de dados)](http://technet.microsoft.com/library/ms182602.aspx).  
  
 Há suporte explícito do Provedor WMI para eventos de servidor à sintaxe WQL a seguir. É possível especificar sintaxe WQL adicional, mas ela não é específica deste provedor e é analisada pelo serviço de host WMI. Para obter mais informações sobre a linguagem de consulta WMI, consulte a documentação do WQL no MSDN (Microsoft Developer Network).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition  
```  
  
## <a name="arguments"></a>Argumentos  
 *event_property*  
 É uma propriedade de um evento. Exemplos incluem `PostTime`, `SPID` e `LoginName`. Procure cada evento listado na [provedor WMI para Classes de eventos do servidor e as propriedades](wmi-provider-for-server-events-classes-and-properties.md) para determinar as propriedades que ele contém. Por exemplo, o evento DDL_DATABASE_LEVEL_EVENTS contém as propriedades `DatabaseName` e `UserName`. Ele também herda as propriedades `SQLInstance`, `LoginName`, `PostTime`, `SPID` e `ComputerName` de seus eventos pai.  
  
 **,** *...n*  
 Indica que *event_property* podem ser consultados várias vezes, separadas por vírgulas.  
  
 \*  
 Especifica que todas as propriedades associadas com um evento são consultadas.  
  
 *event_type*  
 É qualquer evento no qual uma notificação de eventos pode ser criada. Para obter uma lista de eventos disponíveis, consulte [provedor WMI para Classes de eventos do servidor e as propriedades](http://technet.microsoft.com/library/ms186449.aspx). Observe que *tipo de evento* nomes correspondem ao mesmo *event_type* | *event_group* que pode ser especificado quando você cria manualmente uma notificação de eventos usando CREATE EVENT NOTIFICATION. Exemplos de *tipo de evento* incluem CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS e TRC_DATABASE.  
  
> [!NOTE]  
>  Certos procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar notificações de eventos. Teste as notificações de eventos para determinar suas respostas aos procedimentos armazenados que são executados. Por exemplo, a instrução CREATE TYPE e **sp_addtype** procedimento armazenado acionarão uma notificação de eventos é criada em um evento CREATE_TYPE. No entanto, o **sp_rename** procedimento armazenado não aciona nenhuma notificação de eventos. Para obter mais informações, consulte[eventos DDL](../triggers/ddl-events.md).  
  
 *where_condition*  
 É um predicado de consulta de cláusula WHERE composta *event_property* nomes e lógicos e operadores de comparação. O *where_condition* determina o escopo no qual a notificação de evento correspondente é registrada no banco de dados de destino. Ele também pode atuar como um filtro para atingir um determinado esquema ou objeto do qual a consulta *event_type.* Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 Somente o operando `=` pode ser usado juntamente com `DatabaseName`, `SchemaName` e `ObjectName`. Não é possível usar outras expressões com essas propriedades de eventos.  
  
## <a name="remarks"></a>Comentários  
 O *where_condition* do provedor WMI para eventos de servidor sintaxe determina o seguinte:  
  
-   O escopo pelo qual o provedor tenta recuperar especificado *event_type*: o nível de servidor, banco de dados ou nível de objeto (o único objeto atualmente com suporte é a fila). Por fim, esse escopo determina o tipo de notificação de eventos criado no banco de dados de destino. Esse processo chamou o registro de notificação de eventos.  
  
-   O banco de dados, o esquema e o objeto, quando apropriado, no qual registrar.  
  
 O Provedor WMI para eventos de servidor usa um algoritmo ascendente, o primeiro que for válido (first fit), a fim de gerar o escopo mais restrito possível para a EVENT NOTIFICATION subjacente. O algoritmo tenta minimizar a atividade interna no servidor e o tráfego de rede entre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o processo do host WMI. O provedor examina o *event_type* especificado na cláusula FROM e as condições na cláusula WHERE e tenta registrar a EVENT NOTIFICATION subjacente com o menor escopo possível. Se o provedor não puder registrar com o escopo mais restrito, ele tentará registrar com escopos sucessivamente superiores, até que um registro finalmente tenha êxito. Se o escopo mais alto (o nível de servidor) for atingido e falhar, um erro será retornado ao consumidor.  
  
 Por exemplo, se DatabaseName =**'** AdventureWorks **'** é especificado na cláusula WHERE, o provedor tentará registrar uma notificação de evento no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados. Se o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] existir e o cliente que fez a chamada tiver as permissões necessárias para criar uma notificação de eventos em [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], o registro terá êxito. Caso contrário, será feita uma tentativa de registrar a notificação de eventos no nível de servidor. O registro terá êxito se o cliente WMI tiver as permissões necessárias. Porém, neste cenário, os eventos não são retornados ao cliente até que o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tenha sido criado.  
  
 O *where_condition* também pode atuar como um filtro para limitar adicionalmente a consulta a um banco de dados específico, o esquema ou o objeto. Por exemplo, considere a seguinte consulta WQL:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 Dependendo do resultado do processo de registro, essa consulta WQL pode ser registrada no nível de banco de dados ou de servidor. Entretanto, mesmo se registrada no nível de servidor, no final o provedor filtra quaisquer eventos `ALTER_TABLE` que não se aplicam à tabela `AdventureWorks.Sales.SalesOrderDetail`. Em outras palavras, o provedor retorna apenas as propriedades dos eventos `ALTER_TABLE` que ocorrem naquela tabela específica.  
  
 Se uma expressão composta, como `DatabaseName='AW1'` OR `DatabaseName='AW2'`, for especificada, será feita uma tentativa de registrar uma única notificação de eventos no escopo do servidor, em vez de duas notificações de eventos separadas. O registro terá êxito se o cliente que fez a chamada tiver as permissões.  
  
 Se `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` forem todos especificados na `WHERE` cláusula, é feita uma tentativa de registrar a notificação de eventos diretamente no objeto `Z` no esquema `X`. O registro terá êxito se o cliente tiver as permissões. Observe que no momento, os eventos de nível de objeto têm suporte apenas em filas e somente para QUEUE_ACTIVATION *event_type*.  
  
 Observe que nem todos os eventos podem ser consultados em qualquer escopo específico. Por exemplo, uma consulta WQL em um evento de rastreamento, como Lock_Deadlock, ou um grupo de eventos de rastreamento, como TRC_LOCKS, podem ser registrado apenas no nível de servidor. De forma semelhante, o evento CREATE_ENDPOINT e o grupo de eventos DDL_ENDPOINT_EVENTS também podem ser registrados apenas no nível de servidor. Para obter mais informações sobre o escopo apropriado para o registro de eventos, consulte [Criando notificações de eventos](http://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Uma tentativa de registrar um WQL consulta cuja *event_type* só pode ser registrado no servidor de nível sempre é feito no nível do servidor. O registro terá êxito se o cliente WMI tiver as permissões. Caso contrário, será retornado um erro ao cliente. Entretanto, em alguns casos, você ainda pode usar a cláusula WHERE como um filtro para eventos em nível de servidor com base nas propriedades que correspondem ao evento. Por exemplo, vários eventos de rastreamento têm uma propriedade `DatabaseName` que pode ser usada na cláusula WHERE como um filtro.  
  
 Notificações de eventos no escopo do servidor são criadas na **mestre** do banco de dados e pode ser consultada por metadados, usando o [server_event_notifications](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql) exibição do catálogo.  
  
 No escopo do banco de dados ou notificações de eventos no escopo do objeto são criadas no banco de dados especificado e podem ser consultadas por metadados, usando o [event_notifications](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql) exibição do catálogo. (A exibição do catálogo deve ser prefixada com o nome do banco de dados correspondente.)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. Consultando eventos no escopo de servidor  
 A consulta WQL a seguir recupera todas as propriedades de evento de qualquer evento de rastreamento `SERVER_MEMORY_CHANGE` que ocorre na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. Consultando eventos no escopo de banco de dados  
 A consulta WQL a seguir recupera propriedades de evento específicas de qualquer evento que ocorre no banco de dados `AdventureWorks` e existe que existe no grupo de eventos `DDL_DATABASE_LEVEL_EVENTS`.  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. Consultando eventos no escopo de banco de dados, filtrando por esquema e objeto  
 A consulta a seguir recupera todas as propriedades de evento de qualquer evento `ALTER_TABLE` que ocorre na tabela `AdventureWorks.Sales.SalesOrderDetail`.  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>Consulte também  
 [Provedor WMI para conceitos de eventos do servidor](http://technet.microsoft.com/library/ms180560.aspx)   
 [Notificações de eventos (mecanismo de banco de dados)](http://technet.microsoft.com/library/ms182602.aspx)  
  
  
