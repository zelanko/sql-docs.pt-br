---
title: Segurança do SQL Server Express
description: Descreve as considerações de segurança para SQL Server Express.
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452024"
---
# <a name="sql-server-express-security"></a>Segurança do SQL Server Express

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O SQL Server Express (Microsoft SQL Server Express Edition) é baseado em Microsoft SQL Server e oferece suporte à maioria dos recursos do mecanismo de banco de dados. Ele foi projetado para que recursos não essenciais e conectividade de rede estejam desativados por padrão. Isso reduz a área de superfície disponível para ataque por um usuário mal-intencionado.  
  
O SQL Server Express geralmente é instalado como uma instância nomeada. O nome padrão da instância é `SQLExpress`. Uma instância nomeada é identificada pelo nome de rede do computador mais o nome da instância que você especificar durante a instalação.  
  
## <a name="network-access"></a>Acesso de rede  
Por razões de segurança, os protocolos de rede se encontram desabilitados por padrão no SQL Server Express. Isso impede ataques de usuários externos que podem comprometer o computador que hospeda a instância do SQL Server Express. Você deve habilitar explicitamente a conectividade de rede e iniciar o serviço de SQL Server Browser para se conectar a uma instância de SQL Server Express de outro computador.  
  
Quando a conectividade de rede está habilitada, uma instância de SQL Server Express tem os mesmos requisitos de segurança que as outras edições do SQL Server.  
  
## <a name="user-instances"></a>Instâncias de usuário  
Uma instância de usuário é uma instância separada do mecanismo de banco de dados SQL Server Express que é gerada por uma instância pai do SQL Server Express. O objetivo principal de uma instância de usuário é permitir que os usuários que executam o Windows sob uma conta de usuário com privilégios mínimos tenham privilégios de administrador do sistema (`sysadmin`) na instância do SQL Server Express em seu computador local. As instâncias de usuário não são destinadas a usuários que são administradores de sistema em seus próprios computadores.  
  
Uma instância de usuário é gerada a partir de uma instância primária do SQL Server ou SQL Server Express em nome de um usuário. Ele é executado como um processo de usuário no contexto de segurança do Windows do usuário, não como um serviço. Os logons do SQL Server não são permitidos; somente logons do Windows têm suporte. Isso impede que o software em execução em uma instância de usuário faça alterações em todo o sistema que o usuário não teria permissões para fazer. Uma instância de usuário também é conhecida como uma instância filho ou de cliente e, às vezes, é referenciada usando o acrônimo RANU ("executar como usuário normal").  
  
Cada instância de usuário é isolada de sua instância pai e de outras instâncias de usuário em execução no mesmo computador. Os bancos de dados instalados em instâncias de usuário são abertos somente no modo de usuário único; vários usuários não podem se conectar a eles. Replicação, consultas distribuídas e conexões remotas são desabilitadas para instâncias de usuário. Quando conectado a uma instância de usuário, os usuários não têm nenhum privilégio especial na instância de SQL Server Express pai.  
  
## <a name="external-resources"></a>Recursos externos  
Para obter mais informações sobre SQL Server Express, consulte os recursos a seguir.  
  
|||  
|-|-|  
|[Manuais online do Microsoft SQL Server 2005 Express Edition](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|Conclua a documentação para SQL Server 2005 Express Edition.|  
|[Instância de usuário para não administradores](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100)) nos Manuais Online do SQL Server|Descreve como criar e implantar instâncias de usuário.|  
|[Instâncias de usuário do SQL Server Express](sql-server-express-user-instances.md)|Descreve os recursos de instância de usuário em um aplicativo ADO.NET. Fornece informações sobre como habilitar uma instância de usuário, conectar-se a uma instância de usuário usando um <xref:Microsoft.Data.SqlClient.SqlConnection>, tempo de vida da instância do usuário e cenários de instância do usuário.|  
  
## <a name="next-steps"></a>Próximas etapas
- [Segurança do SQL Server](sql-server-security.md)
- [Instâncias de usuário do SQL Server Express](sql-server-express-user-instances.md)
