---
title: "SQL Server Management Studio – Changelog (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2144751277bb10897e0ed39ee24dbad8a32b4ce
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-1653-release"></a>Versão do SSMS 16.5.3
Disponibilidade geral | Número de build: 13.0.16106.4

Os seguintes problemas foram corrigidos nesta versão:

* Corrigido um problema introduzido no SSMS 16.5.2 que estava causando a expansão do nó 'Table' quando a tabela tinha mais de uma coluna esparsa.

* Os usuários podem implantar pacotes do SSIS contendo o Gerenciador de Conexões do OData, que se conectam a um recurso do Microsoft Dynamics AX/CRM Online para o catálogo do SSIS. Para obter mais informações, consulte [Gerenciador de Conexões do OData](https://msdn.microsoft.com/library/dn584133.aspx).

* Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [ID de Conexão 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [ID de Conexão 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [ID de Conexão 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.

* O menu *Abrir recente* não mostra arquivos salvos recentemente. [ID de Conexão 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* O SSMS está lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota (Internet)). [ID de Conexão 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Corrigido um problema com a barra de rolagem do Designer do SQL. [ID de Conexão 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* O menu de contexto para tabelas trava momentaneamente 
 
* Ocasionalmente, o SSMS lança exceções no Monitor de Atividade e falha. [ID de Conexão 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* O SSMS 2016 falha com o erro "O processo foi terminado devido a um erro interno no Tempo de Execução do .NET no IP 71AF8579 (71AE0000) com código de saída 80131506"


## <a name="ssms-1651-release"></a>Versão do SSMS 16.5.1
Disponibilidade geral | Número de build: 13.0.16100.1

* Corrigido um problema em que Invoke-Sqlcmd erroneamente insere várias linhas quando ocorre a restrição check. [Item do Microsoft Connect: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Corrigido um problema em que as versões de idioma de não ENU não funcionam completamente durante a criação de grupos de disponibilidade.

* Corrigido um problema em que o plano de consulta XML não abre a interface do usuário de SSMS adequada.


## <a name="ssms-165-release"></a>Versão do SSMS 16.5
Disponibilidade geral | Número de build: 13.0.16000.28

* Corrigido um problema em que uma falha pode ocorrer quando um banco de dados com o nome da tabela que contém ";:" foi clicado.
* Corrigido um problema em que as alterações feitas na página de modelo na janela Propriedades do Banco de Dados Tabulares AS utilizariam scripts da definição original. 
[Item nº 3080744 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* Corrigido o problema em que os arquivos temporários são adicionados à lista de "Arquivos recentes".  
[Item nº 2558789 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* Corrigido o problema em que o item de menu "Gerenciar compactação" é desabilitado para os nós de tabela de usuário na árvore do Gerenciador de objetos.  
[Item nº 3104616 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* Corrigido o problema que usuário não é capaz de definir o tamanho da fonte para o Pesquisador de objetos, Gerenciador de servidores registrados, Gerenciador de modelos, bem como detalhes do Pesquisador de objetos. Fonte para os pesquisadores estarão usando a fonte de Ambiente.  
[Item nº 691432 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* Corrigido o problema em que o SSMS sempre se reconecta ao banco de dados padrão quando a conexão é perdida.  
[Item nº 3102337 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* Corrigido muitos dos problemas de DPI alta na janela do Gerenciador de Política e Editor de Consulta, incluindo os ícones de plano de execução.

* Corrigido o problema em que a opção de configuração de fonte e cor para Eventos Estendidos está ausente.

* Corrigido o problema de falhas do SSMS que ocorrem no fechamento do aplicativo ou quando está tentando mostrar a caixa de diálogo de erro.


## <a name="ssms-1641-september-2016-release"></a>Versão SSMS 16.4.1 (setembro 2016)
Disponibilidade geral | Número de versão: 13.0.15900.1

*  Foi corrigido um problema no qual ocorria falha durante a tentativa de ALTERAR/Modificar um procedimento armazenado:  
[Item nº 3103831 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* Novos 'Read-SqlTableData', 'Read-SqlViewData' e ‘Write-SqlTableData' para exibir e gravar dados usando o PowerShell.  
[Cartão Read-SqlTableData do Trello](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Item nº 2685363 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* Novo cmdlet 'Add-SqlLogin' para habilitar novos cenários de gerenciamento de logon usando o PowerShell.  
[Item nº 2588952 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  Suporte aprimorado e facilidade de uso para os usuários se conectarem a várias nuvens nacionais.
    
    
*  Corrigido um problema em que uma exceção de memória insuficiente estava sendo lançada.  
[Item nº 3062914 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Item nº 3074856 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  Corrigido um problema em que a filtragem por esquema não é uma opção de filtro válida.  
[Item nº 3058105 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Item nº 3101136 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  Corrigido um problema em que a janela do Monitor de um banco de dados ampliado não estaria acessível.
    
*  Corrigido um problema em que a Ajuda F1 sempre abria conteúdo online. Os usuários agora podem selecionar se preferem ajuda online ou offline por meio do "Definir Preferência de Ajuda" no menu Ajuda.   
[Item nº 2826366 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  Corrigido um problema em que um modelo de tabela do Analysis Services de nível 1200 não remove a senha para script, mesmo que a versão do servidor mostre [objeto de modelo do cliente está agora em sincronização antes de criar scripts].
    
*  Corrigido um problema no qual a opção 'SELECIONAR N LINHAS SUPERIORES' gerava uma sintaxe preterido para o operador TOP.  
[Item nº 3065435 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  Diversos problemas de layout corrigidos em todo o SSMS, incluindo a página Propriedades de Logon e Opções Avançadas de Execução de Consulta.   
[Item nº 3058199 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Item nº 3079122 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Item nº 3071384 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  Corrigido um problema em que uma solução foi criada automaticamente sempre que um usuário abre uma nova janela de consulta.   
[Item nº 2924667 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Item nº 2917742 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Item nº 2612635 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  Corrigido um problema em que tabelas de tempo não puderam ser expandidas no Pesquisador de Objetos quando estiverem em banco de dados do sistema.  
[Item nº2551649 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  Corrigido um problema em que o SSMS executa uma consulta para SELECT @@trancount depois de executar um lote.    
[Item nº 3042364 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  Corrigido um problema no Analysis Services no qual a criação de um script na página de propriedades de um servidor resultava em uma caixa de diálogo de conexão oculta.
    
*  Corrigido um problema em que Ctrl + Q não seleciona a barra de ferramentas Início Rápido.
    
*  Corrigido um problema em que alterar o MaxSize de um banco de dados usando a caixa de diálogo Propriedades do Servidor foi interrompida para bancos de dados com menos de 2 TB.  
[Item do Microsoft Connect nº1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Corrigido um problema em que o Assistente de Restauração do Banco de Dados não aceita nomes de arquivos com espaços em branco à esquerda:   
[Item do Microsoft Connect nº2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>Versão 16.3 do SSMS (agosto de 2016)
Disponibilidade geral | Número de versão: 13.0.15700.28

* Versões mensais do SSMS agora são sinalizadas numericamente.

* [Nova opção de autenticação **'Autenticação Universal do Active Directory'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Esse é um mecanismo de autenticação baseada em token orientado pelo Azure Active Directory que dá suporte a mecanismos de autenticação multifator, de senha e integrada.

* Novos modelos de eventos estendidos correspondentes à funcionalidade dos modelos do SQL Server Profiler [(Item nº 2543925 do Microsoft Connect)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool). Saiba mais sobre os [modelos do SQL Server Profiler](https://msdn.microsoft.com/library/ms190176.aspx)incluídos.

* Novas caixas de diálogo Criar banco de dados e Propriedades de banco de dados para bancos de dados do Azure SQL.

* Cmdlets 'Get-SqlLogin' e 'Remove-SqlLogin' para ajudar a executar o gerenciamento de logon do SQL Server usando o PowerShell.  
*Solicitações vinculadas de bugs dos clientes:*   
[Item do Microsoft Connect nº2588952.](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* Novo cmdlet do PowerShell 'New-SqlColumnMasterKeySettings' que adiciona suporte para a criação de chaves mestras de coluna para provedores arbitrários e caminhos de chaves.

* Nova caixa de diálogo 'Criar banco de dados' para simplificar a criação de bancos de dados do SQL Azure no SSMS>

* Suporte para filtragem no nó 'Databases' do Pesquisador de Objetos do SSMS. Navegue até o nó 'Databases' no Pesquisador de objetos e clique no ícone de filtro na barra de ferramentas do Pesquisador de objetos para filtrar a lista de bancos de dados.

* Suporte para contas de armazenamento do tipo ARM (Azure Resource Manager) nos assistentes de Backup e Restauração.

* [Suporte beta inicial para monitores de alta resolução](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/).  
*Solicitações vinculadas de bugs dos clientes:*   
[Item nº do 1129301 Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display), [Item nº 1858763 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1858763/), [Item nº 1852671 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1852671/), [Item nº 1487643 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1487643/),  [Item nº 1355641 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1355641/), [Item nº 2161595 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2161595/), [Item nº 1854041 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1854041/), [Item nº 1055617 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1055617/), [Item nº 2448774 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2448774/), [Item nº 1521405 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1521405/), [Item nº 2117853 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2117853/), [Item nº 2014256 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2014256/), [Item nº 2162218 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2162218/), [Item nº 2344551 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2344551/), [Item nº 1664436 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1664436/), [Item nº 2554043 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2554043/), [Item nº 2983216 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2983216/), [Item nº 2021706 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* Melhorias no DTA (Orientador de Otimização do Mecanismo de Banco de Dados) para dar suporte à leitura automática de uma carga de trabalho do Repositório de Consultas do SQL Server.

* Melhorias no DTA (Orientador de Otimização do Mecanismo de Banco de Dados) para exibir recomendações de índice para índices columnstore clusterizados, índices columnstore não clusterizados e índices rowstore.

* Suporte para enviar comandos do DBCC (Database Console) usando cmdlets do PowerShell do SQL Server Analysis Services.

* Correção de bug para exibir texto não criptografado de colunas de LOB (Objeto Grande) AlwaysEncrypted descriptografadas no SSMS.  
*Solicitações vinculadas de bugs dos clientes:*   
[Item do Microsoft Connect nº2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* Correção de bug na caixa de diálogo Always Encrypted para corrigir falhas quando estilos visuais do Windows não estão habilitados (por exemplo, habilitando a exibição de alto contraste).

* Correção de bug para o erro 'Método não encontrado' que impede a conexão com instâncias do SQL Server.

* Correção de bug para a falha do SSMS ao criar uma função de partição com deslocamento de data e hora.

* Correção de bug para adicionar ou remover o requisito do Microsoft .NET 3.5 para iniciar a ferramenta de administração do Distributed Replay (DReplay.exe).

* Correção de bug no assistente de Implantação do Analysis Services para dar suporte a nomes de servidor totalmente qualificados.

* Correção de bug no SSMS para exibir as partições em modelos de tabela do Analysis Services com um modelo de compatibilidade de 2016.  
*Solicitações vinculadas de bugs dos clientes:*   
[Item do Microsoft Connect nº2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Melhorias de desempenho e correções de bugs nos modelos de tabela do Analysis Services e SMO (Objetos Compartilhados de Gerenciamento) do SQL Server. 


---
## <a name="ssms-july-2016-hotfix-update-release"></a>Versão de atualização do hotfix de julho de 2016 do SSMS 
Disponibilidade geral | Número de versão: 13.0.15600.2

* **Correção de bug no SSMS para habilitar os itens de menu de atalho ausentes**.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item do Microsoft Connect nº2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Item do Microsoft Connect nº2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Item do Microsoft Connect nº2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>Versão de julho de 2016 do SSMS 
Disponibilidade geral | Número de versão: 13.0.15500.91

* *Edição, 5 de julho:* **suporte aprimorado para bancos de dados de tabela do SQL Server 2016 (nível de compatibilidade 1200) no diálogo Processo do Analysis Services e no assistente de Implantação do Analysis Services.**

* *Edição, 5 de julho:* **nova opção no diálogo 'opções de execução de consulta' no SSMS para definir 'XACT_ABORT'. Essa opção é habilitada por padrão nessa versão do SSMS e instrui o SQL Server a reverter a transação inteira e anular o lote se ocorrer um erro em tempo de execução.**

* **Suporte para SQL Azure Data Warehouse no SSMS.**

* **Atualizações importantes para o módulo PowerShell do SQL Server. Isso inclui um novo [módulo SQL PowerShell e novos CMDLETs para Sempre Criptografados, SQL Agent e Logs de Erros do SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**.

* **Suporte para a geração de script do PowerShell no assistente Always Encrypted**.

* **Tempos de conexão significativamente aprimorados para bancos de dados do SQL Azure.**

* **Novo diálogo 'Backup para URL' para dar suporte à criação de credenciais de armazenamento do Azure para backups de banco de dados do SQL Server 2016. Isso fornece uma experiência mais simplificada para armazenar os backups de banco de dados em uma conta de armazenamento do Azure.**
 
* **Diálogo Nova Restauração para simplificar a restauração de um backup de banco de dados do SQL Server 2016 do serviço de armazenamento do Microsoft Azure.**
 
* **Correção de bug no designer de consulta do SSMS para permitir a adição de tabelas ao designer se um usuário não tiver permissões SELECT.**

* **Correção de bug para adicionar suporte do IntelliSense para as funções 'TRY_CAST()' e 'TRY_CONVERT()'.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2453461 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* **Correção de bug no módulo do PowerShell para habilitar o carregamento da extensão 'SQLAS' do Analysis Services.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2544902 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* **Correção de bug na janela do editor SSMS para permitir as ações do tipo "arrastar e soltar" de abertura para arquivos do Sql.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2690658 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* **Correção de bug no criador de perfil para corrigir falhas de criador de perfil ao sair.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2616550 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Item nº 2319968 do Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* **Correção de bug no SSMS para evitar falha ao tentar editar um link de associação no designer de tabela SSMS.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2721052 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* **Correção de bug no SSMS para habilitar a geração de script de banco de dados para membros da função db_owner.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2869241 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* **Correção de bug no editor do SSMS para remover o atraso no fechamento de uma guia de consulta se o servidor ficar offline.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2656058 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* **Correção de bug para habilitar a opção de Backup em bancos de dados SQL Server Express.**  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2801910 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Item nº 2874434 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* **Correção de bug no Analysis Services para mostrar corretamente o provedor de Feed de Dados para modelos multidimensionais do Analysis Services.**

----
## <a name="ssms-june-2016-generally-available-release"></a>Versão com disponibilidade pública do SSMS de junho de 2016
Disponibilidade geral | Número de versão: 13.0.15000.23

* **O SSMS tem disponibilidade geral a partir da versão de junho de 2016.**

* **Nova caixa de diálogo de localização rápida no SSMS integrada de forma melhor ao documento atual e que permite pesquisar por meio de expressões regulares.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **Aprimoramentos no instalador do SSMS para que você possa acompanhar o progresso da instalação e processas códigos de saída para instalações autônomas por meio de scripts.**

* **Correção de bug na ajuda F1 contextual do SSMS para exibir corretamente artigos e documentos de ajuda.**

* **Correção de bug no modo de exibição de 'Consultas Retornadas' do Armazenamento de Dados de Consulta que causou a falha do SSMS durante a rolagem.** 

* **Correção de bug no conector OLEDB do Excel Analysis Services para permitir conexões do Excel 2016 ao SQL Server Analysis Services.**

* **Correção de bug na caixa de diálogo de conexão do SSMS para mostrar a caixa de diálogo de conexão no mesmo monitor que a janela principal do SSMS em sistemas de vários monitores.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Correções de bugs na experiência do Always Encrypted. Foi corrigido um bug em que a opção de menu Always Encrypted não era habilitada corretamente para Stretch Databases. Também foi corrigido um bug no assistente do Always Encrypted em que ele não usava corretamente o provedor HSM da SafeNet (Luna SA).**

---
## <a name="ssms-april-2016-preview"></a>Visualização de abril de 2016 do SSMS 
Número de versão: 13.0.14000.36
  
* **Melhoria do instalador do SSMS para adicionar mensagens de erro legíveis.**  
  
* **Melhoria no Assistente de banco de dados de alongamento para adicionar suporte a predicados**.  
  
* **Melhoria no commandlet do AlwaysEncrypted Powershell para adicionar APIs de chave de criptografia**.  
  
* **Correção de bug para desligar o IntelliSense na barra de ferramentas do SSMS se ele tiver sido desabilitado em Ferramentas, caixa de diálogo Opções.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **Melhorias e correções de bugs na interface do usuário de comparação de Planos de execução para reduzir o espaçamento usado por planos de consulta longa**.  
  
* **Correções de bugs no SSMS para corrigir problemas que causavam falha do SSMS ao sair**.   
  
* **Correções de bugs no assistente Always Encrypted para manter permissões de usuário durante a criptografia e permitir que o banco de dados desanexe operações após a conclusão do assistente**.  
  
* **Correção de bug na caixa de diálogo Nova Chave Mestra de Coluna do Always Encrypted para fornecer comentários sobre a tentativa de gerar uma chave usando um provedor de CNG (Algoritmo de Criptografia) sem suporte.**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>Atualização da Visualização de março de 2016 do SSMS
Número de versão: 13.0.13000.55
  
* **Agora, o SSMS utiliza o Shell Isolado do Visual Studio 2015.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **Novas ferramentas de início rápido que ajudam a localizar rapidamente itens de menu e opções. (Shell isolado do VS 2015)**  
  
* **Melhorias nas opções de temas do SSMS para adicionar suporte a um tema claro do SSMS. (Shell isolado do VS 2015)**  
  
* **Correção de bug na opção de menu Ferramentas do SSMS para redefinir corretamente atalhos de consulta se o botão "Redefinir para Padrão" for pressionado.**  
  
* **Correção de bug em novos modelos de projeto do SSMS para exibir nomes de modelo facilmente legíveis.**  
  
* **Foi resolvido um erro de exibição do histórico de trabalhos do SQL Agent no SSMS.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **Correção de bug para permitir a instalação offline do SSMS. Isso permite que você instale sem a necessidade de uma conexão com a Internet. (Shell isolado do VS 2015)**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **Correção de bug para manter o diretório atual do usuário quando o módulo do PowerShell SQLPS (SQL Server) for importado.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **Correção de bug no módulo do SQLPS (SQL Server PowerShell) para usar os verbos do PowerShell aprovados.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **Correção de bug no módulo do SQLPS (SQL Server Powershell) para carregar o módulo mais rápido.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **Correção de bug nas Etapas de Trabalho do SQL Agent para permitir a modificação de uma etapa de trabalho.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **Correção de bug no Pesquisador de Objetos do SSMS para listar as tabelas em ordem alfabética.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **Correção de bug na lista suspensa de 'bancos de dados disponíveis' para mostrar a lista precisa dos nomes de banco de dados quando uma conexão do SQL Server é alterada.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **Correção de bug nos atalhos de teclado do SSMS para mover o foco para a lista suspensa 'bancos de dados disponíveis' se 'CTRL+U' for pressionado**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>Visualização de março de 2016 do SSMS 
Número de versão: 13.0.12500.29 
  
* **Melhoria no instalador da Web do SSMS para permitir a navegação usando teclas do teclado.**  
  
* **Melhoria no Assistente AlwaysEncrypted para dar suporte a tipos de dados de alias para criptografia.**  
  
* **Correção de bug no assistente de 'Novo Grupo de Disponibilidade' AlwaysOn para exibir o número máximo correto de destinos de failover automático.**  
*Solicitações vinculadas de bugs dos clientes:* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **Correção de bug no instalador da Web do SSMS para corrigir erros que afetam a instalação.**  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **Correção de bug na versão de visualização do SSMS para habilitar o salvamento de planos de manutenção no SQL Server 2012 e anterior.**  
      
* **Correções de bugs no Assistente de Backup para permitir vários nomes de backup personalizados para backups distribuídos e para exibir o nome do arquivo de backup apropriado se um novo nome for inserido após uma credencial de armazenamento ser selecionada.**  
  
---  
## <a name="ssms-february-2016-preview"></a>Visualização de fevereiro de 2016 do SSMS 
Número de versão: 13.0.12000.65
  
* **Melhoria no Monitor de atividade para exibir opções de texto quando configurações de alto contraste estão habilitadas no SSMS.**  
  
* **Melhoria na caixa de diálogo do assistente Always Encrypted para exibir um aviso se o agrupamento de uma coluna for alterado durante o processo de criptografia.**  
  
* **Melhoria no gerenciamento de políticas para adicionar suporte à criação de condições em Chaves de Criptografia de Coluna, Coluna de Valores de Chave de Criptografia e Chaves Mestras de Coluna.**  
  
* **Correção de bug para melhorar a usabilidade da caixa de diálogo de limpeza de chave mestra do Always Encrypted e mensagens de erro do Always Encrypted.**  
  
* **Correção de bug para desabilitar a rotação de chave mestra de coluna Always Encrypted se existir apenas uma chave.**  
  
* **Correção de bug para o erro de 'inicializador de tipo' que ocorre se a caixa de diálogo Always Encrypted é iniciada usando a versão de janeiro do SSMS ou a versão do SSMS fornecida com a mídia do SQL Server RC0.**  
  
---  
## <a name="ssms-january-2016-preview"></a>Visualização de janeiro de 2016 do SSMS 
Número de versão: 13.0.11000.78 
  
* **Correção de bug no SSMS para permitir a exclusão de sessões de Eventos Estendidos (XEvent).**  
  
* **Correção de bug para abrir a caixa de diálogo de propriedades de um grupo de disponibilidade do SQL Server 2014.**  
 *Solicitações vinculadas de bugs dos clientes:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **Correção de bug para habilitar a capacidade de adicionar uma réplica do Azure a um grupo de disponibilidade.**  
 *Solicitações vinculadas de bugs dos clientes:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **Correção de bug para abrir a caixa de diálogo de propriedades de bancos de dados do SQL Server 2014.**  
 *Solicitações vinculadas de bugs dos clientes:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Correção de bug para remover colunas duplicadas que aparecem para cada tabela quando conectada a um Banco de Dados SQL do Microsoft Azure.**  
 *Solicitações vinculadas de bugs dos clientes:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>Visualização de dezembro de 2015 do SSMS 
Número de versão: 13.0.900.73
  
* **Aperfeiçoamentos de comparação do plano de execução para habilitar a comparação do plano de execução da consulta atual com um salvo em um arquivo.**  
  
* **Suporte aprimorado do IntelliSense para índices de columnstore embutido no SSMS.**  
  
* **Correção de bug no Assistente da sessão de Eventos Estendidos para habilitar a seleção de modelos quando conectado a um servidor V12 do Azure.**  
  
* **Novas paradas de tabulação nas caixas de diálogo "Criar Auditoria" e "Novo Logon" na pasta de segurança para permitir a navegação de teclado mais fácil.**  
  
* **Correção de bug para habilitar a funcionalidade "Mudar para a guia resultados após a execução da consulta" se o SSMS estiver definido para exibir resultados em formato de grade.**   
 *Solicitações vinculadas de bugs dos clientes:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **Correção de bug para exibir cabeçalhos de coluna não truncados se o SSMS estiver definido para exibir resultados em formato de grade.**  
 *Solicitações vinculadas de bugs dos clientes:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **Correções de bugs para permitir a instalação correta do instalador do SSMS da web.**  
 *Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>Visualização de novembro de 2015 do SSMS
Número de versão: 13.0.800.111
  
* **Suporte a ajuste de bitmap para vídeos com alto DPI no SSMS.**  
  
* **Aperfeiçoamentos na interface de usuário de assistentes e caixas de diálogo AlwaysEncrypted para simplificar o processo de criação de chaves de criptografia de banco de dados.**  
  
* **Nova opção de menu de contexto que se clica com o botão direito do mouse na lista “Processos” no monitor Atividade para exibir Estatísticas de Consulta ao vivo.**  
  
* **Correção de bug para habilitar a desinstalação adequada das versões de visualização do SSMS em computadores cliente.**  
  *Solicitações vinculadas de bugs dos clientes:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **Correção de bug para permitir a edição das etapas de trabalho no Agente de Trabalho do SQL mesmo quando um arquivo estiver ausente**.  
  *Solicitações vinculadas de bugs dos clientes:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **Correção de bug na opção de menu "Exibir dados de destino" para uma sessão de eventos estendidos em um banco de dados em execução em uma máquina virtual do Azure.**  
  *Solicitações vinculadas de bugs dos clientes*:  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>Visualização de outubro de 2015 do SSMS 
Número de versão: 13.0.700.242  
* **Novo instalador da Web leve e modernizado que simplifica o download do SSMS e o processo de instalação.**  
  
* **Novo assistente de criptografia da coluna Always Encrypted que permite criptografia e descriptografia das colunas selecionadas do lado do cliente.**  
  
* **Nova caixa de diálogo de rotação de chave mestra de coluna (CMK) para bancos de dados Always Encrypted que simplifica o processo de rotação de chaves de criptografia para manter a segurança dos dados.**  
  
* **Novo monitoramento de banco de dados ampliado que permite solucionar problemas e monitorar o status da migração de dados para a nuvem do Azure.**  
  
* **Melhorias ao assistente de banco de dados ampliado para dar suporte à escolha de um servidor do Microsoft Azure que não consta na assinatura padrão do Microsoft Azure.**  
  *Solicitações vinculadas de bugs dos clientes:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **Correção de bug para permitir a exibição correta do plano de execução ao vivo no SSMS.**  
  *Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **Correção de bug para remover opções inválidas nos scripts de SSMS dos instantâneos dos bancos de dados**  
  *Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **Correção de bug na interface do usuário do armazenamento de dados de consulta para mostrar os detalhes no painel "Consultas de Consumo de Recurso Superior".**  
  *Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>Visualização de setembro de 2015 do SSMS 
Número de versão: 13.0.600.65  
* **Nova caixa de diálogo de regra de firewall que simplifica o processo de conexão a um banco de dados SQL do Azure.**      
    
* **Caixa de diálogo "Novo índice" atualizada que permite a criação de índices rowstore não clusterizados, mesmo quando houver um índice columnstore clusterizado. Essa funcionalidade está disponível para o SQL 2016 e outros programas.**      
  *Solicitações vinculadas de bugs dos clientes:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **Correção de bug para permitir a exibição e edição de trabalho do SQL Agent em versões de visualização do SSMS em execução no Windows 7.**      
  *Solicitações vinculadas de bugs dos clientes:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **Correção de bug para exibir nós do gatilho no SSMS para SQL Server 2014 e versões posteriores.**      
  *Solicitações vinculadas de bugs dos clientes:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **Correções de bugs no banco de dados e interface do usuário de relatórios padrão do servidor para excluir informações de versão do cabeçalho.**      
  *Solicitações vinculadas de bugs dos clientes:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **Correção de bug para evitar que o nó de estatísticas de consulta ao vivo seja exibido como concluído quando não estiver concluído.**      
  *Solicitações vinculadas de bugs dos clientes:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>Visualização de agosto de 2015 do SSMS 
Número de versão: 13.0.500.53
  
* **Atualizações ao Pesquisador de Objetos para reduzir o atraso no carregamento quando houver muitos bancos de dados.**  
  
* **Melhorias para a instalação do SSMS em computadores com Windows 10.**  
  
* **Correções de bugs e atualizações para o SQL Server Configuration Manager e a interface do usuário de relatórios do SSMS**    
***  
  
## <a name="ssms-july-2015-preview"></a>Visualização de julho de 2015 do SSMS
Número de versão: 13.0.400.91
  
* **Diagramas de banco de dados para o Banco de Dados SQL do Azure (V12).**  
  
* **Suporte aprimorado ao IntelliSense para a nova sintaxe de tabela temporal.**  
  
* **Biblioteca DacFx atualizada para dar suporte aos mais recentes recursos de bancos de dados SQL do Azure, incluindo segurança em nível de linha e autenticação do Azure Active Directory.**  
  
* **Correções de bugs (interface do usuário de verificação de atualizações atualizada, correção da interface do usuário na lista de nível de compatibilidade e muito mais).**  
***  
  
## <a name="ssms-june-2015-preview"></a>Visualização de junho de 2015 do SSMS 
Número de versão: 13.0.300.44
  
* **Novo instalador da Web leve do SSMS.**  
  
* **Verificação automática de atualizações.**  
  
* **O SSMS agora dá suporte à pesquisa de texto completo para o banco de dados SQL do Azure (V12).**  
  
* **Principais solicitações dos clientes abordadas:**  
  * Edição das 200 linhas habilitada para tabelas e exibições no Pesquisador de Objetos.  
  * Designer de tabela habilitado para o banco de dados SQL do Azure (V12).  
  * Caixas de diálogo de propriedades de bancos de dados e tabelas habilitadas para o banco de dados SQL do Azure (V12).  
    
 * **Nova opção para ignorar o prompt para salvar arquivos T-SQL.**  
   
 * **Suporte ao assistente de importação/exportação para novas camadas de serviço do banco de dados SQL do Azure (Basic, Standard e Premium).**  
   
 * **Diversas correções de bugs (cenários de script, o que permite alterar o acompanhamento de bancos de dados SQL e muito mais).**   
     
  
  
  
  
  
  
    

