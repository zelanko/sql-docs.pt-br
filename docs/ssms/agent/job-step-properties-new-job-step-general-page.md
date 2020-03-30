---
title: Novas propriedades da etapa de trabalho (Página geral)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepgeneral.f1
ms.assetid: 8d1885ba-4386-4528-8f2b-68c16852720c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7c8c707e8a1916041b32a2509e54d6150ea8df9a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242218"
---
# <a name="job-step-properties---new-job-step-general-page"></a>Propriedades da etapa de trabalho – Nova etapa de trabalho (página Geral)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para ver e alterar as propriedades ou para definir uma nova etapa de trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
Para navegar até essa página, no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , expanda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, clique com o botão direito do mouse em **Trabalhos**, clique em **Novos Trabalhos**, selecione a página **Etapas** e clique em **Novo**. Você também pode navegar até essa página. Para isso, clique com o botão direito do mouse em um trabalho no Pesquisador de Objetos, clique em **Propriedades**, selecione a página **Etapas** e clique em **Novo**, **Inserir**ou **Editar**.  
  
## <a name="options"></a>Opções  
**Nome da etapa**  
Defina o nome da etapa de trabalho.  
  
**Tipo**  
Defina o subsistema usado pela etapa de trabalho. Dependendo do subsistema que você escolher as opções exibidas para definir a etapa de trabalho serão diferentes.  
  
**Executar como**  
Defina a conta proxy para a etapa de trabalho. Membros da função de servidor fixa sysadmin também podem especificar a **Conta de Serviço do SQL Agent**.  
  
**Backup de banco de dados**  
Defina o banco de dados no qual a etapa de trabalho é executada. Esta opção não está disponível para todos os tipos de etapas de trabalho.  
  
**Comando**  
Defina o comando executado pela etapa de trabalho.  
  
## <a name="options-for-transact-sql-job-steps"></a>Opções para etapas de trabalho Transact-SQL  
**Abrir**  
Carregue o comando de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado para a Área de Transferência.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
**Analisar**  
Verifique a sintaxe do comando.  
  
## <a name="options-for-activex-script-job-steps"></a>Opções para etapas de trabalho ActiveX Script  
  
> [!IMPORTANT]
> O subsistema de script do ActiveX será removido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em uma futura versão do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam.  
  
**VBScript**  
Especifique o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Basic Scripting Edition como a linguagem para a etapa de trabalho.  
  
**JScript**  
Especifique JScript como a linguagem para a etapa de trabalho.  
  
**Outros**  
Digite o nome da linguagem para etapas de trabalho escritas em outra linguagem de criação de scripts.  
  
**Abrir**  
Carregue o comando de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Opções para etapas de trabalho do sistema operacional (CmdExec)  
**Código de saída do processo de um comando bem sucedido**  
Digite o código de saída que o comando retorna para indicar sucesso.  
  
**Abrir**  
Carregue o comando de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-powershell-job-steps"></a>Opções para etapas de trabalho do PowerShell  
**Abrir**  
Carregue o script de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do script.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-replication-distributor-job-steps"></a>Opções para etapas de trabalho do Distribuidor de Replicação  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-replication-merge-job-steps"></a>Opções para etapas de trabalho de Mesclagem de Replicação  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Opções para etapas de trabalho do Replication Queue Reader  
**Backup de banco de dados**  
O banco de dados a ser usado para a etapa de trabalho.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-replication-snapshot-job-steps"></a>Opções para etapas de trabalho do instantâneo de replicação  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-replication-transaction-log-reader-job-steps"></a>Opções para etapas de trabalho do Leitor do Log de Transações da Replicação  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-sql-server-analysis-services-command-job-steps"></a>Opções para etapas de trabalho do comando do SQL Server Analysis Services  
**Servidor**  
Selecione o servidor onde a etapa de trabalho é executada.  
  
