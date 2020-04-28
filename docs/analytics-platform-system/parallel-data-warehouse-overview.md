---
title: Componentes data warehouse paralelos
description: Este artigo explica o software de dispositivo e os componentes de software que não são de dispositivo do Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400928"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>Componentes data warehouse paralelos – Analytics Platform System
Este artigo explica o software do dispositivo e os componentes de software que não são de dispositivo do Analytics Platform System.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software data warehouse paralelo](media/parallel-data-warehouse-software.png "Software data warehouse paralelo")  
  
## <a name="appliance-software---query-processing-and-user-data-storage"></a><a name="sec1"></a>Software de dispositivo – processamento de consultas e armazenamento de dados do usuário  
  
### <a name="control-node"></a>Nó de Controle  
Mecanismo MPP  
O mecanismo MPP é o cérebro do sistema MPP (processamento paralelo maciço). Ele faz o seguinte:  
  
-   Cria planos de consulta paralelos e coordena a execução de consulta paralela nos nós de computação.  
  
-   Armazena e coordena metadados e dados de configuração para todos os bancos de dado.  
  
-   Gerencia SQL Server PDW autenticação e autorização do banco de dados.  
  
-   Rastreia o status de hardware e software.  
  
### <a name="data-movement-service-dms"></a>Serviço de movimentação de dados (DMS)  
O serviço de movimentação de dados (DMS) faz parte do "segredo ingrediente" do PDW. Ele faz o seguinte:  
  
-   Transfere dados de e para os nós de SQL Server PDW.  
  
-   Processa operações de consulta que exigem a transferência de dados entre os nós.  
  
-   Melhora o desempenho da consulta otimizando as velocidades de transferência de dados.  
  
### <a name="admin-console"></a>Console de administração  
O console de administração é um aplicativo Web que apresenta as informações de estado, integridade e desempenho do dispositivo.  
  
### <a name="configuration-manager"></a>Configuration Manager  
O Configuration Manager (dwconfig. exe), é a ferramenta que os administradores de dispositivo usam para configurar o sistema de plataforma de análise.  
  
### <a name="control-node-databases"></a>Bancos de dados do nó de controle  
SQL Server gerencia todos os bancos de dados no nó de controle.  
  
-   O banco de dados do Shell gerencia os metadados de todos os bancos de dados de usuário distribuído.  
  
-   TempDB contém os metadados para todas as tabelas temporárias do usuário em todo o dispositivo.  
  
-   Mestre é a tabela mestra para SQL Server no nó de controle.  
  
### <a name="compute-node"></a>Nó de computação  
Os nós de computação são unidades de armazenamento e processamento de dados paralelos. Eles têm um armazenamento anexado direto e usam SQL Server para gerenciar dados do usuário.  
  
### <a name="data-movement-service-dms"></a>Serviço de movimentação de dados (DMS)  
O serviço de movimentação de dados (DMS) é executado em cada nó de computação para fazer o seguinte:  
  
-   Como parte do processamento de consultas paralelas, DMS transfere dados de e para outros nós de computador e o nó de controle.  
  
-   O DMS, em execução em cada nó de computação, recebe cargas de dados em paralelo. Os dados são carregados em paralelo diretamente do servidor de carregamento para os nós de computação  
  
-   O DMS transfere dados de cada nó de computação diretamente para o servidor de backup.  
  
-   Usando o polybase, o DMS transfere dados de e para um cluster Hadoop externo ou Azure Storage Blob.  
  
### <a name="compute-node-databases"></a>Bancos de dados do nó de computação 
Cada nó de computação executa uma instância do SQL Server para processar consultas e gerenciar dados do usuário.  
  
## <a name="appliance-fabric"></a>Malha do dispositivo  
A malha do dispositivo fornece o sistema operacional, os serviços e a infraestrutura de rede para o dispositivo.  
  
### <a name="domain-controller"></a>Controlador de domínio  
Serviços de domínio do Active Directory (AD) (DS)  
O Analytics Platform System executa a autenticação entre os nós do sistema de plataforma de análise e gerencia a autenticação de SQL Server PDW logons de autenticação do Windows.  
  
Serviço DNS  
O DNS (serviço de nomes de domínio do Windows) resolve nomes de domínio para endereços IP para o dispositivo de sistema de plataforma de análise.  
  
### <a name="windows-deployment-service"></a>Serviço de implantação do Windows  
O WDS (serviço de implantação do Windows) implanta o sistema operacional Windows Server no dispositivo. Ele é implantado em todos os hosts e máquinas virtuais em todo o dispositivo.  
  
O serviço DHCP cria endereços IP para que os hosts dentro do domínio do dispositivo possam ingressar na rede do dispositivo sem ter um endereço IP pré-configurado.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
O Analytics Platform System usa a virtualização para obter alta disponibilidade. O Virtual Machine Manager hospeda o System Center para implantar o sistema operacional nos hosts físicos.  
  
Windows Server Update Services (WSUS) para aplicar ou remover as atualizações do Windows em todos os hosts e máquinas virtuais.  
  
### <a name="windows-server"></a>Windows Server  
Todos os hosts e máquinas virtuais no dispositivo executam o sistema operacional Windows Server.  
  
### <a name="failover-clustering"></a>Clustering de failover  
O clustering de failover do Windows fornece a capacidade de reiniciar processos em um host passivo no caso de um host falhar.  
  
### <a name="storage-spaces"></a>Espaços de Armazenamento  
Os espaços de armazenamento do Windows gerenciam os dados do usuário como um pool de armazenamento para um pequeno grupo de nós de computação. Se um nó de computação falhar, os dados ainda estarão acessíveis por meio de outro nó de computação no grupo.  
  
