---
title: Transações – grupos de disponibilidade AlwaysOn e espelhamento de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad9700e9b1c86b454191e51c6a7e4ee52c393c6b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606836"
---
# <a name="transactions---availability-groups-and-database-mirroring"></a>Transações – grupos de disponibilidade e espelhamento de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve o suporte de transações distribuídas e entre bancos de dados para Grupos de Disponibilidade Always On e espelhamento de banco de dados.  

## <a name="support-for-distributed-transactions"></a>Suporte a transações distribuídas

O SQL Server 2017 dá suporte para transações distribuídas em bancos de dados em grupos de disponibilidade. Esse suporte inclui bancos de dados na mesma instância do SQL Server ou bancos de dados em instâncias diferentes do SQL Server. Não há suporte para transações distribuídas em bancos de dados configurados para o espelhamento de banco de dados.

>[!NOTE]
>O [!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] Service Pack 2 e posteriores oferecem suporte completo para transações distribuídas em grupos de disponibilidade. 
>
>Nas versões anteriores do [!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] anteriores ao Service Pack 2, não há suporte para as transações distribuídas entre bancos de dados (ou seja, transação usando bancos de dados na mesma instância do SQL Server) que envolvem um banco de dados em um grupo de disponibilidade.

Para configurar transações distribuídas em um grupo de disponibilidade, consulte [Configurar um grupo de disponibilidade para transações distribuídas](configure-availability-group-for-distributed-transactions.md).

Obtenha mais informações em:

- [Guia de Administração do DTC](https://msdn.microsoft.com/library/ms681291.aspx)
- [Guia de Desenvolvedores do DTC](https://msdn.microsoft.com/library/ms679938.aspx)
- [Referência de Programadores do DTC](https://msdn.microsoft.com/library/ms686108.aspx)

## <a name="sql-server-2016-sp1-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 SP1 e anteriores: suporte para transações entre bancos de dados na mesma instância do SQL Server  

No SQL Server 2016 SP1 e anteriores, não há suporte para transações entre bancos de dados na mesma instância do SQL Server em grupos de disponibilidade. Não será possível hospedar dois bancos de dados em uma transação entre bancos de dados na mesma instância do SQL Server se um ou ambos os bancos de dados estiverem em um grupo de disponibilidade. Essa limitação também se aplica quando esses bancos de dados fazem parte do mesmo grupo de disponibilidade.  
  
Também não há suporte para transações entre bancos de dados para espelhamento de banco de dados.  
  
##  <a name="dtcsupport"></a> SQL Server 2016 SP1 e anteriores: suporte para transações distribuídas  
Transações distribuídas são compatíveis com grupos de disponibilidade quando os bancos de dados são hospedados por diferentes instâncias do SQL Server. Ela também se aplica a transações distribuídas entre instâncias do SQL Server e outro servidor em conformidade com DTC.  
 
O DTC ou MSDTC (Coordenador de Transações Distribuídas da Microsoft) é um serviço Windows que fornece a infraestrutura de transação para sistemas distribuídos. O MSDTC permite que aplicativos clientes incluam várias fontes de dados em uma transação, que é então confirmada em todos os servidores incluídos na transação. Por exemplo, você pode usar o MSDTC para coordenar transações que abrangem vários bancos de dados em servidores diferentes.

O SQL Server 2016 introduz a capacidade de usar transações distribuídas em que um ou mais dos bancos de dados na transação estão em um Grupo de Disponibilidade. Antes do SQL Server 2016, as transações distribuídas não tinham suporte para bancos de dados em Grupos de Disponibilidade. O SQL Server 2016 pode registrar um resource manager por banco de dados. Essa nova funcionalidade é a razão pela qual as transações distribuídas podem incluir bancos de dados em Grupos de Disponibilidade.
  
 Os seguintes requisitos devem ser atendidos:  
  
-   Os grupos de disponibilidade devem estar em execução no Windows Server 2012 R2 ou posteriores. Para o Windows Server 2012 R2, é necessário instalar a atualização na KB3090973 disponível em [https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973).  
  
-   Os grupos de disponibilidade devem ser criados com o comando **CREATE AVAILABILITY GROUP** e a cláusula **WITH DTC\_SUPPORT = PER_DB**. No momento, você não pode alterar um grupo de disponibilidade existente.  

- Todas as instâncias do SQL Server que participam do Grupo de Disponibilidade devem ter o SQL Server 2016 ou posterior.
 
 ## <a name="non-support-for-distributed-transactions"></a>Sem suporte para transações distribuídas
 Casos específicos em que não há suporte para as transações distribuídas:
 
 - No SQL Server 2016 SP1 e anteriores, em que mais de um banco de dados envolvido na transação está no mesmo grupo de disponibilidade.
 
 - No SQL Server 2016 SP1 e anteriores, em que pelo menos um banco de dados está em um grupo de disponibilidade e outro banco de dados está na mesma instância do SQL Server. 
 
 - quando o grupo de disponibilidade não foi criado com as transações distribuídas habilitadas.
 
 - Espelhamento de banco de dados.
 
 > [!IMPORTANT]
 > Determine o resultado padrão apropriado de transações que o DTC é incapaz de resolver para o seu ambiente.  Para obter informações sobre como configurar o resultado padrão, consulte [Opção de configuração de servidor in-doubt xact resolution](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## <a name="example-scenario-with-database-mirroring"></a>Cenário de exemplo com espelhamento de banco de dados  
 O exemplo de espelhamento de banco de dados a seguir ilustra como uma inconsistência lógica pode ocorrer. Neste exemplo, um aplicativo usa uma transação de banco de dados cruzado para inserir duas linhas de dados: uma linha é inserida em uma tabela em um banco de dados espelho, A, e a outra linha é inserida em uma tabela em outro banco de dados, B. O banco de dados A está sendo espelhado em modo de alta segurança com failover automático. Enquanto a transação está sendo confirmada, o banco de dados A torna-se indisponível e ocorre failover automático na sessão de espelhamento para o espelho do banco de dados A.  
  
 Depois do failover, a transação entre bancos de dados pode ser confirmada com sucesso no banco de dados B, mas não no banco de dados onde ocorreu failover. Por exemplo, se o servidor principal original para o banco de dados A não tiver enviado o log de transações entre bancos de dados para o servidor de espelho antes da falha. Depois do failover, a transação não existirá no novo servidor principal. Os bancos de dados A e B se tornarão inconsistentes, porque os dados inseridos no banco de dados B permanecerão intactos, mas os dados inseridos no banco de dados A serão perdidos.  
  
 Um cenário semelhante pode acontecer ao usar uma transação MS DTC. Por exemplo, depois do failover, o novo principal contata o MS DTC. Mas o MS DTC não tem conhecimento do novo servidor principal e encerra qualquer transação que esteja "sendo preparada para confirmação”, considerada confirmada em outros bancos de dados.  
  
> [!NOTE]  
>  Não há suporte para o uso do Espelhamento de Banco de Dados com o DTC nem para o uso de grupos de disponibilidade com o DTC de maneiras não aprovadas neste artigo.  Isso não significa que os aspectos do produto não relacionados ao DTC não tenham suporte; no entanto, quaisquer problemas decorrentes do uso incorreto de transações distribuídas não são compatíveis.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  