**Abrir**  
Carregue o comando de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-sql-server-analysis-services-query-job-steps"></a>Opções para etapas de trabalho da consulta do SQL Server Analysis Services  
**Servidor**  
Selecione o servidor onde a etapa de trabalho é executada.  
  
**Backup de banco de dados**  
O banco de dados a ser usado para a etapa de trabalho.  
  
**Abrir**  
Carregue o comando de um arquivo.  
  
**Selecionar tudo**  
Selecione o texto do comando.  
  
**Copy**  
Copie o texto selecionado.  
  
**Colar**  
Cole o conteúdo da área de transferência.  
  
## <a name="options-for-integration-services-package-execution-job-steps"></a>Opções para etapas de trabalho de execução de pacotes de Integration Services  
  
### <a name="general-tab"></a>Guia Geral  
Especifique onde o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis_md.md)]) está localizado e qual o método de autenticação a ser usado. As seguintes opções estão disponíveis quando você seleciona essa guia.  
  
**Origem do pacote**  
Especifique onde o pacote [!INCLUDE[ssIS](../../includes/ssis_md.md)] está armazenado. Escolha uma destas opções:  
  
-   **SQL Server**  
  
-   **Sistema de Arquivos**  
  
-   **Armazenamento de Pacotes SSIS**  
  
**Servidor**  
Digite o nome do servidor em que o pacote [!INCLUDE[ssIS](../../includes/ssis_md.md)] está armazenado. Essa opção só está disponível quando **SQL Server** ou **Repositório de Pacotes SSIS** está especificado para **Origem do Pacote**.  
  
**Usar Autenticação do Windows**  
Logons para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam a autenticação do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows.  
  
**Usar Autenticação do SQL Server**  
Logons para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se este método de autenticação for selecionado, digite o **Nome de usuário** e a **Senha**apropriados.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A autenticação é fornecida para fins de compatibilidade com versões anteriores. Para maior segurança, use a autenticação do Windows, se possível.  
  
**Pacote**  
Digite o local do pacote.  
  
> [!IMPORTANT]  
> Para pacotes [!INCLUDE[ssIS](../../includes/ssis_md.md)] protegidos por senha, clique na guia **Configurações** para digitar a senha na caixa de diálogo **Senha do Pacote** . Caso contrário, o trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executa o pacote protegido por senha falhará.  
  
### <a name="configurations-tab"></a>Guia Configurações  
Especifique as opções de configuração para o pacote [!INCLUDE[ssIS](../../includes/ssis_md.md)] . As seguintes opções estão disponíveis quando essa guia é selecionada.  
  
**Arquivos de configuração**  
Lista os arquivos de configuração para o pacote.  
  
**Adicionar**  
Adicione um arquivo de configuração para o pacote.  
  
**Remover**  
Remova um arquivo de configuração para o pacote.  
  
**Mover para Cima**  
Mova para cima o arquivo de configuração selecionado.  
  
**Mover para Baixo**  
Mova para baixo o arquivo de configuração selecionado.  
  
### <a name="command-files-tab"></a>Guia Arquivos de Comando  
Selecione os arquivos de comando para o pacote. Os arquivos de comando são processados na ordem em que aparecem na lista. As seguintes opções estão disponíveis quando você seleciona essa guia.  
  
**Arquivos de comando**  
Lista os arquivos de comando para o pacote.  
  
**Adicionar**  
Adicione um arquivo de comando.  
  
**Remover**  
Remova o arquivo de comando selecionado.  
  
**Mover para Cima**  
Mova para cima o arquivo de comando selecionado.  
  
**Mover para Baixo**  
Mova para baixo o arquivo de comando selecionado.  
  
### <a name="data-sources-tab"></a>Guia Fontes de Dados  
Esta guia exibe as fontes de dados especificadas no pacote.  
  
**Gerenciador de Conexões**  
Exibe o nome da fonte de dados.  
  
