---
title: "Quais são as novidades do SQL Server de 2017 RC1 no Linux | Microsoft Docs"
description: "Este tópico destaca o que há de novo para a versão atual do SQL Server 2017 no Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 649c7cbd03b6d2e61dbbb572a34cdbcd2a7ab7cd
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---

# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novidades do SQL Server 2017 no Linux

Este tópico descreve o que há de novo para 2017 do SQL Server em execução no Linux.

## <a name="rc2"></a>RC2

A versão RC2 contém diversas correções de bugs e aprimoramentos.

## <a name="rc1"></a>RC1

Versão RC1 contém os seguintes aprimoramentos e correções:

- Habilitado transparente Layer Security (TLS) para conexões criptografadas. Para obter mais informações, consulte [criptografando conexões com o SQL Server no Linux](sql-server-linux-encrypted-connections.md).
- Habilitado [autenticação do Active Directory](sql-server-linux-active-directory-authentication.md).
- Habilitado [DB Mail](../relational-databases/database-mail/database-mail.md).
- Adicionado suporte a IPV6.
- Variáveis de ambiente adicionado para a configuração inicial do SQL Server. Para obter mais informações, consulte [as configurações de configurar o SQL Server com variáveis de ambiente em Linux](sql-server-linux-configure-environment-variables.md).
- Removido **sqlpackage** do instalado binários. SqlPackage pode ainda ser executado em Linux remotamente do Windows.
- Compartilhado conjuntos de agente do disco cluster recursos que o nome do recurso como ele opera em uma instância de cluster de failover do SQL Server do Windows. `@@ServerName`Retorna o nome de recurso de cluster de disco compartilhado do SQL Server; antes do RC1 retornou o nome do nó de cluster que o recurso de propriedade.

## <a name="ctp-21"></a>CTP 2.1

A versão CTP 2.1 contém os seguintes aprimoramentos e correções:

