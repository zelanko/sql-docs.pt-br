---
title: Cópia de tabela remota - Parallel Data Warehouse | Microsoft Docs
description: Usando a cópia de tabela remota no Analytics Platform System Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 28bd5deda25650d36467281ccbffa7b666f4c695
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960200"
---
# <a name="remote-table-copy"></a>Cópia de tabela remota
Descreve como usar o recurso de cópia de tabela remota para copiar tabelas de bancos de dados do SQL Server PDW para bancos de dados do SQL Server do SMP (não seja de dispositivo) remotos. Use cópia de tabela remota para possibilita cenários de hub e spoke para SQL Server PDW.  
  
## <a name="BasicsPDE"></a>Entender a cópia de tabela remota para o SQL Server PDW  
Cópia de tabela remota é um recurso do SQL Server PDW que habilita cenários de Hub e Spoke, copiando os resultados de uma instrução SQL SELECT para uma tabela em um banco de dados SMP. A cópia de tabela remota é iniciada com o [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrução.  
  
## <a name="BasicsPrerequisites"></a>Requisitos para usar a cópia de tabela remota  
Você pode usar tabelas de copiar para copiar a tabela remota do SQL Server PDW para um banco de dados do SQL Server quando essas condições forem atendidas:  
  
-   O banco de dados de destino deve ser uma instância do Microsoft® SQL Server® que está em execução em um sistema Microsoft Windows® que pode se conectar ao dispositivo de PDW do SQL Server, mas não reside em um servidor em que o dispositivo. O SQL Server remoto pode ser conectado para o SQL Server PDW usando a rede InfiniBand ou por meio da rede Ethernet.  
  
-   Os dados a serem copiados devem ser selecionáveis usando um único válido do SQL Server PDW [selecionar](../t-sql/queries/select-transact-sql.md) instrução.  
  
-   O servidor de destino deve ser um servidor que não seja de dispositivo. Dados não podem ser copiados diretamente de um dispositivo para outro usando as instruções neste tópico.  
  
-   O servidor de destino deve ser acessível a todos os nós na rede do Infiniband do equipamento.  
  
## <a name="ConfigureRemote"></a>Configurar a cópia de tabela remota  
Para usar a cópia de tabela remota, você precisa para adquirir e configurar um servidor Windows, configurar o SQL Server no servidor do Windows e configurar o SQL Server PDW. Use os links a seguir para executar essas três etapas de configuração.  
  
1.  [Configurar um sistema Windows externo para receber cópias da tabela remota usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurar um servidor SQL do SMP externo para receber cópias da tabela remota](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurar o SQL Server PDW para cópias da tabela remota](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>Executar uma cópia da tabela remota  
Para executar uma cópia da tabela remota, use o [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) instrução SQL. Exemplos estão incluídos com o tópico CREATE REMOTE TABLE.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
