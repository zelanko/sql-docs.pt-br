# Visão geral

## [O que são os Serviços de Machine Learning do SQL Server?](what-is-sql-server-machine-learning.md)
### [Análise no banco de dados](r/sql-server-r-services.md)
### [Servidor autônomo](r/r-server-standalone.md)
## [Novos recursos](what-s-new-in-sql-server-machine-learning-services.md)
## [Recursos por edição](r/differences-in-r-features-between-editions-of-sql-server.md)

# [Arquitetura](architecture-overview-machine-learning.md)
## [R](r/architecture-overview-sql-server-r.md)
### [Interoperabilidade de R](r/r-interoperability-in-sql-server.md)
### [Componentes que dão suporte à integração de R](r/new-components-in-sql-server-to-support-r.md)
### [Segurança para R](r/security-overview-sql-server-r.md)
## [Python](python/architecture-overview-sql-server-python.md)
### [Python nos Serviços de Machine Learning](python/sql-server-python-services.md)
### [Interoperabilidade do Python](python/python-interoperability.md)
### [Componentes para dar suporte a Python](python/new-components-in-sql-server-to-support-python-integration.md)
### [Segurança do Python](python/security-overview-sql-server-python-services.md)
<!-- ### [How To Create a Resource Pool for Python](python/how-to-create-a-resource-pool-for-python.md)-->
<!-- ### [Extended Events for Python](python/extended-events-for-python.md)-->
<!-- ### [DMVs for Python](python/dmvs-for-python.md)-->
<!-- ### [Resource Governance for Python](python/resource-governance-for-python.md)-->

# Instalar 

## SQL Server 2017
### [Análise no banco de dados](install/sql-machine-learning-services-windows-install.md)
### [Servidor autônomo](install/sql-machine-learning-standalone-windows-install.md)
## SQL Server 2016
### [R Services (no Banco de Dados)](install/sql-r-services-windows-install.md)
### [R Server (Autônomo)](install/sql-r-standalone-windows-install.md)
## [Modelos previamente treinados](install/sql-pretrained-models-install.md)
## [Instalação de prompt de comando](install/sql-ml-component-commandline-install.md)
## [Instalação offline (sem Internet)](install/sql-ml-component-install-without-internet-access.md)
## [Atualizar R e Python](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
## [Configurar ferramentas R](r/set-up-a-data-science-client.md)
## [Configurar ferramentas Python](python/setup-python-client-tools-sql.md)

# Guias de início rápido

## R
### [Olá, Mundo em R e SQL](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
### [Lidar com entradas e saídas](tutorials/rtsql-working-with-inputs-and-outputs.md)
### [Lidar com tipos de dados e objetos](tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)
### [Criar um modelo preditivo](tutorials/rtsql-create-a-predictive-model-r.md)
### [Prever e plotar com base no modelo](tutorials/rtsql-predict-and-plot-from-model.md)

# [Tutoriais](tutorials/machine-learning-services-tutorials.md)
## [R](tutorials/sql-server-r-tutorials.md)
### [Aprender análise no banco de dados](tutorials/sqldev-in-database-r-for-sql-developers.md)
#### [1 – Obter dados e scripts](tutorials/sqldev-download-the-sample-data.md)
#### [2 – Configurar o ambiente](r/sqldev-import-data-to-sql-server-using-powershell.md)
#### [3 – Visualizar dados](tutorials/sqldev-explore-and-visualize-the-data.md)
#### [4 – Criar recursos de dados](tutorials/sqldev-create-data-features-using-t-sql.md)
#### [5 – Treinar e salvar em SQL](r/sqldev-train-and-save-a-model-using-t-sql.md)
#### [6 – Prever resultados](tutorials/sqldev-operationalize-the-model.md)

### [Passo a passo de ponta a ponta sobre a ciência de dados](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
#### [Preparar dados](tutorials/walkthrough-prepare-the-data.md)
#### [Explorar os dados usando SQL](tutorials/walkthrough-view-and-explore-the-data.md)
#### [Resumir os dados usando R](tutorials/walkthrough-view-and-summarize-data-using-r.md)
#### [Criar grafos e gráficos](tutorials/walkthrough-create-graphs-and-plots-using-r.md)
#### [Criar recursos de dados](tutorials/walkthrough-create-data-features.md)
#### [Criar e salvar o modelo](tutorials/walkthrough-build-and-save-the-model.md)
#### [Implantar e usar o modelo](tutorials/walkthrough-deploy-and-use-the-model.md)

