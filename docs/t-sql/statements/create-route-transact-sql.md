---
title: CREATE ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c57c5a76818eabcc956a197b52b275a289576173
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823501"
---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  Adiciona uma nova rota à tabela de roteamento para o banco de dados atual. Por mensagens de saída, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] determina o roteamento verificando a tabela de roteamento no banco de dados local. Para mensagens sobre conversas que se originam em outra instância, incluindo mensagens a serem encaminhadas, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] verifica as rotas em **msdb**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *route_name*  
 É o nome da rota a ser criada. Uma rota nova é criada no banco de dados atual e é de propriedade do principal especificado na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *route_name* deve ser um **sysname** válido.  
  
 AUTHORIZATION *owner_name*  
 Define o proprietário da rota para o usuário ou função de banco de dados especificados. O *owner_name* pode ser o nome de qualquer usuário ou função válida quando o usuário atual é um membro da função de banco de dados fixa **db_owner** ou da função de servidor fixa **sysadmin**. Caso contrário, *owner_name* deve ser o nome do usuário atual, o nome de um usuário para o qual o usuário atual tenha a permissão IMPERSONATE ou o nome de uma função à qual o usuário atual pertença. Quando esta cláusula é omitida, a rota pertence ao usuário atual.  
  
 WITH  
 Introduz as cláusulas que definem a rota que é criada.  
  
 SERVICE_NAME = **'** _service\_name_ **'**  
 Especifica o nome do serviço remoto ao qual essa rota aponta. O *service_name* precisa corresponder exatamente ao nome que o serviço remoto usa. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa uma comparação byte a byte para corresponder ao *service_name*. Em outras palavras, a comparação diferencia maiúsculas de minúsculas e não considera a ordenação atual. Se o SERVICE_NAME for omitido, essa rota corresponderá a qualquer nome de serviço, mas terá uma prioridade menor para correspondência que uma rota que especifique um SERVICE_NAME. Uma rota com o nome de serviço **'SQL/ServiceBroker/BrokerConfiguration'** é uma rota para um serviço Broker Configuration Notice. Uma rota para esse serviço pode não especificar uma instância do agente.  
  
 BROKER_INSTANCE = **'** _broker\_instance\_identifier_ **'**  
 Especifica o banco de dados que hospeda o serviço de destino. O parâmetro *broker_instance_identifier* deve ser o identificador de instância do agente para o banco de dados remoto, que pode ser obtido com a execução ad seguinte consulta no banco de dados selecionado:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 Quando a cláusula BROKER_INSTANCE é omitida, essa rota corresponde a qualquer instância do agente. Uma rota que corresponde a qualquer instância do agente tem prioridade maior para correspondência do que rotas com uma instância do agente explícita quando a conversa não especifica a instância. Para conversas que especificam uma instância do agente, uma rota com uma instância do agente tem prioridade maior do que uma rota que corresponde a qualquer instância do agente.  
  
 LIFETIME **=** _route\_lifetime_  
 Especifica a hora, em segundos, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém a rota na tabela de roteamento. No fim do tempo de vida, a rota expira e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não a considera mais ao escolher uma rota para uma nova conversa. Se essa cláusula for omitida, a *route_lifetime* será NULL e a rota nunca expirará.  
  
 ADDRESS **='** _next\_hop\_address_ **'**  
Para a Instância Gerenciada de SQL, `ADDRESS` precisa ser local. 

Especifica o endereço de rede para essa rota. O *next_hop_address* especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** _port\_number_  
  
 O *port_number* especificado precisa corresponder ao número da porta do ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando o serviço é hospedado em um banco de dados espelho, é necessário também especificar o MIRROR_ADDRESS para a outra instância que hospeda um banco de dados espelho. Caso contrário, essa rota não realizará failover no espelho.  
  
 Quando uma rota especifica **'LOCAL'** para o *next_hop_address*, a mensagem é entregue a um serviço na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no endereço de rede no nome do serviço. Uma rota que especifica **'TRANSPORT'** pode não especificar um nome de serviço ou uma instância de agente.  
  
 MIRROR_ADDRESS **='** _next\_hop\_mirror\_address_ **'**  
 Especifica o endereço de rede para um banco de dados espelhado com um banco de dados espelhado hospedado no *next_hop_address*. O *next_hop_mirror_address* especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 O *port_number* especificado precisa corresponder ao número da porta do ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando MIRROR_ADDRESS é especificado, a rota deve especificar as cláusulas SERVICE_NAME e BROKER_INSTANCE. Uma rota que especifica **'LOCAL'** ou **'TRANSPORT'** para o *next_hop_address* pode não especificar um endereço espelho.  
  
