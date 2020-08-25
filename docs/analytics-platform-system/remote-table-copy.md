---
title: Cópia da tabela remota
description: Usando a cópia de tabela remota no data warehouse paralelo do sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400486"
---
# <a name="remote-table-copy"></a>Cópia de tabela remota
Descreve como usar o recurso de cópia de tabela remota para copiar tabelas de bancos de dados SQL Server PDW para bancos de dados SQL Server SMP remotos (não dispositivos). Use a cópia da tabela remota para habilitar cenários de Hub e spoke para SQL Server PDW.  
  
## <a name="understand-remote-table-copy-for-sql-server-pdw"></a><a name="BasicsPDE"></a>Entender a cópia da tabela remota para SQL Server PDW  
A cópia de tabela remota é um recurso de SQL Server PDW que habilita cenários de Hub e spoke copiando os resultados de uma instrução SQL SELECT para uma tabela em um banco de dados SMP. A cópia da tabela remota é iniciada com a instrução [criar tabela remota como SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) .  
  
## <a name="requirements-for-using-remote-table-copy"></a><a name="BasicsPrerequisites"></a>Requisitos para usar a cópia de tabela remota  
Você pode usar a cópia de tabela remota para copiar tabelas de SQL Server PDW para um banco de dados SQL Server quando essas condições forem atendidas:  
  
-   O banco de dados de destino deve ser uma instância do Microsoft® SQL Server® que esteja em execução em um sistema de® do Microsoft Windows que possa se conectar ao dispositivo SQL Server PDW, mas que não reside em um servidor dentro do dispositivo. O SQL Server remoto pode ser conectado ao SQL Server PDW usando a rede InfiniBand ou por meio da rede Ethernet.  
  
-   Os dados a serem copiados devem ser selecionáveis usando uma única instrução [Select](../t-sql/queries/select-transact-sql.md) de SQL Server PDW válida.  
  
-   O servidor de destino deve ser um servidor que não seja de dispositivo. Os dados não podem ser copiados diretamente de um dispositivo para outro usando as instruções neste tópico.  
  
-   O servidor de destino deve estar acessível a todos os nós na rede InfiniBand do dispositivo.  
  
## <a name="configure-remote-table-copy"></a><a name="ConfigureRemote"></a>Configurar cópia de tabela remota  
Para usar a cópia de tabela remota, você precisa comprar e configurar um Windows Server, configurar SQL Server no Windows Server e configurar SQL Server PDW. Use os links a seguir para executar essas três etapas de configuração.  
  
1.  [Configurar um sistema Windows externo para receber cópias de tabela remota usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [Configurar um SQL Server SMP externo para receber cópias de tabelas remotas](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [Configurar SQL Server PDW para cópias de tabelas remotas](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="perform-a-remote-table-copy"></a><a name="PerformRemote"></a>Executar uma cópia de tabela remota  
Para executar uma cópia de tabela remota, use a instrução SQL [criar tabela remota como SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) . Os exemplos são incluídos no tópico criar tabela remota.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
