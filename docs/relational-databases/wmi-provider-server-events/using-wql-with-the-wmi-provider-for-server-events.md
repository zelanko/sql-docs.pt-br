---
title: Usando o WQL com o Provedor WMI para eventos de servidor
description: Saiba como os aplicativos de gerenciamento acessam SQL Server eventos usando o provedor WMI para eventos de servidor emitindo instruções linguagem WQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 076c91605c245ad49f6c51a2a656d48c7dba2109
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545148"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Usando o WQL com o Provedor WMI para eventos de servidor
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Os aplicativos de gerenciamento acessam eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o Provedor WMI para eventos de servidor emitindo instruções WQL. O WQL é um subconjunto simplificado da linguagem SQL, com algumas extensões específicas do WMI. Ao usar o WQL, um aplicativo recupera um tipo de evento em uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um banco de dados ou um objeto de banco de dados (o único objeto com suporte no momento é o de fila). O provedor WMI para eventos de servidor traduz a consulta em uma notificação de evento que é criada no banco de dados de destino para notificações de eventos no escopo do banco de dados ou no escopo do objeto, ou no banco de dados **mestre** para notificações de eventos no escopo do servidor.  
  
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
  
 O argumento na cláusula `FROM` da consulta WQL (`DDL_DATABASE_LEVEL_EVENTS`) pode ser qualquer evento válido no qual uma notificação de eventos pode ser criada. Os argumentos nas cláusulas `SELECT` e `WHERE` podem especificar qualquer propriedade de evento associada com um evento ou seu evento pai. Para obter uma lista de eventos válidos e propriedades de eventos, consulte [Event Notifications (mecanismo de banco de dados)](https://technet.microsoft.com/library/ms182602.aspx).  
  
 Há suporte explícito do Provedor WMI para eventos de servidor à sintaxe WQL a seguir. É possível especificar sintaxe WQL adicional, mas ela não é específica deste provedor e é analisada pelo serviço de host WMI. Para obter mais informações sobre a linguagem de consulta WMI, consulte a documentação do WQL no MSDN (Microsoft Developer Network).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>Argumentos  
 *event_property*  
 É uma propriedade de um evento. Os exemplos incluem a **hora**, **SPID**e **LoginName**. Pesquise cada evento listado no [provedor WMI para classes de eventos de servidor e propriedades](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) para determinar quais propriedades ele contém. Por exemplo, o evento DDL_DATABASE_LEVEL_EVENTS mantém as propriedades **DatabaseName** e **username** . Ele também herda as propriedades **SQLInstance**, **LoginName**, **TimeTime**, **SPID**e **ComputerName** de seus eventos pai.  
  
 **,** *... n*  
 Indica que *event_property* pode ser consultada várias vezes, separadas por vírgulas.  
  
 \*  
 Especifica que todas as propriedades associadas com um evento são consultadas.  
  
 *event_type*  
 É qualquer evento no qual uma notificação de eventos pode ser criada. Para obter uma lista de eventos disponíveis, consulte [provedor WMI para classes e propriedades de eventos de servidor](https://technet.microsoft.com/library/ms186449.aspx). Observe que os nomes de *tipo de evento* correspondem ao mesmo *event_type*  |  *event_group* que podem ser especificados quando você cria manualmente uma notificação de evento usando criar notificação de eventos. Os exemplos de *tipo de evento* incluem CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS e TRC_DATABASE.  
  
> [!NOTE]  
>  Certos procedimentos armazenados do sistema que executam operações similares a DDL também podem acionar notificações de eventos. Teste as notificações de eventos para determinar suas respostas aos procedimentos armazenados que são executados. Por exemplo, a instrução CREATE TYPE e **sp_addtype** procedimento armazenado acionarão uma notificação de evento que é criada em um evento CREATE_TYPE. No entanto, o procedimento armazenado **sp_rename** não aciona nenhuma notificação de evento. Para obter mais informações, consulte[eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *where_condition*  
 É um predicado de consulta de cláusula WHERE composto por nomes de *event_property* e operadores lógicos e de comparação. O *where_condition* determina o escopo no qual a notificação de evento correspondente é registrada no banco de dados de destino. Ele também pode atuar como um filtro para direcionar um esquema ou objeto específico do qual consultar *event_type.* Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 Somente o `=` operando pode ser usado junto com **DatabaseName**, **SchemaName**e **objectname**. Não é possível usar outras expressões com essas propriedades de eventos.  
  
## <a name="remarks"></a>Comentários  
 O *where_condition* da sintaxe do provedor WMI para eventos de servidor determina o seguinte:  
  
-   O escopo pelo qual o provedor tenta recuperar o *event_type*especificado: nível de servidor, nível de banco de dados ou nível de objeto (o único objeto com suporte no momento é a fila). Por fim, esse escopo determina o tipo de notificação de eventos criado no banco de dados de destino. Esse processo chamou o registro de notificação de eventos.  
  
-   O banco de dados, o esquema e o objeto, quando apropriado, no qual registrar.  
  
 O Provedor WMI para eventos de servidor usa um algoritmo ascendente, o primeiro que for válido (first fit), a fim de gerar o escopo mais restrito possível para a EVENT NOTIFICATION subjacente. O algoritmo tenta minimizar a atividade interna no servidor e o tráfego de rede entre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o processo do host WMI. O provedor examina a *event_type* especificada na cláusula From e as condições na cláusula WHERE e tenta registrar a notificação de evento subjacente com o escopo mais estreito possível. Se o provedor não puder registrar com o escopo mais restrito, ele tentará registrar com escopos sucessivamente superiores, até que um registro finalmente tenha êxito. Se o escopo mais alto (o nível de servidor) for atingido e falhar, um erro será retornado ao consumidor.  
  
 Por exemplo, se DatabaseName =**'** AdventureWorks **'** for especificado na cláusula WHERE, o provedor tentará registrar uma notificação de evento no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados. Se o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] existir e o cliente que fez a chamada tiver as permissões necessárias para criar uma notificação de eventos em [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], o registro terá êxito. Caso contrário, será feita uma tentativa de registrar a notificação de eventos no nível de servidor. O registro terá êxito se o cliente WMI tiver as permissões necessárias. Porém, neste cenário, os eventos não são retornados ao cliente até que o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tenha sido criado.  
  
 O *where_condition* também pode atuar como um filtro para limitar ainda mais a consulta a um banco de dados, esquema ou objeto específico. Por exemplo, considere a seguinte consulta WQL:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 Dependendo do resultado do processo de registro, essa consulta WQL pode ser registrada no nível de banco de dados ou de servidor. Entretanto, mesmo se registrada no nível de servidor, no final o provedor filtra quaisquer eventos `ALTER_TABLE` que não se aplicam à tabela `AdventureWorks.Sales.SalesOrderDetail`. Em outras palavras, o provedor retorna apenas as propriedades dos eventos `ALTER_TABLE` que ocorrem naquela tabela específica.  
  
 Se uma expressão composta, como `DatabaseName='AW1'` OR `DatabaseName='AW2'`, for especificada, será feita uma tentativa de registrar uma única notificação de eventos no escopo do servidor, em vez de duas notificações de eventos separadas. O registro terá êxito se o cliente que fez a chamada tiver as permissões.  
  
 Se `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` forem todos especificados na `WHERE` cláusula, será feita uma tentativa de registrar a notificação de eventos diretamente no objeto `Z` no esquema `X` . O registro terá êxito se o cliente tiver as permissões. Observe que, no momento, os eventos de nível de objeto têm suporte apenas em filas e somente para o QUEUE_ACTIVATION *event_type*.  
  
 Observe que nem todos os eventos podem ser consultados em qualquer escopo específico. Por exemplo, uma consulta WQL em um evento de rastreamento, como Lock_Deadlock, ou um grupo de eventos de rastreamento, como TRC_LOCKS, podem ser registrado apenas no nível de servidor. De forma semelhante, o evento CREATE_ENDPOINT e o grupo de eventos DDL_ENDPOINT_EVENTS também podem ser registrados apenas no nível de servidor. Para obter mais informações sobre o escopo apropriado para o registro de eventos, consulte [criando notificações de eventos](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Uma tentativa de registrar uma consulta WQL cujo *event_type* só pode ser registrado no nível do servidor sempre é feita no nível do servidor. O registro terá êxito se o cliente WMI tiver as permissões. Caso contrário, será retornado um erro ao cliente. Entretanto, em alguns casos, você ainda pode usar a cláusula WHERE como um filtro para eventos em nível de servidor com base nas propriedades que correspondem ao evento. Por exemplo, muitos eventos de rastreamento têm uma propriedade **DatabaseName** que pode ser usada na cláusula WHERE como um filtro.  
  
 As notificações de eventos no escopo do servidor são criadas no banco de dados **mestre** e podem ser consultadas quanto aos metadados usando a exibição do catálogo [Sys. server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) .  
  
 As notificações de eventos no escopo do banco de dados ou no escopo do objeto são criadas no banco de dados especificado e podem ser consultadas para obter os metadados usando a exibição do catálogo [Sys. event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) . (A exibição do catálogo deve ser prefixada com o nome do banco de dados correspondente.)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>a. Consultando eventos no escopo de servidor  
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
  
## <a name="see-also"></a>Consulte Também  
 [Provedor WMI para conceitos de eventos de servidor](https://technet.microsoft.com/library/ms180560.aspx)   
 [Notificações de eventos (Mecanismo de Banco de Dados)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
