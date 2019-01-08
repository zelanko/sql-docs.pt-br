---
title: Componentes do Data Warehouse - Analytics Platform System em paralelo | Microsoft Docs
description: Este artigo explica o software de dispositivo e os componentes de software não seja de dispositivo do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: aaf90124cc7877b633a997a2c4f170057b965028
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510927"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>Componentes do Data Warehouse - Analytics Platform System em paralelo
Este artigo explica o software de dispositivo e os componentes de software não seja de dispositivo do Analytics Platform System.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software de Data Warehouse em paralelo](media/parallel-data-warehouse-software.png "software Parallel Data Warehouse")  
  
## <a name="sec1"></a>Software do dispositivo - armazenamento de dados de usuário e processamento de consulta  
  
### <a name="control-node"></a>Nó de controle  
Mecanismo MPP  
O mecanismo MPP é o cérebro do sistema paralela MPP (processamento). Ele faz o seguinte:  
  
-   Cria planos de consulta paralelos e coordena a execução de consulta paralela em nós de computação.  
  
-   Armazena e coordena os metadados e dados de configuração para todos os bancos de dados.  
  
-   Gerencia a autorização e autenticação de banco de dados do SQL Server PDW.  
  
-   Rastreia o status de hardware e software.  
  
### <a name="data-movement-service-dms"></a>Serviço de movimentação de dados (DMS)  
Serviço de movimentação de dados (DMS) é parte do "ingrediente secreto" do PDW. Ele faz o seguinte:  
  
-   Transferências de dados de e para os nós do SQL Server PDW.  
  
-   Processos de operações que exigem a transferência de dados entre os nós de consulta.  
  
-   Melhora o desempenho de consulta ao otimizar velocidades de transferência de dados.  
  
### <a name="admin-console"></a>Console de administração  
O Console de administração é um aplicativo web que apresenta o estado do dispositivo, integridade e informações de desempenho.  
  
### <a name="configuration-manager"></a>Configuration Manager  
O Configuration Manager (dwconfig.exe) é a ferramenta que os administradores do dispositivo usam para configurar o Analytics Platform System.  
  
### <a name="control-node-databases"></a>Bancos de dados de nó de controle  
SQL Server gerencia todos os bancos de dados no nó de controle.  
  
-   O banco de dados Shell gerencia os metadados de todos os bancos de dados de usuário distribuída.  
  
-   TempDB contém os metadados para todas as tabelas temporárias de usuário entre o dispositivo.  
  
-   Mestre é a tabela mestra para o SQL Server no nó de controle.  
  
### <a name="compute-node"></a>Nó de computação  
Os nós de computação são unidades de armazenamento e processamento paralelo de dados. Eles têm armazenamento anexado direto e usam o SQL Server para gerenciar os dados de usuário.  
  
### <a name="data-movement-service-dms"></a>Serviço de movimentação de dados (DMS)  
Serviço de movimentação de dados (DMS) é executado em cada nó de computação para fazer o seguinte:  
  
-   Como parte do processamento de consultas paralelas, o DMS transferir dados e para outros nós do computador e o nó de controle.  
  
-   DMS, em execução em cada nó de computação, recebe os carregamentos de dados em paralelo. Dados são carregados em paralelo diretamente do servidor de carregamento para os nós de computação  
  
-   DMS transfere os dados de cada nó de computação diretamente para o servidor de backup.  
  
-   Usando o PolyBase, o DMS transfere dados de e para um cluster Hadoop externo ou o armazenamento de BLOBs do Azure.  
  
### <a name="compute-node-databases"></a>Bancos de dados do nó de computação 
Cada nó de computação executa uma instância do SQL Server para processar as consultas e gerenciar dados de usuário.  
  
## <a name="appliance-fabric"></a>Malha de dispositivo  
A malha de dispositivo fornece o sistema operacional, serviços e infraestrutura de rede para o dispositivo.  
  
### <a name="domain-controller"></a>Controlador de domínio  
Serviços de domínio do Active Directory (AD) (DS)  
O Analytics Platform System realiza a autenticação entre os nós do Analytics Platform System e gerencia a autenticação de logons de autenticação do Windows do SQL Server PDW.  
  
Serviço DNS  
Serviço de nome de domínio (DNS) Windows resolve nomes de domínio para endereços IP para o dispositivo do Analytics Platform System.  
  
### <a name="windows-deployment-service"></a>Serviço de implantação do Windows  
Serviço de implantação do Windows (WDS) implanta o sistema de operacional do Windows Server para o dispositivo. Ele é implantado em cada host e máquina virtual entre o dispositivo.  
  
O serviço DHCP cria endereços IP para que os hosts dentro do domínio de dispositivo podem se associar à rede de dispositivo sem a necessidade de um endereço IP configurado previamente.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
O Analytics Platform System usa a virtualização para alcançar alta disponibilidade. O Virtual Machine Manager hospeda o System Center para implantar o sistema operacional nos hosts físicos.  
  
Windows Server Update Services (WSUS) para aplicar ou remover as atualizações do Windows em todos os hosts e máquinas virtuais.  
  
### <a name="windows-server"></a>Windows Server  
Todos os hosts e máquinas virtuais no dispositivo de executam o sistema operacional Windows Server.  
  
### <a name="failover-clustering"></a>Clustering de failover  
Clustering de Failover do Windows fornece a capacidade de reiniciar processos em um host passivo que um host falhar.  
  