- Adicionado [variáveis de ambiente para configurar o serviço SQL Server](sql-server-linux-configure-environment-variables.md).
- [MSSQL conf](sql-server-linux-configure-mssql-conf.md) agora requer a convenção de nomenclatura de duas partes para configurações.
- O [scripter mssql](https://github.com/Microsoft/sql-xplat-cli) ferramenta. Esse utilitário permite que desenvolvedores, DBAs e administradores do sistema gerar `CREATE` e `INSERT` scripts Transact-SQL de objetos de banco de dados em bancos de dados do SQL Server, banco de dados de SQL do Azure e Azure SQL DW da linha de comando.
- O [ferramenta DBFS](https://github.com/Microsoft/dbfs). Isso é uma ferramenta de código-fonte aberto que permite que os DBAs e administradores do sistema monitorar o SQL Server mais facilmente com a exposição de dados ao vivo de exibições de gerenciamento dinâmico (DMVs) do SQL Server como arquivos virtuais em um diretório virtual em sistemas operacionais Linux.
- Agora, o SQL Server Integration Services (SSIS) é executado no Linux. Além disso, há um novo pacote que lhe permite executar pacotes SSIS no Linux de linha de comando. Para obter mais informações, consulte o [anúncio de postagem de blog SSIS oferecem suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). Com o SSIS na atualização do Linux CTP 2.1, seus pacotes SSIS podem usar conexões ODBC no Linux. Para obter mais informações, consulte o [postagem do blog anunciar suporte a ODBC no Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

## <a name="ctp-20"></a>CTP 2.0

A versão CTP 2.0 contém as seguintes melhorias e correções:

- Adicionado **o envio de logs** funcionalidade do SQL Server Agent.
- Mensagens localizadas de conf mssql
- Formatação de caminho do Linux agora são compatíveis em todo o mecanismo do SQL Server. Mas o suporte para "c:\\" caminhos prefixados continuará.
- Habilitado DMV **sys.dm_os_file_exists**.
- Habilitado DMV **fn_trace_gettable**.
- Adicionado [modo de segurança rigorosa CLR](/sql/database-engine/configure-windows/clr-strict-security).
- Gráfico SQL.
- Recriações de índice Online reiniciável.
- Processamento de consulta adaptável.
- Adicionado codificação UTF-8 para arquivos do sistema, incluindo arquivos de log.
- Corrigido limitação de local de bancos de dados na memória. 
- Adicionar novo tipo de cluster `CLUSTER_TYPE = EXTERNAL` para configurar um grupo de disponibilidade para alta disponibilidade.
- Corrija o ouvinte do grupo de disponibilidade para roteamento somente leitura.
- Suporte de produção para os clientes do programa de adoção antecipada (EAP). Inscreva-se [aqui](http://aka.ms/eapsignup).

## <a name="ctp-14"></a>CTP 1.4

A versão CTP 1.4 contém os seguintes aprimoramentos e correções:

- Habilitada a [do SQL Server Agent](sql-server-linux-setup-sql-agent.md).
  - Funcionalidade de trabalhos do T-SQL habilitada.
- Bugs de fuso horário fixo:
  - Suporte de fuso horário para a Ásia/Calcutá.
  - Função GETDATE () Fixed.
- Rede assíncrona 0 melhorias:
  - Melhorias significativas de desempenho da carga de trabalho de OLTP na memória.
- Imagem do docker agora inclui utilitários de linha de comando do SQL Server. (sqlcmd bcp).
- Suporte Virtual Device Interface (VDI) habilitado para backups.
- Local de TempDB agora pode ser modificado após a instalação usando `ALTER DATABASE`.

## <a name="ctp-13"></a>CTP 1.3

A versão CTP 1.3 contém os seguintes aprimoramentos e correções:

- Habilitado [pesquisa de texto completo](sql-server-linux-setup-full-text-search.md) recurso.
- Ativado sempre [funcionalidade de grupos de disponibilidade](sql-server-linux-availability-group-overview.md) para alta disponibilidade.
- Funcionalidade adicional no **mssql conf**:
  - Primeira configuração de tempo usando **mssql conf**. Consulte o uso do mssql-conf no [guias de instalação](sql-server-linux-setup.md#platforms).
  - Habilitando grupos de disponibilidade. Consulte o [tópico de grupos de disponibilidade](sql-server-linux-availability-group-overview.md).
- Caminho fixo de Linux native oferece suporte para grupos de arquivos OLTP em memória.
- Funcionalidade DMV dm_os_host_info habilitado.

## <a name="ctp-12"></a>CTP 1.2

A versão CTP 1.2 contém os seguintes aprimoramentos e correções:

- Suporte para [SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md).
- Correções de bug para melhorias de mecanismo e a estabilidade do núcleo.
- Imagem do docker: 
  - Fixa [emitir #1](https://github.com/Microsoft/mssql-docker/issues/1) adicionando Python para a imagem.
  - Removido `/opt/mssql/data` como volume de padrão.
- Atualizado para .NET 4.6.2.

## <a name="ctp-11"></a>CTP 1.1

A versão CTP 1.1 contém as seguintes melhorias e correções:

- Suporte para Red Hat Enterprise Linux versão 7.3.
- Suporte para Ubuntu 16.10.
- Camada atualizada OS de Docker 16.04 Ubuntu.
- Correção de problemas de telemetria na imagem do Docker.
- Script de instalação do SQL Server fixa relacionado bugs.
- Desempenho aprimorado para módulos T-SQL compilados nativamente, incluindo:
  - **OPENJSON**, **FOR JSON**, **JSON** internos.
  - Colunas computadas (índices só são permitidos em colunas computadas persistentes, mas não em colunas computadas persistentes para tabelas na memória).
  - **CROSS APPLY** operações.
- Novos recursos de idioma:
  - Funções de cadeia de caracteres: **TRIM**, **CONCAT_WS**, **traduzir** e **STRING_AGG** com suporte para **WITHIN GROUP (ORDER BY)**.
  - **IMPORTAÇÃO em MASSA** agora dá suporte ao formato CSV e o armazenamento de BLOBs do Azure como fonte de arquivo.

No modo de compatibilidade 140:

- O desempenho de atualizações para índices columnstore não clusterizado no caso de melhor quando a linha está no repositório delta. Alterado de exclusão e inserção de operações de atualização. Também alterar a forma do plano usada em toda a restringir.
- Consultas de modo de lote agora oferecem suporte a "concessão da memória loops de comentários". Isso aumentará a simultaneidade e a taxa de transferência em sistemas que executam consultas repetidas que usam o modo de lote. Isso pode permitir que mais consultas sejam executadas em sistemas que estão bloqueando caso contrário, na memória antes de iniciar as consultas.
- Desempenho aprimorado de paralelismo de modo de lote ignorando plano trivial para planos de modo de lote permitir que os planos paralelos para serem selecionadas, em vez disso, em columnstores. 

[Aprimoramentos do Service Pack 1](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/) nesta versão do CTP1.1:
- Clonagem de CLR, Filestream/Filetable, objetos na memória e o repositório de consultas de banco de dados.
- **CRIAR** ou **ALTER** operadores para objetos de programação.
- Novo **dica USE** opção para fornecer dicas para o processador de consultas de consulta. Saiba mais aqui: [dicas de consulta](https://msdn.microsoft.com/en-us/library/ms181714.aspx).
- Conta de serviço do SQL agora pode identificar programaticamente habilitar bloquear páginas na memória e a inicialização instantânea de arquivo permissões.
- Suporte para a contagem de arquivos TempDB, tamanho do arquivo e as configurações de crescimento do arquivo.
- Diagnóstico estendido no showplan XML.
- Perfis de execução de consulta de operador de leve.
- Nova função de gerenciamento dinâmico **sys.dm_exec_query_statistics_xml**.
- Nova função de gerenciamento dinâmico para estatísticas incrementais.
- Removido com ruídos de memória relacionados a mensagens de log do errorlog.
- Diagnóstico de latência do AlwaysOn aprimorado.
- Limpa o controle de alterações Manual.
- **DROP TABLE** suporte para replicação.
- **BULK INSERT** em heaps com **automática TABLOCK** em TF 715.
- Paralelo **INSERT... Selecione** alterações para tabelas temporárias locais.

Saiba mais sobre essas correções de [descrição da versão do Service Pack 1](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/).

Muitos aprimoramentos do mecanismo de banco de dados se aplicam ao Windows e Linux. A única exceção seria para recursos do mecanismo de banco de dados que atualmente não há suporte para Linux. Para obter mais informações, consulte [Novidades no SQL Server 2017 (mecanismo de banco de dados)](https://msdn.microsoft.com/library/mt775028).

## <a name="see-also"></a>Consulte também

Para requisitos de instalação, áreas de recursos sem suporte e problemas conhecidos, consulte [notas de versão do SQL Server 2017 no Linux](sql-server-linux-release-notes.md).

