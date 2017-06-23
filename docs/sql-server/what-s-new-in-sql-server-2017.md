---
title: O que &#39; s no SQL Server de 2017 | Microsoft Docs
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: aa08b5e7de9bb317fd781a98ee5d829431b92df6
ms.openlocfilehash: 66c9bc4f2cba20076c357d27fdfacbc767a94c5c
ms.contentlocale: pt-br
ms.lasthandoff: 06/23/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>O que &#39; s no SQL Server de 2017
SQL Server 2017 representa uma etapa importante para fazer do SQL Server em uma plataforma que oferece opções de linguagens de desenvolvimento, tipos de dados, locais e na nuvem e em sistemas operacionais, colocando a capacidade do SQL Server para Linux, contêineres do Docker com base em Linux e Windows.

Este tópico é um resumo do que há de novo no mais recente versão Community Technical Preview (CTP) e links para mais detalhes das novidades para as áreas de recurso específico.

![info_tip](../sql-server/media/info-tip.png) Execute o SQL Server no Linux! Para obter mais informações, consulte:
-  [Novidades do SQL Server 2017 no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [Documentação de SQL Server no Linux](https://docs.microsoft.com/sql/linux/)


**Experimente:**    
   -   [![Baixar no Centro de avaliação](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  **[baixar o SQL Server de 2017 Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>Novidades no SQL Server de 2017 CTP 2.1 (maio de 2017)
### <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server  
- Um novo DMF, [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), é apresentada para expor atributos de nível de resumos e as informações nos arquivos de log de transações; útil para monitorar a integridade do log de transações.  
- Este CTP contém correções e melhorias de desempenho para o mecanismo de banco de dados.
- Para obter uma lista detalhada de 2017 aprimoramentos do CTP em versões anteriores do CTP, consulte [Novidades no SQL Server 2017 (mecanismo de banco de dados)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- SQL Server Reporting Services não está mais disponível para instalar por meio da instalação do SQL Server a partir do CTP 2.1.
- Comentários agora estão disponíveis para relatórios. Comentários que você adicionar perspectiva ao que está em um relatório e colaborar com outras pessoas em sua organização. Você também pode incluir os anexos com o seu comentário.
- Para obter informações mais detalhadas sobre as novidades do SSRS, incluindo detalhes de versões anteriores, veja [Novidades do Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Para obter informações sobre o servidor de relatório do Power BI, consulte [Introdução ao servidor de relatório do Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

### <a name="sql-server-machine-learning-services"></a>Serviços de aprendizado de máquina do SQL Server
- Não há recursos novos serviços de aprendizado de máquina neste CTP.
- Para obter mais serviços de aprendizado de máquina que novas informações, incluindo detalhes de CTPs anteriores, consulte [o que há de novo nos serviços de aprendizado de máquina do SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

### <a name="sql-server-analysis-services-ssas"></a>SSAS (SQL Server Analysis Services)
- Não há recursos novos do SSAS neste CTP.  
- Para obter mais detalhes sobre melhorias e correções nesta versão, consulte [o que há de novo no SQL Server de 2017 Analysis Services](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
-   Agora você pode usar o **Use32BitRuntime** parâmetro.
-   O desempenho de registro em log foi aprimorado.
- Para obter mais SSIS que novas informações, incluindo detalhes de CTPs anteriores, consulte [Novidades nos serviços de integração do SQL Server de 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>Novidades no SQL Server de 2017 CTP 2.0 (abril de 2017)
### <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server
- **Recompilação de índice online retomáveis**. Recompilação de índice online reiniciável permite que você retome uma operação de recompilação de índice online de onde parou após uma falha. Por exemplo, um failover em uma réplica ou uma situação de espaço em disco insuficiente. Você pode também pausar e retomar a uma operação de recompilação de índice online mais tarde. Por exemplo, talvez seja necessário para temporariamente liberar recursos de sistemas para executar uma tarefa de alta prioridade ou concluir a recompilação de índice em outra janela miniatous se as janelas de manutenção disponível é muito pequeno para uma tabela grande. Por fim, recompilação de índice online retomáveis não requer espaço de log significativa, que permite que você execute o truncamento de log enquanto a operação de recriação retomáveis está em execução. Consulte [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) e [diretrizes para operações de índice online](../relational-databases/indexes/guidelines-for-online-index-operations.md).
- **A opção IDENTITY_CACHE para ALTER DATABASE SCOPED CONFIGURATION**. Uma nova opção IDENTITY_CACHE foi adicionada à instrução ALTER DATABASE com escopo configuração T-SQL. Quando essa opção é definida como OFF, lacunas podem ser evitadas nos valores das colunas de identidade no caso de um servidor for reiniciado inesperadamente ou fizer failover para um servidor secundário. Consulte [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).  
- CLR usa segurança de acesso do código (CAS) no .NET Framework, que não é mais suportado como um limite de segurança. Um assembly CLR criado com `PERMISSION_SET = SAFE` pode ser capaz de acessar recursos externos do sistema, chamar código não gerenciado e adquirir privilégios de sysadmin. Começando com [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)], uma `sp_configure` opção chamada `clr strict security` é introduzido para aumentar a segurança de assemblies do CLR. `clr strict security`é habilitado por padrão e trata `SAFE` e `EXTERNAL_ACCESS` assemblies como se eles foram marcados `UNSAFE`. O `clr strict security` opção pode ser desabilitada para compatibilidade com versões anteriores, mas não é recomendado. A Microsoft recomenda que todos os assemblies ser assinados por um certificado ou chave assimétrica com um logon correspondente que tenha sido concedido `UNSAFE ASSEMBLY` no banco de dados mestre. Para obter mais informações, consulte [segurança estrita CLR](../database-engine/configure-windows/clr-strict-security.md).  
- Recursos de banco de dados do gráfico para o modelo de relações de muitos-para-muitos. Isso inclui novos [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) sintaxe para criar o nó e tabelas de borda e a palavra-chave [correspondência](../t-sql/queries/match-sql-graph.md) para consultas. Para obter mais informações, consulte [de processamento gráfico com o SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md).   
- Ajuste automático é um recurso de banco de dados que fornece informações sobre consulta possível problemas de desempenho, ele pode recomendar soluções e correção identificadas problemas. O ajuste automático [!INCLUDE[ssnoversion](../includes/ssnoversion.md)], notifica você sempre que um problema de desempenho potencial é detectado e permite que você aplique ações corretivas ou permite que o [!INCLUDE[ssde](../includes/ssde-md.md)] corrigir automaticamente os problemas de desempenho. Para obter mais informações, consulte [ajuste automático](../relational-databases/automatic-tuning/automatic-tuning.md).  
-   Lote modo adaptável Join para melhorar a qualidade do plano (sob a compatibilidade do banco de dados 140).
-   Execução intercalada de várias instruções T-SQL TVFs melhorar a qualidade do plano (sob a compatibilidade do banco de dados 140).
- Repositório de consultas agora também rastreia informações de resumo de estatísticas de espera. Categorias de estatísticas de espera por consulta no repositório de consultas de controle permite que o próximo nível de desempenho experiência de solução de problemas, fornecendo ainda mais informações sobre o desempenho da carga de trabalho e seus afunilamentos enquanto preserva as principais vantagens de repositório de consultas.
- Suporte DTC para grupos de disponibilidade AlwaysOn para todas as transações de banco de dados entre bancos de dados que fazem parte do grupo de disponibilidade, incluindo bancos de dados que fazem parte da mesma instância. Para obter mais informações, consulte [transações - grupos de disponibilidade AlwaysOn e espelhamento de banco de dados](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- Uma nova coluna **modified_extent_page_count** foi introduzido no [sys.DM db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) para controlar alterações diferenciais em cada arquivo de banco de dados do banco de dados.
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) agora dá suporte ao carregamento de uma tabela em um grupo de arquivos que não seja um grupo de arquivos padrão do usuário usando o **ON** palavra-chave.
- Instalação do SQL Server oferece suporte à especificação de tamanho do arquivo tempdb inicial até **256 GB (262.144 MB)** por arquivo com um aviso se o tamanho do arquivo é definido como um valor maior que **1 GB** e se IFI não estiver habilitado.
- Um novo modo de exibição (DMV de gerenciamento dinâmico) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) é introduzido para controlar o uso do armazenamento de versão por banco de dados.
- Um novo DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) é introduzido para expor as informações de VLF semelhantes para DBCC LOGINFO.
- Tabelas temporais com versão de sistema agora oferecem suporte a exclusão em cascata e CASCADE UPDATE.
- Este CTP contém correções de bugs para o Mecanismo do Banco de Dados.
- Para obter uma lista detalhada de 2017 aprimoramentos do CTP em versões anteriores do CTP, consulte [Novidades no SQL Server 2017 (mecanismo de banco de dados)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).   

### <a name="sql-server-machine-learning-services"></a>Serviços de aprendizado de máquina do SQL Server
- SQL Server R Services tem um novo nome para refletir o suporte para a linguagem Python no CTP 2.0. Agora você pode usar os serviços de aprendizado de máquina do SQL Server (no banco de dados) para executar scripts R ou Python no SQL Server. Ou então, instale o Microsoft Machine Learning Server (autônomo) para implantar e consumir R e Python modelos que não exigem o SQL Server. 
- Ambas as plataformas incluem novos algoritmos MicrosoftML para aprendizado de máquina distribuída e a versão mais recente do Microsoft R (versão 9.1.0).
- Para obter mais informações, consulte [novidades para o aprendizado de máquina](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>Novidades no SQL Server de 2017 CTP 1.4 (março de 2017)
### <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server
- Não há nenhum recurso novo do Mecanismo de Banco de Dados neste CTP.
- Este CTP contém correções de bugs para o Mecanismo do Banco de Dados.
- Para obter uma lista detalhada de 2017 aprimoramentos do CTP em versões anteriores do CTP, consulte [Novidades no SQL Server 2017 (mecanismo de banco de dados)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-r-services"></a>SQL Server R Services
- Não há recursos novos do R Services neste CTP.
- Para obter informações mais detalhadas sobre as novidades do R Services, incluindo detalhes de CTPs anteriores, consulte [Novidades do SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md).  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- Não há novos recursos do SSRS neste CTP.
- Para obter informações mais detalhadas sobre as novidades do SSRS, incluindo detalhes de versões anteriores, veja [Novidades do Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 

### <a name="sql-server-analysis-services-ssas"></a>SSAS (SQL Server Analysis Services)
- Não há recursos novos do SSAS neste CTP.  
- Para obter detalhes, incluindo novidades do Analysis Services em versões de visualização mais recentes do SSDT e SSMS, consulte [Novidades no Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- Não há recursos novos do SSIS neste CTP.
- Para obter mais SSIS que novas informações, incluindo detalhes de CTPs anteriores, consulte [Novidades nos serviços de integração 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>Novidades no SQL Server de 2017 CTP 1.3 (fevereiro de 2017)
### <a name="sql-server-database-engine"></a>Mecanismo de Banco de Dados do SQL Server
- Melhorias indiretas de desempenho do ponto de verificação.
- Suporte a grupos de disponibilidade sem cluster adicionado.
- Configuração de Grupos de Disponibilidade de Confirmação de Réplica Mínima adicionada.
- Os Grupos de Disponibilidade agora podem trabalhar no Windows-Linux para permitir as migrações e testes entre sistemas operacionais.
- Adicionado o suporte da política de retenção de tabelas temporal. Para obter mais informações, consulte [gerenciar retenção de dados históricos em tabelas temporais com versão de sistema](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach).
- Novo DMV SYS.DM_DB_STATS_HISTOGRAM
- On-line columnstore não clusterizado compilação de índice e recriar o suporte adicionado
- Cinco novas exibições de gerenciamento dinâmico para retornar informações sobre o processo do Linux. Para saber mais, veja [Exibições de Gerenciamento Dinâmico de Processos do Linux](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) é adicionado para análise de estatísticas.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- Dicas de codificação - um recurso avançado usado para otimizar o processamento (atualização de dados) de grandes modelos de tabela na memória. Para obter mais informações, consulte [Novidades no Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md). 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Entre em contato com a equipe de engenharia do SQL Server 
- [Stack Overflow (marcação sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [Fóruns do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect – relatar bugs e solicitar recursos](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit – discussão geral sobre R](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>Consulte também    
- ![Notas de versão](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [notas de versão do SQL Server de 2017](../sql-server/sql-server-2017-release-notes.md). 
- [Recursos com suporte por Edição](https://msdn.microsoft.com/library/cc645993.aspx)
- [Requisitos de instalação de hardware e software](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [Assistente de instalação do SQL Server](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Instalar atualizações de serviço do SQL Server](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

