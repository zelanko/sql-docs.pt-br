---
title: incluir arquivo
description: incluir arquivo
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 0e7d549c2f3b02349007815019cc47647f172f73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68213530"
---
## <a name="specifying-application-intent"></a>Especificando a intenção do aplicativo

A palavra-chave **ApplicationIntent** pode ser especificada na cadeia de conexão. Os valores atribuíveis são **ReadWrite** ou **ReadOnly**. O padrão é **ReadWrite**.

Quando **ApplicationIntent=ReadOnly**, o cliente solicita uma carga de trabalho de leitura ao se conectar. O servidor impõe a intenção no momento da conexão e durante uma instrução **USE** do banco de dados.

A palavra-chave **ApplicationIntent** não funciona com bancos de dados herdados somente leitura.  


#### <a name="targets-of-readonly"></a>Destinos de ReadOnly

Quando uma conexão escolhe **ReadOnly**, ela é atribuída a qualquer uma das configurações especiais que podem existir para o banco de dados:

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - Um banco de dados pode permitir ou não cargas de trabalho de leitura no banco de dados Always On de destino. A escolha é controlada usando a cláusula **ALLOW_CONNECTIONS** das instruções Transact-SQL **PRIMARY_ROLE** e **SECONDARY_ROLE**.

- [Replicação geográfica](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [Expansão de leitura](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

Se nenhum desses destinos especiais estiver disponível, o banco de dados regular será lido.

&nbsp;

A palavra-chave **ApplicationIntent** habilita o *roteamento somente leitura*.


## <a name="read-only-routing"></a>Roteamento somente leitura

O roteamento somente leitura é um recurso que pode garantir a disponibilidade de uma réplica somente leitura de um banco de dados. Para habilitar o roteamento somente leitura, todos os itens a seguir se aplicam:

- Você deve conectar-se a um ouvinte de grupo de disponibilidade AlwaysOn.

- A palavra-chave de cadeia de conexão **ApplicationIntent** deve ser definida como **ReadOnly**.

- O grupo de disponibilidade deve ser configurado pelo administrador de banco de dados para permitir o roteamento somente leitura.

Várias conexões que usam roteamento somente leitura podem se conectar à mesma réplica somente leitura. Alterações na sincronização de banco de dados ou alterações na configuração de roteamento de servidor podem resultar em conexões de cliente com réplicas somente leitura diferentes. Garanta que todas as solicitações somente leitura se conectem à mesma réplica somente leitura. Assegure a uniformidade *não* passando um ouvinte de grupo de disponibilidade para a palavra-chave da cadeia de conexão do **Servidor**. Em vez disso, especifique o nome da instância somente leitura.

O roteamento somente leitura pode levar mais tempo do que se conectar ao principal. A espera mais longa é porque o roteamento somente leitura se conecta primeiro à instância primária e, em seguida, procura a melhor instância secundária legível disponível. Devido a essas várias etapas, é preciso aumentar o tempo limite de logon para, no mínimo, 30 segundos.

