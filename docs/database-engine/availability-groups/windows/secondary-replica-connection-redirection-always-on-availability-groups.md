---
title: Redirecionamento de conexão de leitura/gravação de réplica secundária para primária do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: article
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e64768dcfaf4342c3ea52f1b01c29940fb1c8cf0
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206302"
---
# <a name="secondary-to-primary-replica-readwrite-connection-redirection-always-on-availability-groups"></a>Redirecionamento de conexão de leitura/gravação de réplica secundária para primária (Grupos de Disponibilidade Always On)

[!INCLUDE[appliesto](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] CTP 2.0 apresenta o *redirecionamento de conexão de leitura/gravação de réplica secundária para primária* para Grupos de Disponibilidade Always On. O redirecionamento de conexão de leitura/gravação está disponível em qualquer plataforma de sistema operacional. Ele permite que conexões do aplicativo cliente sejam direcionadas para a réplica primária, independentemente do servidor de destino especificado na cadeia de conexão. 

Por exemplo, a cadeia de conexão pode ser direcionada a uma réplica secundária. Dependendo da configuração de réplica do AG (grupo de disponibilidade) e as configurações na cadeia de conexão, a conexão pode ser redirecionada automaticamente para a réplica primária. 

## <a name="use-cases"></a>Casos de uso

Antes do [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)], o ouvinte do AG e o recurso de cluster correspondente redirecionam o tráfego do usuário para a réplica primária para garantir a reconexão depois do failover. O [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] continua a ser compatível com a funcionalidade de ouvinte do AG e adiciona redirecionamento de conexão da réplica para cenários que não podem incluir um ouvinte. Por exemplo:

* A tecnologia de cluster integrada pelos grupos de disponibilidade do SQL Server não oferece uma funcionalidade semelhante a ouvinte 
* Uma configuração de várias sub-redes, como na nuvem ou em um IP flutuante de várias sub-redes com o Pacemaker em que as configurações se tornam complexas, propensas a erros e com problemas difíceis de solucionar devido aos vários componentes envolvidos
* Escala de leitura ou recuperação de desastres e o tipo do cluster é `NONE`, porque não há nenhum mecanismo simples para garantir a reconexão transparente após o failover manual

## <a name="requirement"></a>Requisito

Para que uma réplica secundária redirecione as solicitações de conexão de leitura/gravação:
* A réplica secundária precisa estar online. 
* A especificação de réplica `PRIMARY_ROLE` precisa incluir `READ_WRITE_ROUTING_URL`.
* A cadeia de conexão precisa definir `ApplicationIntent` como `ReadWrite` – que é o padrão.

## <a name="set-readwriteroutingurl-option"></a>Definir a opção READ_WRITE_ROUTING_URL

Para configurar o redirecionamento de conexão de leitura/gravação, defina `READ_WRITE_ROUTING_URL` para a réplica primária ao criar o AG. 

Em [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)], `READ_WRITE_ROUTING_URL` foi adicionado à especificação `<add_replica_option>`. Consulte os seguintes tópicos: 

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)
* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)


### <a name="primaryrolereadwriteroutingurl-not-set-default"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL) não definido (padrão) 

Por padrão, o redirecionamento de conexão de réplica de leitura/gravação não é definido para uma réplica. A forma como uma réplica secundária trata as solicitações de conexão depende se a réplica secundária está definida para permitir conexões ou não e a configuração de `ApplicationIntent` na cadeia de conexão. A tabela a seguir mostra como uma réplica secundária lida com conexões com base em `SECONDARY_ROLE (ALLOW CONNECTIONS = )` e `ApplicationIntent`.

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/> Padrão|Conexões com falha|Conexões com falha|Conexões bem-sucedidas<br/>Leituras bem-sucedidas<br/>Gravações com falha|
|`ApplicationIntent=ReadOnly`|Conexões com falha|Conexões bem-sucedidas|Conexões bem-sucedidas

A tabela anterior mostra o comportamento padrão, que é o mesmo que as versões do SQL Server antes de [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)]. 

### <a name="primaryrolereadwriteroutingurl-set"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL) definido 

Depois de definir o redirecionamento de conexão de leitura/gravação, a maneira como a réplica trata as solicitações de conexão se comporta de forma diferente. O comportamento de conexão ainda depende da configuração de `SECONDARY_ROLE (ALLOW CONNECTIONS = )` e `ApplicationIntent`. A tabela a seguir mostra como uma réplica secundária com `READ_WRITE_ROUTING` definido lida com conexões com base em `SECONDARY_ROLE (ALLOW CONNECTIONS = )` e `ApplicationIntent`.

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/>Padrão|Conexões com falha|Conexões com falha|Rotas de conexões para a primária|
|`ApplicationIntent=ReadOnly`|Conexões com falha|Conexões bem-sucedidas|Conexões bem-sucedidas

A tabela anterior mostra que, quando a réplica primária tem `READ_WRITE_ROUTING_URL` definido, a réplica secundária redirecionará as conexões para a réplica primária quando `SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)` e a conexão especificar `ReadWrite`.

## <a name="example"></a>Exemplo 

Neste exemplo, um grupo de disponibilidade tem três réplicas:
* Uma réplica primária em COMPUTER01
* Uma réplica secundária síncrona em COMPUTER02
* Uma réplica secundária síncrona em COMPUTER03

A imagem a seguir representa o grupo de disponibilidade.

![Grupo de disponibilidade original](media/replica-connection-redirection-always-on-availability-groups/01_originalAG.png)

O script transact-SQL a seguir cria este AG. Neste exemplo, cada réplica especifica o `READ_WRITE_ROUTING_URL`.
```sql
CREATE AVAILABILITY GROUP MyAg   
     WITH ( CLUSTER_TYPE =  NONE )  
   FOR   
     DATABASE  <Database1>   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER02, COMPUTER03),
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL, 
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER03),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER02),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' )  
         SESSION_TIMEOUT = 10  
         );
GO  
```
   - `<domain>.<tld>`
      - Domínio e o domínio de nível superior do nome de domínio totalmente qualificado. Por exemplo, `corporation.com`.


### <a name="connection-behaviors"></a>Comportamentos de conexão

No diagrama a seguir, um aplicativo cliente se conecta ao COMPUTER02 com `ApplicationIntent=ReadWrite`. A conexão é redirecionada para a réplica primária. 

![Grupo de disponibilidade original](media/replica-connection-redirection-always-on-availability-groups/02_redirectionAG.png)

A réplica secundária redireciona chamadas de leitura/gravação para a réplica primária. Uma conexão de leitura e gravação para qualquer uma das réplicas será redirecionada para a réplica primária. 

No diagrama a seguir, a réplica primária passou por failover manual para COMPUTER02. Um aplicativo cliente se conecta ao COMPUTER01 com `ApplicationIntent=ReadWrite`. A conexão é redirecionada para a réplica primária. 

![Grupo de disponibilidade original](media/replica-connection-redirection-always-on-availability-groups/03_redirectionAG.png)


## <a name="sql-server-instance-offline"></a>Instância do SQL Server offline

Se a instância do SQL Server especificada na cadeia de conexão não estiver disponível (devido a interrupção), a conexão falhará independentemente da função que a réplica desempenha no servidor de destino. Para evitar um tempo de inatividade prolongado no aplicativo, configure um `FailoverPartner` alternativo na cadeia de conexão. O aplicativo precisa implementar a lógica de repetição para acomodar as réplicas primária e secundária que não ficam online durante o failover real. Para obter informações sobre cadeias de conexão, consulte [Propriedade SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx).

## <a name="see-also"></a>Consulte Também

[Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 
[Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   

[Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md) 