### <a name="hyper-v"></a>Hyper-V  
O Microsoft Hyper-V Server fornece uma solução de virtualização simples e confiável. O Analytics Platform System usa virtualização para balancear os recursos de CPU e fornecer alta disponibilidade para os nós do PDW e para os componentes do Appliance Fabric.  
  
## <a name="non-relational-data"></a><a name="sec2"></a>Dados não relacionais
A tecnologia polybase integra dados de SQL Server PDW com dados do Hadoop externos. Os dados do Hadoop podem ser armazenados em qualquer uma dessas fontes de dados do Hadoop:  
  
-   Distribuição do Hadoop Hortonworks  
  
-   Distribuição Cloudera do Hadoop  
  
-   Dados do HDInsight armazenados em Azure Storage Blob  
  
## <a name="query-tools"></a>Ferramentas de consulta   
  
As consultas são gravadas\-com o Transact SQL modificado para se ajustar à natureza do MPP das consultas. Todas as consultas são enviadas para o nó de controle, que gera um plano de consulta paralelo para executar a consulta nos nós de computação.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
O SQL Server Data Tools é executado dentro do Visual Studio e é nossa ferramenta de GUI recomendada para enviar consultas para SQL Server PDW. É semelhante a SQL Server Management Studio, permitindo que você navegue por um pesquisador de objetos.  
  
Se você ainda não tiver o Visual Studio, poderá baixar as ferramentas de que precisa gratuitamente. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Ferramenta de consulta de linha de comando sqlcmd  
o sqlcmd é a ferramenta de linha de comando SQL Server para\-executar instruções Transact SQL e comandos do sistema. Ele funciona com SQL Server PDW e é nossa ferramenta de linha de comando recomendada para consultar SQL Server PDW. Com o sqlcmd, você pode\-executar instruções Transact SQL interativamente a partir da linha de comando, como um arquivo em lotes ou do Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Você pode usar Integration Services para consultar SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Servidor vinculado  
Usando uma conexão de servidor vinculado SQL Server, você pode usar SQL Server para enviar instruções\-Transact SQL para SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Ferramentas de Business Intelligence
  
### <a name="analysis-services"></a>Serviços de análise  
O SQL Server PDW é uma fonte de dados válida para os modelos de Analysis Services de bancos de dados e PowerPivot do Excel. Usando o provedor de OLE DB, você pode configurar um cubo de Analysis Services para usar o processamento analítico online multidimensional (MOLAP) ou o armazenamento de ROLAP (processamento analítico online) relacional.  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Construtor de Relatórios  
Você pode usar SQL Server PDW como uma fonte de dados de SQL Server para relatórios que você desenvolve para Reporting Services usando SQL Server Construtor de Relatórios. Você também pode usar SQL Server PDW como uma fonte de SQL Server para modelos de relatório. Usando Report Manager ou a API do servidor de relatório, você pode gerar um modelo de um banco de dados SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot para Excel  
Você pode se conectar a SQL Server PDW com o PowerPivot para Excel, um download gratuito que expande significativamente os recursos de análise de dados do Excel.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Carregando ferramentas 
  
### <a name="integration-services"></a>Integration Services  
Instale os adaptadores de destino específicos do PDW que permitem usar os serviços ServerIntegrations do SQL para carregar dados no SQL Server PDW.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Carregador de linha de comando dwloader  
dwloader é uma ferramenta de carregamento de linha de comando que carrega dados em paralelo do seu servidor de carregamento para os nós de computação SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>Polybase para integração do Hadoop  
Com a tecnologia polybase, você pode carregar dados não relacionais de um cluster Hadoop em uma tabela relacional no SQL Server PDW. Os dados do Hadoop podem estar localizados em um cluster Hadoop externo ou em um Azure Storage Blob.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Backup e restauração de banco de dados  
O SQL Server PDW usa comandos de backup e restauração de banco de dados Transact-SQL para fazer backup e restaurar bancos de dados de usuário, em paralelo, de e para um servidor de backup. SQL Server PDW grava o backup em um diretório em um compartilhamento de arquivos do Windows e, da mesma forma, restaura os dados de um compartilhamento de arquivos do Windows.  
  
Para obter mais informações, consulte [planejar o backup e carregar hardware](backup-and-loading-hardware.md) e [visão geral de backup e restauração](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Cópia de tabela remota  
O recurso de cópia de tabela remota permite copiar tabelas de bancos de dados SQL Server PDW para bancos de dados de SQL Server SMP remotos (não dispositivos). Isso habilita cenários de Hub e spoke para SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Monitoramento  
O Analytics Platform System tem várias maneiras de monitorar a atividade do dispositivo  
  
### <a name="admin-console"></a>Console de administração  
O console de administração permite que você exiba o status atual sobre a integridade do dispositivo. Isso é executado como um aplicativo Web no nó de controle e pode ser acessado via HTTPS.  
  
Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Exibições do sistema  
O console de administração do é baseado em consultas de exibição do sistema. Você pode consultar as exibições do sistema individualmente para obter a informação específica de que precisa.  

Para obter mais informações, consulte [monitorar o dispositivo usando as exibições do sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Há pacotes de gerenciamento System Center Operations Manager (SCOM) para SQL Server PDW. 

Para configurar o dispositivo para o SCOM, consulte [monitorar o dispositivo usando System Center Operations Manager &#40;o sistema de plataforma de análise&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
