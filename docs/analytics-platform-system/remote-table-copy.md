---
title: "Cópia de tabela remota (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e00d948f-fede-4d41-a45d-67134770ce37
caps.latest.revision: "23"
ms.openlocfilehash: 3de6700957b48c5022c73c3d521bf6f6ed090553
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="remote-table-copy"></a>Cópia da tabela remota
Descreve como usar o recurso de cópia da tabela remota para copiar tabelas de bancos de dados do SQL Server PDW para bancos de dados de SMP SQL Server (não appliance) remotos. Use cópia de tabela remota para possibilita cenários de hub e spoke para SQL Server PDW.  
  
## <a name="BasicsPDE"></a>Entender a cópia da tabela remota do SQL Server PDW  
Cópia da tabela remota é um recurso do SQL Server PDW que permite cenários de Hub e Spoke, copiando os resultados de uma instrução SQL SELECT em uma tabela em um banco de dados SMP. A cópia da tabela remota é iniciada com o [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrução.  
  
## <a name="BasicsPrerequisites"></a>Requisitos para usar a cópia da tabela remota  
Você pode usar tabelas de copiar para copiar a tabela remota do SQL Server PDW para um banco de dados do SQL Server quando essas condições forem atendidas:  
  
-   O banco de dados de destino deve ser uma instância do Microsoft® SQL Server® que é executado em um sistema Microsoft Windows® que pode se conectar ao dispositivo de PDW do SQL Server, mas não reside em um servidor no dispositivo. O SQL Server remoto pode estar conectado com o PDW do SQL Server usando a rede InfiniBand ou por meio de rede Ethernet.  
  
-   Os dados a serem copiados devem ser selecionáveis usando um único SQL Server PDW válido [selecione](../t-sql/queries/select-transact-sql.md) instrução.  
  
-   O servidor de destino deve ser um servidor não seja de aplicação. Dados não podem ser copiados diretamente de um dispositivo para outro usando as instruções neste tópico.  
  
-   O servidor de destino deve ser acessível a todos os nós na rede de Infiniband do equipamento.  
  
## <a name="ConfigureRemote"></a>Configurar a cópia da tabela remota  
Para usar a cópia da tabela remota, você precisa adquirir e configurar um servidor Windows, configurar o SQL Server no Windows server e configurar o SQL Server PDW. Use os links a seguir para executar essas etapas de configuração de três.  
  
1.  [Configure um sistema Windows externo para receber cópias da tabela remota usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurar um servidor SQL SMP externos para receber cópias da tabela remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurar o SQL Server PDW para cópias da tabela remota](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Executar uma cópia da tabela remota  
Para executar uma cópia da tabela remota, use o [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrução SQL. Exemplos são incluídos com o tópico CREATE REMOTE TABLE.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
