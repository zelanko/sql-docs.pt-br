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
ms.openlocfilehash: 842a7377bcd6bdcb649a78b2f31eb66de95bc5a3
ms.sourcegitcommit: a98ed7872afc055c65aa9697d571f8b300f6eeb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313392"
---
## <a name="specifying-application-intent"></a>Especificando a intenção do aplicativo

A palavra-chave **ApplicationIntent** podem ser especificadas em sua cadeia de caracteres de conexão. Os valores atribuíveis são **ReadWrite** ou **ReadOnly**. O padrão é **ReadWrite**.

Quando **ApplicationIntent = ReadOnly**, o cliente solicita uma carga de trabalho de leitura ao se conectar. O servidor imporá a intenção em tempo de conexão e durante uma **USE** instrução de banco de dados.

O **ApplicationIntent** palavra-chave não funciona com bancos de dados somente leitura herdados.  


#### <a name="targets-of-readonly"></a>Destinos de somente leitura

Quando uma conexão escolhe **ReadOnly**, a conexão é atribuída a qualquer uma das seguintes configurações especiais que podem existir para o banco de dados:

- [Sempre ativo](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - Um banco de dados pode permitir ou impedir que cargas de trabalho de leitura no banco de dados de sempre no destino. Essa opção é controlada usando o **ALLOW_CONNECTIONS** cláusula do **PRIMARY_ROLE** e **SECONDARY_ROLE** instruções Transact-SQL.

- [Replicação geográfica](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [Expansão de leitura](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

Se nenhum desses destinos especiais estão disponíveis, o banco de dados regular é lidos no.

&nbsp;

O **ApplicationIntent** habilita a palavra-chave *roteamento somente leitura*.


## <a name="read-only-routing"></a>Roteamento somente leitura

O roteamento somente leitura é um recurso que pode garantir a disponibilidade de uma réplica somente leitura de um banco de dados. Para habilitar o roteamento somente leitura, todos os itens a seguir se aplicam:

- Você deve conectar-se a um ouvinte de grupo de disponibilidade AlwaysOn.

- A palavra-chave de cadeia de conexão **ApplicationIntent** deve ser definida como **ReadOnly**.

- O grupo de disponibilidade deve ser configurado pelo administrador de banco de dados para permitir o roteamento somente leitura.

Várias conexões usando o roteamento somente leitura pode não conectar-se à mesma réplica somente leitura. Alterações na sincronização de banco de dados ou alterações na configuração de roteamento de servidor podem resultar em conexões de cliente com réplicas somente leitura diferentes. Você pode garantir que todas as solicitações de somente leitura se conectem à mesma réplica somente leitura. Verifique se essa igualdade por *não* passando um ouvinte de grupo de disponibilidade para o **Server** palavra-chave de cadeia de caracteres de conexão. Em vez disso, especifique o nome da instância somente leitura.

Roteamento somente leitura pode demorar mais do que conectar-se à réplica primária. A espera mais é porque o roteamento somente leitura primeiro se conecta à réplica primária e, em seguida, procura a melhor secundária legível disponível. Devido a essas staps vários, você deve aumentar o tempo limite de logon para a pelo menos 30 segundos.

