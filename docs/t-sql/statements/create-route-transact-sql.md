---
title: Criar ROTA (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7268b5c9b43505d3c66fb6573a9a41c3cd62e3a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma nova rota à tabela de roteamento para o banco de dados atual. Por mensagens de saída, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] determina o roteamento verificando a tabela de roteamento no banco de dados local. Para mensagens em conversas que se originam em outra instância, incluindo mensagens a serem encaminhadas, [!INCLUDE[ssSB](../../includes/sssb-md.md)] verifica as rotas em **msdb**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 É o nome da rota a ser criada. Uma rota nova é criada no banco de dados atual e é de propriedade do principal especificado na cláusula AUTHORIZATION. Os nomes de servidor, banco de dados e esquema não podem ser especificados. O *route_name* deve ser um válido **sysname**.  
  
 AUTORIZAÇÃO *owner_name*  
 Define o proprietário da rota para o usuário ou função de banco de dados especificados. O *owner_name* pode ser o nome de qualquer usuário ou função válida quando o usuário atual é um membro do **db_owner** função de banco de dados fixa ou **sysadmin** função de servidor fixa. Caso contrário, *owner_name* deve ser o nome do usuário atual, o nome de um usuário que o usuário atual tenha a permissão IMPERSONATE ou o nome de uma função ao qual pertence o usuário atual. Quando esta cláusula é omitida, a rota pertence ao usuário atual.  
  
 com  
 Introduz as cláusulas que definem a rota que é criada.  
  
 SERVICE_NAME = **'***service_name***'**  
 Especifica o nome do serviço remoto ao qual essa rota aponta. O *service_name* deve corresponder exatamente ao nome de serviço remoto utiliza. [!INCLUDE[ssSB](../../includes/sssb-md.md)]usa uma comparação byte por byte para corresponder a *service_name*. Em outras palavras, a comparação diferencia maiúsculas de minúsculas e não considera o agrupamento atual. Se o SERVICE_NAME for omitido, essa rota corresponderá a qualquer nome de serviço, mas terá uma prioridade menor para correspondência que uma rota que especifique um SERVICE_NAME. Uma rota com um nome de serviço de **' SQL/ServiceBroker/BrokerConfiguration'** é uma rota para um serviço Broker Configuration Notice. Uma rota para esse serviço pode não especificar uma instância do agente.  
  
 BROKER_INSTANCE = **'***broker_instance_identifier***'**  
 Especifica o banco de dados que hospeda o serviço de destino. O *broker_instance_identifier* parâmetro deve ser o identificador de instância do agente para o banco de dados remoto, o que pode ser obtido executando a consulta a seguir no banco de dados selecionado:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 Quando a cláusula BROKER_INSTANCE é omitida, essa rota corresponde a qualquer instância do agente. Uma rota que corresponde a qualquer instância do agente tem prioridade maior para correspondência do que rotas com uma instância do agente explícita quando a conversa não especifica a instância. Para conversas que especificam uma instância do agente, uma rota com uma instância do agente tem prioridade maior do que uma rota que corresponde a qualquer instância do agente.  
  
 Tempo de vida  **=**  *route_lifetime*  
 Especifica a hora, em segundos, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém a rota na tabela de roteamento. No fim do tempo de vida, a rota expira e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não a considera mais ao escolher uma rota para uma nova conversa. Se essa cláusula for omitida, o *route_lifetime* for NULL e a rota nunca expira.  
  
 ENDEREÇO **='***next_hop_address***'**  
 Especifica o endereço de rede para essa rota. O *next_hop_address* Especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *endereço_IP* } **:**  *número_da_porta*  
  
 Especificado *port_number* deve corresponder ao número de porta para o [!INCLUDE[ssSB](../../includes/sssb-md.md)] ponto de extremidade de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando o serviço é hospedado em um banco de dados espelho, é necessário também especificar o MIRROR_ADDRESS para a outra instância que hospeda um banco de dados espelho. Caso contrário, essa rota não realizará failover no espelho.  
  
 Quando uma rota especifica **'LOCAL'** para o *next_hop_address*, a mensagem é entregue a um serviço na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no endereço de rede no nome do serviço. Uma rota que especifica **'TRANSPORT'** pode não especificar uma instância do nome ou o agente de serviço.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 Especifica o endereço de rede para um banco de dados espelhado com um banco de dados espelho hospedado no *next_hop_address*. O *next_hop_mirror_address* Especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *endereço_IP* } **:**  *número_da_porta*  
  
 Especificado *port_number* deve corresponder ao número de porta para o [!INCLUDE[ssSB](../../includes/sssb-md.md)] ponto de extremidade de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando MIRROR_ADDRESS é especificado, a rota deve especificar as cláusulas SERVICE_NAME e BROKER_INSTANCE. Uma rota que especifica **'LOCAL'** ou **'TRANSPORT'** para o *next_hop_address* pode não especificar um endereço de espelho.  
  
## <a name="remarks"></a>Comentários  
 A tabela de roteamento que armazena as rotas é uma tabela de metadados que pode ser lidos por meio de **routes** exibição do catálogo. Essa exibição do catálogo pode ser atualizada somente pelas instruções CREATE ROUTE, ALTER ROUTE e DROP ROUTE.  
  
 Por padrão, a tabela de roteamento em cada banco de dados de usuário contém uma rota. Essa rota é chamada **AutoCreatedLocal**. A rota especifica **'LOCAL'** para o *next_hop_address* e corresponde a qualquer identificador de instância de nome e o agente de serviço.  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no nome do serviço. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pode processar com sucesso os nomes de serviço que começam com um endereço de rede em um formato válido para um *next_hop_address*.  
  
 A tabela de roteamento pode conter qualquer quantidade de rotas que especifiquem o mesmo serviço, endereço de rede e identificador de instância do agente. Nesse caso, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] escolhe uma rota usando um procedimento criado para encontrar a correspondência mais exata entre as informações especificadas na conversa e as informações da tabela de roteamento.  
  
 O [!INCLUDE[ssSB](../../includes/sssb-md.md)] não remove rotas expiradas da tabela de roteamento. Uma rota expirada pode se tornar ativa usando a instrução ALTER ROUTE.  
  
 Uma rota não pode ser um objeto temporário. Nomes de rotas que começam com  **#**  são permitidos, mas são objetos permanentes.  
  
## <a name="permissions"></a>Permissões  
 Permissão para criar uma rota assume como padrão membros do **db_ddladmin** ou **db_owner** funções de banco de dados fixas e **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. Criando uma rota TCP/IP com o uso de um nome DNS  
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
  
## <a name="see-also"></a>Consulte também  
 [ALTER ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [Remover ROTA &#40; Transact-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