## <a name="remarks"></a>Comentários  
 A tabela de roteamento que armazena as rotas é uma tabela de metadados que pode ser lida por meio da exibição do catálogo **sys.routes**. Essa exibição do catálogo pode ser atualizada somente pelas instruções CREATE ROUTE, ALTER ROUTE e DROP ROUTE.  
  
 Por padrão, a tabela de roteamento em cada banco de dados de usuário contém uma rota. Essa rota é chamada **AutoCreatedLocal**. A rota especifica **'LOCAL'** para o *next_hop_address* e faz a correspondência de qualquer nome de serviço e o identificador de instância do agente.  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no nome do serviço. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode processar com êxito nomes de serviço que começam com um endereço de rede em um formato válido para um *next_hop_address*.  
  
 A tabela de roteamento pode conter qualquer quantidade de rotas que especifiquem o mesmo serviço, endereço de rede e identificador de instância do agente. Nesse caso, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] escolhe uma rota usando um procedimento criado para encontrar a correspondência mais exata entre as informações especificadas na conversa e as informações da tabela de roteamento.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] não remove rotas expiradas da tabela de roteamento. Uma rota expirada pode se tornar ativa usando a instrução ALTER ROUTE.  
  
 Uma rota não pode ser um objeto temporário. Nomes de rotas que começam com **#** são permitidos, mas são objetos permanentes.  
  
## <a name="permissions"></a>Permissões  
 A permissão para criar uma rota usa como padrão os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e da função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>a. Criando uma rota TCP/IP com o uso de um nome DNS  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/Expenses`. A rota especifica que as mensagens para esse serviço passam pelo TCP na porta `1234` do host identificado com o nome DNS `www.Adventure-Works.com`. O servidor de destino entrega as mensagens na chegada para a instância de corretor identificada pelo identificador exclusivo `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. Criando uma rota TCP/IP com o uso de um nome NetBIOS  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/Expenses`. A rota especifica que as mensagens para esse serviço passam pelo TCP na porta `1234` do host identificado com o nome NetBIOS `SERVER02`. Na chegada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino entrega a mensagem à instância de banco de dados identificada pelo identificador exclusivo `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. Criando uma rota TCP/IP com o uso de um endereço IP  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/Expenses`. A rota especifica que as mensagens para esse serviço passam pelo TCP na porta `1234` do host identificado com o endereço IP `192.168.10.2`. Na chegada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino entrega a mensagem à instância do agente identificada pelo identificador exclusivo `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. Criando uma rota para um agente de encaminhamento  
 O exemplo a seguir cria uma rota para o corretor de encaminhamento no servidor `dispatch.Adventure-Works.com`. Como o nome de serviço e o identificador de instância do agente não são especificados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa essa rota para serviços que não têm nenhuma outra rota definida.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. Criando uma rota para um serviço local  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/LogRequests` na mesma instância que a rota.  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. Criando uma rota com um tempo de vida especificado  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/Expenses`. O tempo de vida para a rota é de `259200` segundos, que é igual a 72 horas.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. Criando uma rota para um banco de dados espelhado  
 O exemplo a seguir cria uma rota para o serviço `//Adventure-Works.com/Expenses`. O serviço é hospedado em um banco de dados espelho. Um dos bancos de dados espelhados está localizado no endereço `services.Adventure-Works.com:1234` e o outro, no endereço `services-mirror.Adventure-Works.com:1234`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. Criando uma rota que usa o nome do serviço para roteamento  
 O exemplo a seguir cria uma rota que usa o nome de serviço para determinar o endereço de rede ao qual a mensagem será enviada. Observe que uma rota que especifica `'TRANSPORT'` como o endereço de rede tem prioridade menor de correspondência que outras rotas.  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
