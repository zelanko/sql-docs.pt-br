---
title: "Transações – grupos de disponibilidade AlwaysOn e espelhamento de banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc86ef8e495bacaaaebf2470306b25d38d5158e5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="transactions---availability-groups-and-database-mirroring"></a>Transações – grupos de disponibilidade e espelhamento de banco de dados
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Este tópico descreve o suporte de transações distribuídas e entre bancos de dados para Grupos de Disponibilidade do AlwaysOn e espelhamento de banco de dados.  

## <a name="support-for-distributed-transactions"></a>Suporte a transações distribuídas

O SQL Server 2017 dá suporte para transações distribuídas em bancos de dados em grupos de disponibilidade. Esse suporte inclui bancos de dados na mesma instância do SQL Server ou bancos de dados em instâncias diferentes do SQL Server. Não há suporte para transações distribuídas em bancos de dados configurados para o espelhamento de banco de dados.

>[!NOTE]
>[!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] O SQL Server 2016 incluía o suporte limitado para transações distribuídas em bancos de dados em um grupo de disponibilidade. Havia suporte para transações distribuídas usando bancos de dados em um grupo de disponibilidade, desde que nenhum outro banco de dados na transação estivesse na mesma instância do SQL Server. Para obter mais informações, consulte [Suporte do DTC no SQL Server 2016 em grupos de disponibilidade](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-gr)

Para configurar transações distribuídas em um grupo de disponibilidade, consulte [Configurar um grupo de disponibilidade para transações distribuídas](configure-availability-group-for-distributed-transactions.md).

Obtenha mais informações em:

- [Guia de Administração do DTC](http://msdn.microsoft.com/library/ms681291.aspx)
- [Guia de Desenvolvedores do DTC](http://msdn.microsoft.com/library/ms679938.aspx)
- [Referência de Programadores do DTC](http://msdn.microsoft.com/library/ms686108.aspx)

## <a name="sql-server-2016-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 e anterior: suporte para transações entre bancos de dados na mesma instância do SQL Server  

No SQL Server 2016 e anterior, não há suporte para transações entre bancos de dados na mesma instância do SQL Server em grupos de disponibilidade. Isso significa que não há dois bancos de dados em uma transação entre bancos de dados que possam ser hospedados pela mesma instância do SQL Server. Isso é verdadeiro mesmo se os bancos de dados fizerem parte do mesmo grupo de disponibilidade.  
  
Também não há suporte para transações entre bancos de dados para espelhamento de banco de dados.  
  
##  <a name="dtcsupport"></a> SQL Server 2016: Suporte para transações distribuídas  
Há suporte para transações distribuídas com grupos de disponibilidade. Isso se aplica a transações distribuídas entre bancos de dados hospedados por duas instâncias do SQL Server diferentes. Isso também se aplica a transações distribuídas entre o SQL Server e outro servidor compatível com o DTC.  
 
O DTC ou MSDTC (Coordenador de Transações Distribuídas da Microsoft) é um serviço Windows que fornece a infraestrutura de transação para sistemas distribuídos. O MSDTC permite que aplicativos clientes incluam várias fontes de dados em uma transação que é então confirmada em todos os servidores incluídos na transação. Por exemplo, você pode usar o MSDTC para coordenar transações que abrangem vários bancos de dados em servidores diferentes.

O SQL Server 2016 introduz a capacidade de usar transações distribuídas em que um ou mais dos bancos de dados na transação estão em um Grupo de Disponibilidade. Antes do SQL Server 2016, as transações distribuídas não tinham suporte para bancos de dados em Grupos de Disponibilidade. O SQL Server 2016 pode registrar um resource manager por banco de dados. Essa nova funcionalidade é a razão pela qual as transações distribuídas podem incluir bancos de dados em Grupos de Disponibilidade.
  
 Os seguintes requisitos devem ser atendidos:  
  
-   Os grupos de disponibilidade devem estar em execuçaõ no Windows Server 2016 ou Windows Server 2012 R2. Para o Windows Server 2012 R2, é necessário instalar a atualização em KB3090973 disponível em [https://support.microsoft.com/pt-br/kb/3090973](https://support.microsoft.com/en-us/kb/3090973).  
  
-   Availability groups must be created with the **CREATE AVAILABILITY GROUP** e a cláusula **WITH DTC_SUPPORT = PER_DB** . No momento, você não pode alterar um grupo de disponibilidade existente.  

- Todas as instâncias do SQL Server que farão parte do Grupo de Disponibilidade devem ter o SQL Server 2016 ou posterior.
 
 ## <a name="non-support-for-distributed-transactions"></a>Sem suporte para transações distribuídas
 Casos específicos em que não há suporte para as transações distribuídas:
 
 - No SQL Server 2016 e anterior, quando mais de um banco de dados envolvido na transação está no mesmo grupo de disponibilidade.
 
 - No SQL Server 2016 e anterior, quando pelo menos um banco de dados está em um grupo de disponibilidade e outro banco de dados está na mesma instância do SQL Server. 
 
 - quando o grupo de disponibilidade não foi criado com as transações distribuídas habilitadas.
 
 - Espelhamento de banco de dados.
 
 > [!IMPORTANT]
 > Determine o resultado padrão apropriado de transações que o DTC é incapaz de resolver para o seu ambiente.  Para obter informações sobre como configurar o resultado padrão, consulte [Opção de configuração de servidor in-doubt xact resolution](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## <a name="example-scenario-with-database-mirroring"></a>Cenário de exemplo com espelhamento de banco de dados  
 O exemplo de espelhamento de banco de dados a seguir ilustra como uma inconsistência lógica pode ocorrer. Neste exemplo, um aplicativo usa uma transação de banco de dados cruzado para inserir duas linhas de dados: uma linha é inserida em uma tabela em um banco de dados espelho, A, e a outra linha é inserida em uma tabela em outro banco de dados, B. O banco de dados A está sendo espelhado em modo de alta segurança com failover automático. Enquanto a transação está sendo confirmada, o banco de dados A torna-se indisponível e ocorre failover automático na sessão de espelhamento para o espelho do banco de dados A.  
  
 Depois do failover, a transação entre bancos de dados pode ser confirmada com sucesso no banco de dados B, mas não no banco de dados onde ocorreu failover. Isso poderá ocorrer se o servidor original principal para o banco de dados A não enviar o log de transações entre bancos de dados para o servidor de espelho antes da falha. Depois do failover, a transação não existirá no novo servidor principal. Os bancos de dados A e B se tornarão inconsistentes, porque os dados inseridos no banco de dados B permanecerão intactos, mas os dados inseridos no banco de dados A serão perdidos.  
  
 Um cenário semelhante pode acontecer no uso de uma transação MS DTC. Por exemplo, depois do failover, o novo principal contata o MS DTC. Mas o MS DTC não tem conhecimento do novo servidor principal e encerra qualquer transação que esteja "sendo preparada para confirmação”, considerada confirmada em outros bancos de dados.  
  
> [!NOTE]  
>  Não há suporte para o uso do Espelhamento de Banco de Dados com o DTC nem para o uso de grupos de disponibilidade com o DTC de maneiras não aprovadas neste tópico.  Isso não significa que os aspectos do produto não relacionados ao DTC não tenham suporte; no entanto, quaisquer problemas decorrentes do uso incorreto de transações distribuídas não terão suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  

