---
title: ALTER ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 27d08ae64d0387f60963358bbdbb04471d9ffb05
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453550"
---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Modifica informações de rota para uma rota existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 


[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)] 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *route_name*  
 É o nome da rota a ser alterada. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 com  
 Introduz as cláusulas que definem a rota a ser alterada.  
  
 SERVICE_NAME **='***service_name***'**  
 Especifica o nome do serviço remoto ao qual essa rota aponta. O *service_name* precisa corresponder exatamente ao nome que o serviço remoto usa. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa uma comparação byte a byte para corresponder ao *service_name*. Em outras palavras, a comparação diferencia maiúsculas de minúsculas e não considera o agrupamento atual. Uma rota com o nome de serviço **'SQL/ServiceBroker/BrokerConfiguration'** é uma rota para um serviço Broker Configuration Notice. Uma rota para esse serviço pode não especificar uma instância do agente.  
  
 Se a cláusula SERVICE_NAME for omitida, o nome de serviço para a rota permanecerá inalterado.  
  
 BROKER_INSTANCE **='***broker_instance***'**  
 Especifica o banco de dados que hospeda o serviço de destino. O parâmetro *broker_instance* precisa ser o identificador da instância do agente para o banco de dados remoto, que pode ser obtido ao executar a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 Quando a cláusula BROKER_INSTANCE é omitida, a instância do agente para a rota permanece inalterada.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 LIFETIME **=***route_lifetime*  
 Especifica a hora, em segundos, que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retém a rota na tabela de roteamento. No fim do tempo de vida, a rota expira e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não a considera mais ao escolher uma rota para uma nova conversa. Se essa cláusula for omitida, o tempo de vida da rota permanecerá inalterado.  
  
 ADDRESS **='***next_hop_address'*  

 Para a Instância Gerenciada do Banco de Dados SQL, `ADDRESS` deve ser local.

 Especifica o endereço de rede para essa rota. O *next_hop_address* especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP://** { *dns_name* | *netbios_name* |*ip_address* } **:** *port_number*  
  
 O *port_number* especificado precisa corresponder ao número da porta do ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando uma rota especifica **'LOCAL'** para o *next_hop_address*, a mensagem é entregue a um serviço na instância atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no endereço de rede no nome do serviço. Uma rota que especifica **'TRANSPORT'** pode especificar um nome de serviço ou uma instância do agente.  
  
 Quando o *next_hop_address* for o servidor principal para um espelho de banco de dados, você também deverá especificar o MIRROR_ADDRESS para o servidor espelho. Caso contrário, essa rota não fará failover automaticamente no servidor espelho.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 Especifica o endereço de rede para o servidor espelho de um par espelhado cujo servidor principal está no *next_hop_address*. O *next_hop_mirror_address* especifica um endereço TCP/IP no seguinte formato:  
  
 **TCP://**{ *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 O *port_number* especificado precisa corresponder ao número da porta do ponto de extremidade do [!INCLUDE[ssSB](../../includes/sssb-md.md)] de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. Isso pode ser obtido executando a seguinte consulta no banco de dados selecionado:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Quando MIRROR_ADDRESS é especificado, a rota deve especificar as cláusulas SERVICE_NAME e BROKER_INSTANCE. Uma rota que especifica **'LOCAL'** ou **'TRANSPORT'** para o *next_hop_address* pode não especificar um endereço espelho.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
## <a name="remarks"></a>Remarks  
 A tabela de roteamento que armazena as rotas é uma tabela de metadados que pode ser lida por meio da exibição de catálogo **sys.routes**. A tabela de roteamento pode ser atualizada somente pelas instruções CREATE ROUTE, ALTER ROUTE e DROP ROUTE.  
  
 As cláusulas que não são especificadas no comando ALTER ROUTE permanecem inalteradas. Portanto, não é possível alterar uma rota com ALTER para especificar que ela não expira, que corresponde a qualquer nome de serviço ou qualquer instância do agente. Para alterar essas características de uma rota, é necessário descartar a rota existente e criar uma nova com as novas informações.  
  
 Quando uma rota especifica **'TRANSPORT'** para o *next_hop_address*, o endereço de rede é determinado com base no nome do serviço. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode processar com êxito nomes de serviço que começam com um endereço de rede em um formato válido para um *next_hop_address*. Serviços com nomes que contêm endereços de rede válidos serão roteados para o endereço de rede no nome de serviço.  
  
 A tabela de roteamento pode conter qualquer quantidade de rotas que especifiquem o mesmo serviço, endereço de rede e/ou identificador de instância do agente. Nesse caso, o [!INCLUDE[ssSB](../../includes/sssb-md.md)] escolhe uma rota usando um procedimento criado para encontrar a correspondência mais exata entre as informações especificadas na conversa e as informações da tabela de roteamento.  
  
 Para alterar a AUTHORIZATION para um serviço, use a instrução ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissões  
 A permissão para alterar uma rota assume como padrão o proprietário dessa rota, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-service-for-a-route"></a>A. Alterando o serviço para uma rota  
 O exemplo a seguir modifica a rota `ExpenseRoute` para apontar para o serviço remoto `//Adventure-Works.com/Expenses`.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>B. Alterando o banco de dados de destino para uma rota  
 O exemplo a seguir altera o banco de dados de destino para a rota `ExpenseRoute` ao banco de dados identificado pelo identificador exclusivo `D8D4D268-00A3-4C62-8F91-634B89B1E317.`  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>C. Alterando o endereço para uma rota  
 O exemplo a seguir altera o endereço de rede para a rota `ExpenseRoute` à porta TCP `1234` no host com o endereço IP `10.2.19.72`.  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>D. Alterando o banco de dados e o endereço para uma rota  
 O exemplo a seguir altera o endereço de rede para a rota `ExpenseRoute` à porta TCP `1234` no host com o nome DNS `www.Adventure-Works.com`. Ele também altera o banco de dados de destino para o banco de dados identificado pelo identificador exclusivo `D8D4D268-00A3-4C62-8F91-634B89B1E317`.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [DROP ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