**Descrição**  
Exiba a descrição da fonte de dados.  
  
**Cadeia de Conexão**  
Exiba a cadeia de conexão para a fonte de dados.  
  
### <a name="execution-options-tab"></a>Guia Opções de Execução  
Exiba ou altere as opções de execução para o pacote nesta guia.  
  
**Falha de pacote com avisos de validação**  
Selecione essa opção para que a execução do pacote falhe se ocorrerem avisos de validação.  
  
**Validar pacote sem executar**  
Selecione esta opção para que a etapa de trabalho valide, mas não execute, o pacote.  
  
**Executáveis máximos simultâneos**  
Número máximo de arquivos executáveis que podem ser executados ao mesmo tempo.  
  
**Ativar pontos de verificação do pacote**  
Selecione esta opção para que a etapa de trabalho use pontos de verificação do pacote.  
  
**Arquivo de ponto de verificação**  
Digite o nome do arquivo do ponto de verificação do pacote.  
  
**...**  
Procure para localizar o arquivo do ponto de verificação do pacote.  
  
**Substituir opções de reinicialização**  
Selecione esta opção para especificar opções de reinício para essa etapa de trabalho que sejam diferentes das opções de reinício especificadas no pacote.  
  
**Opção de reinicialização**  
Selecione a ação a ser tomada quando o pacote reiniciar.  
  
### <a name="logging-tab"></a>Guia Log  
Exiba ou altere as opções de provedores de log para o pacote nesta guia.  
  
**Provedor de Log**  
Selecione o ClassID para o provedor de log.  
  
**Cadeia de Caracteres de Configuração**  
Digite a cadeia de caracteres de configuração para o provedor de log.  
  
**Remover**  
Remova o provedor de log.  
  
### <a name="set-values-tab"></a>Guia Definir Valores  
Exiba ou altere os valores de propriedade para o pacote nesta guia.  
  
**Caminho da propriedade**  
Exiba ou altere o caminho para a propriedade.  
  
**Valor**  
Exiba ou altere o valor para a propriedade.  
  
**Remover**  
Remova a propriedade.  
  
### <a name="verification-tab"></a>Guia Verificação  
Selecione as opções de verificação para a etapa de trabalho nesta guia.  
  
**Executar apenas pacotes assinados**  
Execute apenas pacotes que tenham sido assinados. Quando esta opção está selecionada, a etapa de trabalho apresentará falha se o pacote não estiver assinado.  
  
**Verificar construção de pacote**  
Execute apenas pacotes com um número de construção específico. Quando esta opção está selecionada, a etapa de trabalho apresentará falha se o pacote não tiver o número de construção especificado.  
  
**Compilar**  
Digite o número de construção do pacote.  
  
**Verificar ID do pacote**  
Execute apenas pacotes com um ID específico. Quando esta opção está selecionada, a etapa de trabalho apresentará falha se o pacote não tiver o ID especificado.  
  
**ID do Pacote**  
Digite o ID do pacote.  
  
**Verificar ID da versão**  
Execute apenas pacotes com uma ID de versão específica. Quando esta opção está selecionada, a etapa de trabalho apresentará falha se o pacote não tiver a ID da versão especificada.  
  
**ID da Versão**  
Digite o ID da versão.  
  
### <a name="command-line-tab"></a>Guia Linha de Comando  
Especifique as opções de linha de comando para o pacote. As seguintes opções estão disponíveis quando essa guia é selecionada.  
  
**Restaurar as opções originais**  
Use o conjunto de opções de linha de comando nesta caixa de diálogo.  
  
**Editar a linha de comando manualmente**  
Especifique opções na janela de linha de comando.  
  
**Linha de comando**  
Digite as opções de linha de comando a usar para o pacote.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)  
[Trabalhos do SQL Server Agent para pacotes](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)  
[Administrando agentes de replicação](../../relational-databases/replication/agents/replication-agent-administration.md)  
  
