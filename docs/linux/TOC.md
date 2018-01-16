# [Sobre o SQL Server no Linux](sql-server-linux-overview.md)

# Visão geral
## [Notas de versão](sql-server-linux-release-notes.md)
## [O que há de novo nesta versão?](sql-server-linux-whats-new.md)
## [Artigos novos e atualizados](new-updated-linux.md)
## [Edições e recursos com suporte](sql-server-linux-editions-and-components-2017.md)

# Guias de início rápido
## [Instalar e conectar – Red Hat](quickstart-install-connect-red-hat.md)
## [Instalar e conectar – SUSE](quickstart-install-connect-suse.md)
## [Instalar e conectar – Ubuntu](quickstart-install-connect-ubuntu.md)
## [Executar e conectar – Docker](quickstart-install-connect-docker.md)
## [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
## [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

# Tutoriais
## [1_Migrar do Windows](sql-server-linux-migrate-restore-database.md)
## [2_Migrar do Oracle](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)
## [3_Migrar para Docker](tutorial-restore-backup-in-sql-server-container.md)
## [4_Criar um trabalho](sql-server-linux-run-sql-server-agent-job.md)
## [5_Configurar autenticação do AD](sql-server-linux-active-directory-authentication.md)
## [6_Criar instância de Cluster de Failover](sql-server-linux-shared-disk-cluster-configure.md)
### [iSCSI](sql-server-linux-shared-disk-cluster-configure-iscsi.md)
### [NFS](sql-server-linux-shared-disk-cluster-configure-nfs.md)
### [SMB](sql-server-linux-shared-disk-cluster-configure-smb.md)
## [7_Implantar um Pacemaker cluster](sql-server-linux-deploy-pacemaker-cluster.md)
## [8_Criar e configurar grupos de disponibilidade](sql-server-linux-create-availability-group.md)
## [9_Configurar no Kubernetes para alta disponibilidade](tutorial-sql-server-containers-kubernetes.md)

# Conceitos
## Instalar
### [Instalar o SQL Server](sql-server-linux-setup.md)
### [Instalar as ferramentas do SQL Server](sql-server-linux-setup-tools.md)
### [Instalar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)
### [Instalar a pesquisa de texto completo do SQL Server](sql-server-linux-setup-full-text-search.md)
### [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
### [Registrar repositório GA](sql-server-linux-change-repo.md)

## Configurar
### [Configurar com mssql-conf](sql-server-linux-configure-mssql-conf.md)
### [Variáveis de ambiente](sql-server-linux-configure-environment-variables.md)
### [Configurar contêineres do Docker](sql-server-linux-configure-docker.md)
### [Comentários do cliente](sql-server-linux-customer-feedback.md)

## [Desenvolver](sql-server-linux-develop-overview.md)
### [Bibliotecas de conectividade](sql-server-linux-develop-connectivity-libraries.md)
### [Usar o Visual Studio Code](sql-server-linux-develop-use-vscode.md)
### [Usar o SSMS](sql-server-linux-develop-use-ssms.md)
### [Usar o SSDT](sql-server-linux-develop-use-ssdt.md)

## [Gerenciar](sql-server-linux-management-overview.md)
### [Usar o SSMS para gerenciar](sql-server-linux-manage-ssms.md)
### [Usar o PowerShell para gerenciar](sql-server-linux-manage-powershell.md)
### [Usar o envio de logs](sql-server-linux-use-log-shipping.md)
### [Usar o DB Mail e os alertas de email](sql-server-linux-db-mail-sql-agent.md)
### [Configurar múltiplas sub-redes para disponibilidade](sql-server-linux-configure-multiple-subnet.md)

## [Migrar](sql-server-linux-migrate-overview.md)
### [Exportar e importar um BACPAC do Windows](sql-server-linux-migrate-ssms.md)
### [Migrar com o Assistente de Migração do SQL Server](sql-server-linux-migrate-ssma.md)
### [Cópia em massa com bcp](sql-server-linux-migrate-bcp.md)

## [Extrair, transformar e carregar](sql-server-linux-migrate-ssis.md)
### [Limitações e problemas conhecidos](sql-server-linux-ssis-known-issues.md)
### [Configurar SSIS](sql-server-linux-configure-ssis.md)
### [Agendar pacotes SSIS](sql-server-linux-schedule-ssis-packages.md)

## [Configurar a continuidade dos negócios](sql-server-linux-business-continuity-dr.md)
### [Noções básicas de disponibilidade](sql-server-linux-ha-basics.md)
### [Backup e restauração](sql-server-linux-backup-and-restore-database.md)
#### [Interface de dispositivo virtual – Linux](sql-server-linux-backup-vdi-specification.md)
### [Instância de cluster de failover](sql-server-linux-shared-disk-cluster-concepts.md)
#### [Red Hat Enterprise Linux (RHEL)]()
##### [Configurar (complemento de alta disponibilidade)](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)
##### [Operar (complemento de alta disponibilidade)](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
#### [SUSE Linux Enterprise Server (SLES)]()
##### [Configurar (complemento de alta disponibilidade)](sql-server-linux-shared-disk-cluster-sles-configure.md)
### [Grupos de disponibilidade](sql-server-linux-availability-group-overview.md)
#### [Criar para alta disponibilidade](sql-server-linux-availability-group-ha.md)
##### [Configurar grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md)
##### [Configurar em RHEL](sql-server-linux-availability-group-cluster-rhel.md)
##### [Configurar em SLES](sql-server-linux-availability-group-cluster-sles.md)
##### [Configurar em Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
##### [Operar](sql-server-linux-availability-group-failover-ha.md)
#### [Criar para escala de leitura apenas]()
##### [Configurar grupo de disponibilidade](sql-server-linux-availability-group-configure-rs.md)

## [Segurança](sql-server-linux-security-overview.md)
### [Introdução a recursos de segurança](sql-server-linux-security-get-started.md)
### [Criptografar conexões](sql-server-linux-encrypted-connections.md)

## Desempenho
### [Práticas recomendadas](sql-server-linux-performance-best-practices.md)
### [Introdução aos recursos de desempenho](sql-server-linux-performance-get-started.md)

# Exemplos
## Instalação autônoma
### [Red Hat Enterprise Linux (RHEL)](sample-unattended-install-redhat.md)
### [SUSE Linux Enterprise Server (SLES)](sample-unattended-install-suse.md)
### [Ubuntu](sample-unattended-install-ubuntu.md)

# Recursos
## [Perguntas Frequentes](sql-server-linux-faq.md)
## [Solucionar problemas](sql-server-linux-troubleshooting-guide.md)
## [SQL Server, documentação](../sql-server/sql-server-technical-documentation.md)
## Parceiros
### [Monitoramento](../sql-server/partner-monitor-sql-server.md)
### [Alta disponibilidade e recuperação de desastre](../sql-server/partner-hadr-sql-server.md)
### [Gerenciamento](../sql-server/partner-management-sql-server.md)
### [Desenvolvimento](../sql-server/partner-dev-sql-server.md)
## [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)
## [Estouro de pilha](http://stackoverflow.com/questions/tagged/sql-server)
## [Fóruns do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
## [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)
## [Reddit](https://www.reddit.com/r/SQLServer)