### [Aprofundamento com RevoScaleR](tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
#### [Criar banco de dados e permissões](tutorials/deepdive-work-with-sql-server-data-using-r.md)
#### [Criar objetos de dados usando RxSqlServerData](tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
#### [Consultar e modificar dados](tutorials/deepdive-query-and-modify-the-sql-server-data.md)
#### [Definir um contexto de computação](tutorials/deepdive-define-and-use-compute-contexts.md)
#### [Criar e executar scripts do R](tutorials/deepdive-create-and-run-r-scripts.md)
#### [Visualizar dados](tutorials/deepdive-visualize-sql-server-data-using-r.md)
#### [Criar modelos](tutorials/deepdive-create-models.md)
#### [Pontuar novos dados](tutorials/deepdive-score-new-data.md)
#### [Transformar dados](tutorials/deepdive-transform-data-using-r.md)
#### [Carregar dados na memória usando rxImport](tutorials/deepdive-load-data-into-memory-using-rximport.md)
#### [Criar uma tabela usando rxDataStep](tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
#### [Executar análise de agrupamento usando rxDataStep](tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
#### [Analisar dados no contexto de computação local](tutorials/deepdive-analyze-data-in-local-compute-context.md)
#### [Mover dados entre o SQL Server e o arquivo XDF](tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
#### [Criar uma simulação simples](tutorials/deepdive-create-a-simple-simulation.md)

## [Python](tutorials/sql-server-python-tutorials.md)
### [Executar Python usando T-SQL](tutorials/run-python-using-t-sql.md)
#### [Encapsular o Python em um procedimento armazenado](tutorials/wrap-python-in-tsql-stored-procedure.md)
#### [Treinamento e pontuação em um modelo do Python no SQL Server](tutorials/train-score-using-python-in-tsql.md)
#### [Criar um modelo usando revoscalepy em um contexto de computação do SQL Server](tutorials/use-python-revoscalepy-to-create-model.md)
### [Aprender análise no banco de dados](tutorials/sqldev-in-database-python-for-sql-developers.md)
#### [Obter dados e scripts](tutorials/sqldev-py1-download-the-sample-data.md)
#### [Importar dados](tutorials/sqldev-py2-import-data-to-sql-server-using-powershell.md)
#### [Explorar e visualizar dados](tutorials/sqldev-py3-explore-and-visualize-the-data.md)
#### [Criar recursos de dados](tutorials/sqldev-py4-create-data-features-using-t-sql.md)
#### [Treinar e salvar o modelo](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)
#### [Colocar o modelo em operação](tutorials/sqldev-py6-operationalize-the-model.md)

# [Exemplos](https://github.com/Microsoft/sql-server-samples)

# [Soluções](tutorials/data-science-scenarios-and-solution-templates.md)

# [Instruções](r/sql-server-machine-learning-tasks.md)

## Gerenciamento de pacotes
### [Pacotes padrão](r/installing-and-managing-r-packages.md)
### [Obter informações sobre o pacote](r/determine-which-packages-are-installed-on-sql-server.md)
### [Instalar os novos pacotes Python](python/install-additional-python-packages-on-sql-server.md)
### [Instalar os novos pacotes R](r/install-additional-r-packages-on-sql-server.md)
#### [Usar gerenciadores de pacotes R](r/use-r-package-managers-on-sql-server.md)
#### [Usar T-SQL](r/install-r-packages-tsql.md)
#### [Usar RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)
##### [Habilitar o gerenciamento remoto de pacotes R](r/r-package-how-to-enable-or-disable.md)
##### [Sincronizar os pacotes R](r/package-install-uninstall-and-sync.md)
#### [Criar um repositório miniCRAN](r/create-a-local-package-repository-using-minicran.md)
#### [Dicas para usar pacotes de R](r/packages-installed-in-user-libraries.md)

