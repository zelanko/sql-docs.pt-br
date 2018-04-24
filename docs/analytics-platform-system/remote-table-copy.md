---
title: Cópia da tabela remota - Parallel Data Warehouse | Microsoft Docs
description: Usando a cópia da tabela remota em Analytics Platform System Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ed517a471368e4192ad7393a92274424d37f975
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="remote-table-copy"></a>Cópia da tabela remota
Descreve como usar o recurso de cópia da tabela remota para copiar tabelas de bancos de dados do SQL Server PDW para bancos de dados de SMP SQL Server (não appliance) remotos. Use cópia de tabela remota para possibilita cenários de hub e spoke para SQL Server PDW.  
  
## <a name="BasicsPDE"></a>Entender a cópia da tabela remota do SQL Server PDW  
Cópia da tabela remota é um recurso do SQL Server PDW que permite cenários de Hub e Spoke, copiando os resultados de uma instrução SQL SELECT em uma tabela em um banco de dados SMP. A cópia da tabela remota é iniciada com o [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrução.  
  
## <a name="BasicsPrerequisites"></a>Requisitos para usar a cópia da tabela remota  
Você pode usar tabelas de copiar para copiar a tabela remota do SQL Server PDW para um banco de dados do SQL Server quando essas condições forem atendidas:  
  
-   O banco de dados de destino deve ser uma instância do Microsoft® SQL Server® que é executado em um sistema Microsoft Windows® que pode se conectar ao dispositivo de PDW do SQL Server, mas não reside em um servidor no dispositivo. O SQL Server remoto pode estar conectado com o PDW do SQL Server usando a rede InfiniBand ou por meio de rede Ethernet.  
  
-   Os dados a serem copiados devem ser selecionáveis usando um único SQL Server PDW válido [selecione](../t-sql/queries/select-transact-sql.md) instrução.  
  
-   O servidor de destino deve ser um servidor que não seja de dispositivo. Dados não podem ser copiados diretamente de um dispositivo para outro usando as instruções neste tópico.  
  
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
  