### <a name="storage-spaces"></a>Espaços de armazenamento  
Espaços de armazenamento do Windows gerencia dados de usuário como um pool de armazenamento para um pequeno grupo de nós de computação. Se um nó de computação falhar, os dados são ainda pode ser acessados por meio de outro nó de computação no grupo.  
  
### <a name="hyper-v"></a>Hyper-v  
Microsoft Hyper-V Server fornece uma solução de virtualização simples e confiável. Analytics Platform System usa para virtualização para equilibrar os recursos de CPU e para fornecer alta disponibilidade para os nós PDW e o dispositivo de componentes da malha.  
  
## <a name="sec2"></a>Dados não relacionais
A tecnologia PolyBase integra-se a dados do SQL Server PDW com dados externos do Hadoop. Os dados Hadoop podem ser armazenados em qualquer uma dessas fontes de dados do Hadoop:  
  
-   Distribuição do Hadoop da Hortonworks  
  
-   Distribuição Cloudera do Hadoop  
  
-   Dados armazenados no armazenamento de BLOBs do Azure em HDInsight  
  
## <a name="query-tools"></a>Ferramentas de consulta   
  
Consultas são escritas com Transact\-SQL modificado de acordo com a natureza do MPP das consultas. Todas as consultas são enviadas para o nó de controle, que gera um plano de consulta paralela para executar a consulta em todos os nós de computação.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools é executado dentro do Visual Studio e é nossa ferramenta de GUI recomendada para enviar consultas para o SQL Server PDW. Ele é semelhante ao SQL Server Management Studio, permitindo que você navegue por meio de um pesquisador de objetos.  
  
Se você ainda não tiver o Visual Studio, você pode baixar as ferramentas que você precisa gratuitamente. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Ferramenta de linha de comando de consulta do Sqlcmd  
Sqlcmd é a ferramenta de linha de comando do SQL Server para a execução Transact\-SQL instruções e comandos do sistema. Ele funciona com o SQL Server PDW e é nossa ferramenta de linha de comando recomendada para consultar o SQL Server PDW. Com o sqlcmd, você pode executar Transact\-instruções SQL interativamente na linha de comando, como um arquivo em lotes, ou do Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Você pode usar o Integration Services para consultar o SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Servidor vinculado  
Usando uma conexão de servidor vinculado do SQL Server, você pode usar o SQL Server para enviar Transact\-instruções SQL para SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Ferramentas de Business Intelligence
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW é uma fonte de dados válida para bancos de dados do Analysis Services e modelos do PowerPivot do Excel. Usando o provedor OLE DB, você pode configurar um cubo do Analysis Services para usar o processamento analítico online multidimensional (MOLAP) ou armazenamento de processamento analítico online relacional (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Construtor de Relatórios  
Você pode usar o SQL Server PDW como uma fonte de dados do SQL Server para relatórios que você desenvolve para o Reporting Services usando o construtor de relatórios do SQL Server. Você também pode usar o SQL Server PDW como uma fonte de SQL Server para modelos de relatório. Usando o Gerenciador de relatórios ou a API do servidor de relatório, você pode gerar um modelo de um banco de dados do SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot para Excel  
Você pode se conectar ao SQL Server PDW com o PowerPivot para Excel, um download gratuito que expande os recursos de análise de dados do Excel de forma significativa.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Ferramentas de carregamento 
  
### <a name="integration-services"></a>Integration Services  
Instale adaptadores de destino do PDW específicos que permitem que você use serviços de ServerIntegration SQL para carregar dados no SQL Server PDW.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Carregador de linha de comando do dwloader  
dwloader é uma ferramenta de linha de comando de carregamento que carrega dados em paralelo de seu servidor de carregamento para os nós de computação do SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase para integração com o Hadoop  
Com a tecnologia PolyBase, você pode carregar os dados não relacionais de um Hadoop Cluster em uma tabela relacional no SQL Server PDW. Os dados do Hadoop podem estar localizados em um Hadoop Cluster externo ou em um Blob de armazenamento do Azure.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Banco de dados Backup e restauração  
SQL Server PDW usa o backup do banco de dados Transact-SQL e comandos de restauração para fazer backup e restaurar bancos de dados de usuário, em paralelo, de e para um servidor de backup. SQL Server PDW grava o backup para um diretório em um compartilhamento de arquivos do Windows e, em seguida, da mesma forma restaura dados de um compartilhamento de arquivos do Windows.  
  
Para obter mais informações, consulte [plano de Backup e carregamento de Hardware](backup-and-loading-hardware.md) e [Backup e restaurar visão geral](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Cópia de tabela remota  
O recurso de cópia de tabela remota permite que você copiar tabelas de bancos de dados do SQL Server PDW para bancos de dados do SQL Server do SMP (não seja de dispositivo) remotos. Isso permite cenários de hub e spoke para SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Monitoramento  
O Analytics Platform System tem várias maneiras de monitorar a atividade de dispositivo  
  
### <a name="admin-console"></a>Console de administração  
O Console de administração permite que você exibir o status atuais sobre a integridade do dispositivo. Isso é executado como um aplicativo web no nó de controle e é acessível via https.  
  
Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração do &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Exibições do sistema  
O Console de administração se baseia em consultas de modo de exibição do sistema. Você pode consultar as exibições do sistema individualmente para obter a parte específica de informações que você precisa.  

Para obter mais informações, consulte [monitorar o dispositivo por exibições do sistema usando o &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Há pacotes de gerenciamento do System Center Operations Manager (SCOM) para SQL Server PDW. 

Para configurar o dispositivo para o SCOM, consulte [monitorar o dispositivo por usando o System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