## Exploração de dados e modelagem
### [Tipos de dados e bibliotecas do R](r/r-libraries-and-data-types.md)
### [Bibliotecas Python e tipos de dados](python/python-libraries-and-data-types.md)
### [Pontuação nativa](sql-native-scoring.md)
### [Pontuação em tempo real](real-time-scoring.md)
### [Modelagem preditiva com R](r/data-exploration-and-predictive-modeling-with-r.md)
### [Como executar pontuação em tempo real ou nativa](r/how-to-do-realtime-scoring.md)
### [Carregar objetos de R usando o ODBC](r/save-and-load-r-objects-from-sql-server-using-odbc.md)
### [Convertendo o código de R para uso nos serviços do Machine Learning](r/converting-r-code-for-use-in-sql-server.md)
### [Criando vários modelos usando rxExecBy](r/creating-multiple-models-using-rxexecby.md)
### [Usar dados de cubos OLAP no R](r/using-data-from-olap-cubes-in-r.md)
### [Criar um procedimento armazenado usando sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## Desempenho
### [Ajuste de desempenho para R – visão geral](r/sql-server-r-services-performance-tuning.md)
### [Ajuste de desempenho para R – configuração do SQL Server)](r/sql-server-configuration-r-services.md)
### [Ajuste de desempenho para R – otimização de dados e do R](r/r-and-data-optimization-r-services.md)
### [Ajuste de desempenho para R – Resultados](r/performance-case-study-r-services.md)
### [Usar funções de criação de perfil de código de R](r/using-r-code-profiling-functions.md)

## Administração
### [Configurar e gerenciar o R](r/configuration-sql-server-r-services.md)
### [Opções de configuração avançadas para serviços do Machine Learning](r/configure-and-manage-advanced-analytics-extensions.md)
### [Considerações sobre segurança para o tempo de execução de R no SQL Server](r/security-considerations-for-the-r-runtime-in-sql-server.md)
### [Modificar o pool de contas de usuário para os serviços de Machine Learning do SQL Server](r/modify-the-user-account-pool-for-sql-server-r-services.md)
### [Adicionar SQLRUserGroup como um usuário de banco de dados](r/add-sqlrusergroup-to-database.md)
### [Implantar e consumir modelos usando serviços Web](operationalization-with-mrsdeploy.md)
### [Gerenciar e monitorar soluções](r/managing-and-monitoring-r-solutions.md)
### [Governança de recursos para serviços do Machine Learning](r/resource-governance-for-r-services.md)
### [Criar um pool de recursos para o aprendizado de máquina](r/how-to-create-a-resource-pool-for-r.md)
### [Eventos estendidos para serviços do Machine Learning](r/extended-events-for-sql-server-r-services.md)
### [Eventos estendidos para monitoramento de instruções PREDICT](xe-event-predict-tsql.md)
### [DMVs para serviços do Machine Learning](r/dmvs-for-sql-server-r-services.md)
### [Usando funções de criação de perfil de código de R](r/using-r-code-profiling-functions.md)
### [Monitorar os serviços do Machine Learning usando relatórios personalizados no Management Studio](r/monitor-r-services-using-custom-reports-in-management-studio.md)

# [Referência do pacote](r/machine-learning-services-r-reference.md)

## [MicrosoftML no SQL](using-the-microsoftml-package.md)
## [RevoScaleR no SQL](r/revoscaler-overview.md)
## [Lista de funções RevoScaleR para dados do SQL Server](r/scaler-functions-for-working-with-sql-server-data.md)
## [sqlrutils no SQL](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
## [olapR no SQL](r/how-to-create-mdx-queries-using-olapr.md)
## [revoscalepy no SQL](python/what-is-revoscalepy.md)

# Recursos

## [Problemas conhecidos](known-issues-for-sql-server-machine-learning-services.md)
## [Notas de versão](https://docs.microsoft.com/sql/sql-server/sql-server-2017-release-notes)
## [Configurar uma máquina virtual](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)
## [Solução de problemas](machine-learning-troubleshooting-faq.md)
### [Coleta de Dados](data-collection-ml-troubleshooting-process.md)
### [Instalar e atualizar erros](r/upgrade-and-installation-faq-sql-server-r-services.md)
### [Launchpad e erros de execução de script externo](common-issues-external-script-execution.md)
### [Erros de script de R](r-script-execution-errors.md)

## Blogs
### [SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/)
### [R Server](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/)
### [Machine Learning](https://blogs.technet.microsoft.com/machinelearning/)

## Fóruns
### [SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver)
### [Machine Learning Server](https://social.msdn.microsoft.com/Forums/home?forum=MicrosoftR)
