---
title: "SQL Server Management Studio – Changelog (SSMS) | Microsoft Docs"
ms.custom: 
ms.date: 12/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 051c080de8a5b670a7fe3dbe70ccebf73bfb57a3
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2018
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Este artigo fornece detalhes sobre atualizações, aprimoramentos e correções de bug para as versões atuais e anteriores do SSMS. Baixe [versões anteriores do SSMS abaixo](#previous-ssms-releases).


## <a name="ssms-174download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.4](download-sql-server-management-studio-ssms.md)
Geralmente disponível| Número de build: 14.0.17213.0

### <a name="whats-new"></a>Novidades

**SSMS geral**

Avaliação de Vulnerabilidades:
- Adicionado um novo serviço de Avaliação de Vulnerabilidade de SQL para verificar seus bancos de dados para possíveis vulnerabilidades e desvios das práticas recomendadas, como configurações incorretas, excesso de permissões e dados confidenciais expostos. 
- Os resultados da avaliação incluem etapas práticas para resolver cada problema e scripts de correções personalizadas quando aplicável. O relatório de avaliação pode ser personalizado para cada ambiente e ajustado de acordo com requisitos específicos. Saiba mais em [Avaliação de Vulnerabilidades SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Correção do problema no qual *HasMemoryOptimizedObjects* gerava exceção no Azure.
- Adicionado suporte para o novo recurso CATALOG_COLLATION.

Painel AlwaysOn:
- Melhorias para análise de latência em Grupos de disponibilidade.
- Adicionados dois novos relatórios: *AlwaysOn\_Latency\_Primary* e *AlwaysOn\_Latency\_Secondary*.

Plano de execução:
- Links atualizados para apontar para a documentação correta.
- Permita a análise de plano único diretamente do plano real produzido.
- Novo conjunto de ícones.
- Adicionado suporte para reconhecer "Aplicar operadores lógicos" como GbApply, InnerApply.
        
XE Profiler:
- Renomeado para XEvent Profiler.
- Os comandos de menu Parar/Iniciar agora param/iniciam a sessão por padrão.
- Atalhos de teclado habilitados (por exemplo, CTRL-F para pesquisar).
- Ações de nome de host \_nome e cliente\_ do banco de dados adicionadas a eventos apropriados nas sessões do XEvent Profiler. Para que a alteração entre em vigor, talvez seja necessário excluir instâncias existentes da sessão do QuickSessionStandard ou QuickSessionTSQL nos servidores – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

Linha de comando:
- Adicionada uma nova opção de linha de comando ("-G") que pode ser usada para fazer com que o SSMS se conectar automaticamente a um servidor/banco de dados usando a Autenticação do Active Directory ('Integrado' ou 'Senha'). Para obter detalhes, consulte [Utilitário de Ssms](ssms-utility.md).

Assistente Importar Arquivo Simples:
- Adicionada uma maneira de escolher um nome de esquema diferente do padrão ("dbo") ao criar a tabela.

Repositório de Consultas:
- Restaurado o relatório "Consultas Regredidas" ao expandir a lista de relatórios disponíveis do Repositório de Consultas.

**IS (Integration Services)**
- Função de validação de pacote adicionada no Assistente de Implantação, o que ajuda o usuário a descobrir componentes dentro de pacotes do SSIS que não têm suporte no Azure SSIS IR.

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

- Pesquisador de Objetos:
    - Corrigido um problema em que o nó de função com valor de tabela não aparecia para instantâneos de banco de dados – [Connect 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161).
    - Desempenho melhorado ao expandir o nó de *bancos de dados* quando o servidor tem bancos de dados de fechamento automático.
- Editor de consultas:
    - Corrigido um problema em que o IntelliSense falhava para usuários que não têm acesso ao banco de dados mestre.
    - Corrigido um problema que estava fazendo com que o SSMS falhasse em alguns casos, quando a conexão com um computador remoto era fechada – [Connect 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557).
- Visualizador do XEvent:
    - Funcionalidade habilitada novamente para exportar para XEL.
    - Problemas corrigidos em que, em alguns casos, o usuário não conseguia carregar um arquivo XEL inteiro.
- XEvent Profiler:
    - Corrigido um problema que estava fazendo com que o SSMS falhasse quando o usuário não tinha as permissões *VIEW SERVER STATE*.
    - Corrigido um problema em que fechar a janela de Dados dinâmicos do XE Profiler não parava a sessão subjacente.
- Servidores registrados:
    - Corrigido um problema em que o comando "Mover para..." parava de funcionar – [Connect 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) e [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/).
- SMO:
    - Corrigido um problema em que o método TransferData no objeto Transferir não estava funcionando.
    - Corrigido um problema em que os bancos de dados do Servidor lançavam a exceção para bancos de dados SQL DW em pausa.
    - Corrigido um problema em que o script de banco de dados SQL no SQL DW gerava valores incorretos de parâmetro T-SQL.
    - Corrigido um problema em que o script de um banco de dados ampliado emitia incorretamente a opção *DATA\_COMPRESSION*.
- Monitor de Atividade de Trabalho:
    - Corrigido um problema em que o usuário recebia o erro "O índice está fora do intervalo. Deve ser não negativo e menor que o tamanho da coleção. 
        Nome do parâmetro: índice (System.Windows.Forms) "ao tentar filtrar por categoria – [Connect 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691).
- Caixa de diálogo de conexão:
    - Corrigido um problema em que os usuários de domínio sem acesso a um controlador de domínio de Leitura/Gravação não podiam fazer logon em um SQL Server usando a autenticação do SQL – [Connect 2373381 conectar](https://connect.microsoft.com/SQLServer/feedback/details/2373381).
- Replicação:
    - Corrigido um problema em que um erro semelhante a "Não é possível aplicar o valor 'null' à propriedade ServerInstance" era exibido ao olhar as propriedades de uma assinatura pull no SQL Server.
- Instalação do SSMS:
    - Corrigido um problema em que a instalação do SSMS fazia com que todos os produtos instalados no computador fossem reconfigurados incorretamente.
- Configurações do Usuário:
   - Com essa correção, os usuários de nuvem soberana do governo dos EUA terão acesso ininterrupto a seus recursos de banco de dados SQL do Azure e ARM com SSMS por meio de autenticação Universal e logon do Azure Active Directory.  Os usuários de versões anteriores do SSMS precisam abrir as Ferramentas|Opções|Serviços do Azure e, em Gerenciamento de Recursos, alterar a configuração da propriedade "Autoridade do Active Directory" para https://login.microsoftonline.us.

**AS (Analysis Services)**

- Criador de perfil: corrigido um problema ao tentar se conectar usando a Autenticação do Windows com o Azure AS.
- Corrigido um problema que poderia causar uma falha ao cancelar os detalhes de conexão em um modelo de 1400.
- Ao configurar uma chave de blob do Azure na caixa de diálogo de propriedades de conexão ao atualizar as credenciais, ela será visualmente mascarada agora.
- Corrigido um problema em que a caixa de diálogo de seleção de Usuário do Azure Analysis Services deve mostrar o guid da ID do aplicativo em vez da ID do objeto durante a pesquisa.
- Corrigido um problema na barra de ferramentas do designer de consulta Database\MDX que fazia com que os ícones fossem mapeados incorretamente para alguns botões.
- Corrigido um problema que impedia a conexão com o SSAS usando endereços de http/https do IIS msmdpump.
- Várias cadeias de caracteres na caixa de diálogo de Seletor de usuário do Azure Analysis Services agora foram traduzidas para os idiomas adicionais.
- A propriedade MaxConnections agora está visível para fontes de dados em modelos de tabela.
- O Assistente de Implantação agora gera definições de JSON corretas para membros da função AS do Azure.
- Corrigido um problema no SQL Profiler em que selecionar a Autenticação do Windows no Azure ainda solicitaria o logon.


## <a name="previous-ssms-releases"></a>Versões anteriores do SSMS

Baixe versões anteriores do SSMS clicando nos links de título nas seções a seguir.

## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>![baixar](../ssdt/media/download.png) [SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904)
Geralmente disponível| Número de build: 14.0.17199.0

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>Aprimoramentos

- Adição do novo assistente "Importar arquivo simples" para simplificar a experiência de importação de arquivos CSV com uma estrutura inteligente, exigindo a mínima intervenção do usuário ou o mínimo conhecimento especializado do domínio. Para obter detalhes, consulte [Import Flat File to SQL Wizard](../relational-databases/import-export/import-flat-file-wizard.md) (Assistente para Importar arquivo simples no SQL).
- Adição do nó "XEvent Profiler" ao Pesquisador de Objetos. Para obter detalhes, consulte [Use the SSMS XEvent Profiler](../relational-databases/extended-events/use-the-ssms-xe-profiler.md) (Usar o SSMS XEvent Profiler).
- Atualização da filtragem e da categorização de esperas no relatório histórico de esperas do Painel de desempenho.
- Adição da verificação de sintaxe da função “Prever”.
- Adição da verificação de sintaxe das consultas de Gerenciamento de biblioteca externa.
- Adição do suporte SMO para Gerenciamento de biblioteca externa.
- Adição do suporte "Iniciar PowerShell" à janela "Servidores registrados" (requer um novo módulo do SQL PowerShell).
- Sempre ativo: adição do [suporte a roteamento de somente leitura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) para grupos de disponibilidade.
- Adição de uma opção de enviar detalhes do rastreamento para a Janela de Saída para os logons do “Active Directory – suporte universal com MFA” (desativado por padrão, precisa ser ativado nas configurações do usuário em “Ferramentas > Opções > Serviços do Azure > Azure Cloud > Nível de rastreamento da Janela de Saída do ADAL”). 
- Repositório de Consultas: 
  - A interface do usuário do Repositório de Consultas poderá ser acessada mesmo quando o QDS estiver DESATIVADO contanto que o QDS tenha registrado algum dado.
  - Agora a interface do usuário do Repositório de Consultas expõe a categorização de esperas em todos os relatórios existentes. Isso permitirá que os clientes desbloqueiem os cenários das Principais consultas de espera e muitos outros.
- Realização da inclusão dos cabeçalhos dos parâmetros de script opcionais (desativada por padrão; pode ser habilitada nas configurações do usuário em “Ferramentas > Opções > Pesquisador de Objetos do SQL Server > Script > Incluir cabeçalho dos parâmetros de script”) – [Item do Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Marca "RC" removida.

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

- XEvent: 
   - Correção do problema em que o SSMS abre apenas parte dos eventos no arquivo .xel.
   - Melhoria na experiência “Observar dados dinâmicos” quando o banco de dados padrão não é 'mestre' – [Item do Connect 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582).
- Sempre ativo: correção do problema em que "Restaurar backups de log" pode falhar com o erro "O log deste conjunto de backup termina em LSN x, o que é muito cedo para ser aplicado ao banco de dados".
- Monitor de atividade de trabalho: correção de ícones inconsistentes – [Item do Connect 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100).
- Repositório de Consultas: correção do problema em que o usuário não pode escolher o intervalo de datas "personalizado" para relatórios do Repositório de Consultas. Vinculado aos itens do Connect abaixo.
   - [Item do Connect 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Item do Connect 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- Correção do problema no qual a caixa de diálogo de conexão não “limpa” o banco de dados usado mais recentemente quando as informações salvas têm um banco de dados nomeado e quando o usuário seleciona <default>.
- Script de objeto:
    - Correção de um problema no qual "Gerar script de banco de dados" não está funcionando e está gerando um erro quando o usuário tem um banco de dados DW em pausa no servidor, mas selecionou outro banco de dados que não é do DW e tentou gerar o script dele.
    - Correção de um problema no qual o cabeçalho dos Procedimentos armazenados com script não estava correspondendo às configurações do script, resultando em um script incorreto – [Item do Connect 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784).
    - Habilitação nova do "botão de Script" ao direcionar objetos do SQL Azure.
    - Correção do problema no qual o SSMS não estava permitindo scripts para “Alterar” ou “Executar” em alguns objetos (UDF, Exibição, SP, Gatilho) quando conectado a um banco de dados SQL do Azure – [Item do Connect 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386).
- Editor de consultas:
  - Melhoria do intellisense ao direcionar bancos de dados SQL do Azure.
  - Correção de um problema no qual as consultas falhavam devido a um token de autenticação expirado (Autenticação universal).
  - Melhoria do intellisense ao trabalhar com bancos de dados SQL do Azure (particularmente, ao se conectar a um Banco de Dados SQL do Azure, a gramática T-SQL mais recente (140) será usada).
  - Correção do problema no qual abrir uma janela de consulta com uma conexão com a um banco de dados que não é do DataWarehouse em um servidor faria todas as janelas de consulta subsequentes desse servidor com os bancos de dados do DataWarehouse gerarem vários erros sobre tipos/opções sem suporte.
- Always On:
   - Adição da coluna do modo de propagação ao painel do Sempre Ativo e à página de propriedades do grupo de disponibilidade.
   - Correção do problema no qual não era possível criar um grupo de disponibilidade do Linux quando o primário está no Windows – [Item do Connect 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856).
- Correção de vários problemas de “Memória insuficiente” no SSMS ao executar consultas – [Item do Connect 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190), [Item do Connect 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864).
- Profiler: 
   - Correção do problema no qual o Profiler não estava funcionado ao direcionar o SQL 2005.
   - Correção do problema no qual o Profiler não estava respeitando a opção de conexão “confiar no certificado do servidor”.
- Monitor de atividade: correção de um problema em que o Monitor de atividade não funciona quando indicado no SQL Server em execução no Linux.
- Correção de um problema com a classe de Transferência do SMO no qual ela não transferiria os objetos da Fonte de dados externos nem do Formato de arquivo externo; agora os objetos desses tipos devem ser corretamente incluídos na transferência.
- Servidores registrados:
   - Habilitação da consulta multisservidor para servidores do agente do usuário (ela tentará usar o mesmo token para todo servidor do agente do usuário no grupo).
- Autenticação universal do AD:
   - Correção do problema no qual não havia suporte à autenticação do Azure AD.
   - Correção do problema no qual o designer de tabela/exibição não estava funcionando.
   - Correção do problema no qual “Selecionar as primeiras 1000 linhas” e “Editar as primeiras 200 linhas” não estavam funcionando.
- Restauração do banco de dados: correção de um problema em que a restauração omite a última pasta no caminho ao mover arquivos para um local alternativo.
- Assistente de compactação:
   - Correção de um problema com o assistente para gerenciar a compactação para índices; correção de um problema no qual os assistentes para compactar dados estavam corrompidos para o SQL 2016 e anteriores.
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - Adição do Assistente de compactação às tabelas e índices do Azure.
- Plano de execução: 
   - Correção de um problema em que os operadores PDW não eram reconhecidos.
- Propriedades de servidor:
   - Correção de um problema com a incapacidade de modificar a afinidade de processador do servidor.


**AS (Analysis Services)**

- Correção de inúmeros problemas com o Assistente de implantação para dar suporte a modelos de nível de compatibilidade 1400 de tabela e fontes de dados do Power Query.
- Agora o Assistente de implantação pode ser implantado no AS Azure ao ser executado na Linha de comando.
- Ao usar a Autenticação do Windows no AS Azure, agora o usuário verá o nome da conta de usuário no Pesquisador de Objetos corretamente.


### <a name="known-issues-in-this-173-release"></a>Problemas conhecidos nesta versão 17.3:

**SSMS geral**

- A funcionalidade SSMS a seguir não é compatível com a autenticação do Azure AD usando o agente do usuário com MFA:
   - O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com a autenticação do Azure AD; há um problema conhecido em que a mensagem de erro apresentada ao usuário está um pouco criptografada “Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…" em vez da mensagem esperada “O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com o Banco de Dados SQL do Microsoft Azure. (DTAClient)”.
- A tentativa de analisar uma consulta nos resultados do DTA resulta em erro: "o objeto deve implementar IConvertible. (mscorlib)".
- *Consultas retornadas* está ausente na lista de relatórios do Repositório de Consultas no Pesquisador de Objetos.
   - Solução alternativa: clique com o botão direito do mouse no nó **Repositório de Consultas** e selecione **Exibir consultas retornadas**.

**IS (Integration Services)**

- O [execution_path] em [catalog]. [event_messagea] não está correto para execuções de pacote no Scale Out. O [Execution_path] começa com "\Package" em vez do nome do objeto do executável do pacote. Ao exibir o relatório de visão geral de execuções de pacote no SSMS, o link do "Caminho de execução" na Visão geral de execução não funciona. A solução alternativa é clicar em "Exibir mensagens” no relatório de visão geral para verificar todas as mensagens do evento.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![baixar](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
Disponibilidade geral | Número de build: 14.0.17177.0

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

### <a name="enhancements"></a>Aprimoramentos

- MFA (Autenticação Multifator do Microsoft Azure)
  - Autenticação de vários usuários do Azure AD para autenticação Universal com Autenticação Multifator do Microsoft Azure (UA com MFA)
  - Foi adicionado um novo campo de entrada de credenciais do usuário para autenticação Universal com MFA para oferecer suporte à autenticação de vários usuários.
- A caixa de diálogo de conexão agora oferece suporte aos 5 seguintes métodos de autenticação:
  - Autenticação do Windows
  - Autenticação do SQL Server
  - Active Directory – Universal com suporte à MFA
  - Active Directory – Senha
  - Active Directory – Integrado

- Exportação/importação do banco de dados para o assistente de DacFx usando a Autenticação universal com MFA.
- Para suporte de API, consulte a [Interface IUniversalAuthProvider](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Biblioteca ADAL gerenciada usada pela Autenticação universal do Azure AD com MFA foi atualizada para a versão 3.13.9.
- Além disso, uma nova interface de CLI foi entregue com suporte para a configuração de administrador do Azure AD para o banco de dados SQL e SQL Data Warehouse.

 Para obter mais informações sobre os métodos de autenticação do Active Directory, consulte [Autenticação universal com o banco de dados SQL e SQL Data Warehouse (suporte de SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) e [configure a autenticação multifator do Banco de Dados SQL do Azure para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- A janela de saída tem entradas para consultas executadas durante a expansão de nós do Pesquisador de Objetos do SQL Server
- Designer de exibição do Banco de dados SQL do Azure habilitado
- As opções de script padrão para gerar scripts de objetos no Pesquisador de Objetos do SQL Server no SSMS foram alteradas:
  - Anteriormente, o padrão em uma nova instalação era que o script gerado utilizava a versão mais recente do SQL Server (atualmente SQL Server 2017).
  - No SSMS 17.2, uma nova opção foi adicionada: *Corresponder configurações de script com a origem*. Quando definido como *True*, o script gerado utiliza a mesma versão, o tipo de mecanismo e edição do mecanismo que o servidor de onde o objeto que está sendo inserido no script veio.
  - O valor de *Corresponder configurações de script com a origem* é definido como *True* por padrão, portanto, novas instalações do SSMS serão automaticamente padronizadas para sempre gerar scripts de objetos com o mesmo destino do servidor original.
  - Quando o valor de *Corresponder configurações de Script com a origem* estiver definido como *False*, as opções de destino do script normal serão habilitadas e funcionarão como antes.
    - Além disso, todas as opções de script foram movidas para sua própria seção – *Opções de versão*. Elas não estão mais em *Opções Gerais de Script*.

- Suporte adicionado para as Nuvens nacionais em "Restaurar de URL"
- Os relatórios do QueryStoreUI agora dão suporte a métricas adicionais (RowCount, DOP, CLR Time etc.) do sys.query_store_runtime_stats.
- Agora há suporte para o IntelliSense para o banco de dados SQL do Azure
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- Segurança: caixa de diálogo de conexão será padronizada para não confiar em certificados de servidor e solicitar criptografia para conexões de banco de dados SQL do Azure
- Aperfeiçoamentos gerais sobre o suporte do SQL Server no Linux:
 - Nó de Correio do banco de dados está de volta
 - Problemas diversos relacionados aos caminhos corrigidos
 - O Monitor de atividade está mais estável
 - A caixa de diálogo Propriedades da Conexão exibe a plataforma correta
- Relatório de servidor de Painel desempenho agora está disponível como um relatório padrão:
  - Pode se conectar ao SQL Server 2008 e versões mais recentes.
  - O sub-relatório de índices ausentes usa a pontuação para ajudar a identificar os índices mais úteis.
  - O sub-relatório de histórico de estatísticas de espera agora agrega esperas por categoria. Esperas ociosas e suspensas filtradas por padrão.
  - Novo sub-relatório de histórico de travas.
- Pesquisa de nó do plano de execução permite pesquisar nas propriedades do plano. Pesquise facilmente por qualquer propriedade de operador como nome da tabela. Para usar essa opção ao exibir um plano:
  - Clique com o botão direito do mouse no plano e, no menu de contexto, clique na opção Localizar Nó
  - Use CTRL+F


**AS (Analysis Services)**

- Nova seleção de membro de função AAD para usuários sem endereço de email em modelos do AS Azure no SSMS

**IS (Integration Services)**

- Nova coluna adicionada ("Contagem Executada") para o relatório de execução para SSIS

### <a name="known-issues-in-this-release"></a>Problemas conhecidos nesta versão:

- Janelas de consulta usando a autenticação "Active Directory – Universal com suporte a MFA" podem ter um erro semelhante ao seguinte, ao tentar executar uma consulta depois de estarem abertas por uma hora:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   Executar novamente a consulta deve corrigir o erro e ser bem-sucedida.

- Não há suporte para a seguinte funcionalidade do SSMS para autenticação do Azure AD usando a Autenticação universal com MFA:
  - O designer **Nova tabela/exibição** mostra o prompt de logon de estilo antigo e não funciona para a autenticação do Azure AD.
  - O recurso **Editar 200 linhas superiores** não dá suporte à autenticação do Azure AD.
  - O componente **Servidor Registrado** não dá suporte à autenticação do Azure AD.
  - Não há suporte para o **Orientador de Otimização do Mecanismo de Banco de Dados** para autenticação do Azure AD. Há um problema conhecido em que a mensagem de erro apresentada ao usuário não é útil: *Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…* em vez da esperada *O Orientador de Otimização do Mecanismo de Banco de Dados não dá suporte ao Banco de Dados SQL do Microsoft Azure. (DTAClient)*.

**AS (Analysis Services)**

- Pesquisador de Objetos do SQL Server no SSAS não mostrará o nome de usuário de autenticação do Windows nas propriedades de conexão do AS Azure.

### <a name="bug-fixes"></a>Correções de bugs

- Corrigido um problema ao tentar imprimir os resultados de uma consulta (como texto).  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- Corrigido um problema em que o SSMS descartava incorretamente tabelas e outros objetos ao gerar o script de exclusão desses objetos em um banco de dados do SQL Azure.
- Corrigido um problema em que o SSMS ocasionalmente se recusava a iniciar com um erro como "Não é possível localizar um ou mais componentes. Reinstale o aplicativo"
- Um problema foi corrigido, no qual o SPID, na interface do usuário do SSMS, poderia ficar obsoleto e fora de sincronia. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- Corrigido um problema na instalação do SSMS (silencioso) em que o argumento /passive era tratado como /quiet.
- Corrigido um problema em que o SSMS ocasionalmente gera um erro de "Referência de objeto não definida para uma instância do objeto" na inicialização. http://connect.microsoft.com/SQLServer/feedback/details/3134698
- Corrigido um problema no "Assistente de compactação de dados" que estava fazendo com que o SSMS falhasse ao pressionar 'Calcular' na Tabela de gráfico
- Corrigido um problema de desempenho ao clicar com o botão direito do mouse em um índice para uma tabela (com uma conexão lenta com a Internet). https://connect.microsoft.com/SQLServer/feedback/details/3120783
- Corrigido um problema em que o SSMS não enumerava arquivos de backup em servidores com um agrupamento que diferencia maiúsculas de minúsculas. http://connect.microsoft.com/SQLServer/feedback/details/3134787 e https://connect.microsoft.com/SQLServer/feedback/details/3137000
- Diversas correções de plano de execução e comparação de plano de execução
- Corrigido um problema em que a caixa de diálogo de Conexão não permitia que o usuário especificasse o "Protocolo de rede" a ser usado para a conexão, a menos que o SQL Server estivesse instalado no computador que executa o SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- Suporte aprimorado para as configurações de vários monitores em que algumas caixas de diálogo do SSMS apareciam em locais "aleatórios". Adicionada uma nova opção de "Caixas de diálogo de tarefa" nas configurações do usuário "Pesquisador de Objetos do SQL Server | Comandos"para permitir lembrar a posição da caixa de diálogo de uma tarefa ou folha de propriedades quando ela for fechada. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- Corrigido um problema em que o SSMS não conseguia alterar as propriedades de banco de dados para o banco de dados SQL criptografado do Azure
- Opção "Descartar resultados após a execução" melhorada. https://connect.microsoft.com/SQLServer/feedback/details/1196581
- Melhorado/corrigido o problema em que os usuários não conseguiam acessar as assinaturas do Azure para as quais eles não são administradores.
- Assistente "Restauração de banco de dados" aprimorado para manter o banco de dados de destino selecionado no OE independentemente da seleção de banco de dados de origem. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- Corrigido um problema em que o Pesquisador de Objetos do SQL Server não classificava "procedimentos armazenados compilados nativamente" recém-adicionados incorretamente. http://connect.microsoft.com/SQLServer/feedback/details/3133365
- Corrigido um problema em que "SELECT TOP n ROWS" não incluía a cláusula "TOP". Para Azure SQLDW. https://connect.microsoft.com/SQLServer/feedback/details/3133551 e https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: corrigido o problema em que intervalos de tempo não personalizados não funcionavam corretamente para todos os relatórios.
- Always Encrypted:
    - Aprimorado o sistema de mensagens de status de permissão de AKV na caixa de diálogo Novo CMK
    - Dicas de ferramenta adicionadas à lista suspensa CEK para tornar mais fácil distinguir CEKs com nomes longos
    - Corrigido um problema em que alguns provedores de repositório de chaves CNG não seriam exibidos na caixa de diálogo Nova chave mestra de coluna para Always Encrypted
- Corrigido "Nome do aplicativo" inconsistente para conexões de SSMS. http://connect.microsoft.com/SQLServer/feedback/details/3135115
- Corrigido um problema em que SSMS não gerava scripts corretos para o SQL Azure (tabelas e índices com opção DATA_COMPRESSIONS). https://connect.microsoft.com/SQLServer/feedback/details/3133148
- Corrigido um problema em que o usuário não podia usar o atalho CTRL + Q para Início rápido (Observação: as novas associações de tecla para alternar a opção "IntelliSense habilitado" no Editor de consultas agora são CTRL + B, CTRL + I. https://connect.microsoft.com/SQLServer/feedback/details/3131968
- Corrigido um problema em "Restaurar banco de dados" em que o SSMS lançava uma exceção ao tentar selecionar uma conta de armazenamento de uma assinatura que tinha contas com domínios personalizados definidos
- Corrigido um problema em "Diagrama de banco de dados" em que o SSMS gerava um erro externo "O índice estava fora dos limites da matriz"; Além disso, o usuário não conseguia alterar a "Exibição de tabela" para qualquer, exceto padrão. https://connect.microsoft.com/SQLServer/feedback/details/3133792 e http://connect.microsoft.com/SQLServer/feedback/details/3135326
- Corrigido um problema em "Backup/restauração de URL" em que o SSMS não enumerava contas de armazenamento clássicas.
- Corrigido um problema em que uma exceção era lançada ao tentar adicionar protegíveis associados a esquema a funções de banco de dados. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- Corrigido um problema em que o SSMS exibia intermitentemente o erro "Dados são Null. Não é possível chamar este método ou esta propriedade em valores Null”. ao expandir um nó de tabela http://connect.microsoft.com/SQLServer/feedback/details/3136283
- DTA: Corrigido um problema em que o DTAEngine.exe termina com Corrompimento de Heap ao avaliar a função de partição com determinados valores de limite.


**AS (Analysis Services)**

- Corrigido um problema em que o Banco de dados de restauração do AS falha com um erro se o banco de dados tiver um nome diferente da ID
- Corrigido um problema que fazia com que a janela de consulta DAX ignorasse a opção de menu para alternar para IntelliSense habilitado
- Corrigido um problema que impedia a conexão com o SSAS por endereços de http/https do IIS msmdpump
- Permitir a conexão com o AS Azure usando uma senha que contenha um ponto e vírgula
- Realizar o script do comando Banco de dados de restauração do AS com a opção "Ignorar associação" incluirá a nova opção de JSON correspondente quando usada com o servidor do AS do SQL Server 2017 ou Azure AS
- Corrigido um problema extremamente raro que poderia fazer com que a caixa de diálogo Excluir banco de dados gerasse um erro ao carregar
- Corrigido um problema que poderia ocorrer ao tentar exibir partições no modelo de nível de compatibilidade 1400 contendo uma mistura de consulta de SQL e definições de partição M

**IS (Integration Services)**
- Corrigido um problema em que os relatórios de informações de execução de catálogo do SSISDB não podiam ser exibidos
- Problemas corrigidos no SSMS relacionados ao desempenho insatisfatório com uma grande quantidade de pacotes/projetos

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=799832)
Disponibilidade geral | Número de build: 14.0.17119.0

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>Aprimoramentos

- Criador de perfil: Ajuda > A opção Sobre agora exibe o número de versão (por exemplo, 17.1)
- Usuários do Analysis Service podem atualizar as credenciais para suas fontes de dados para modelos 1200 TM e superior no menu de contexto na fonte de dados
- Relatórios de SSIS internos agora mostram logs de execução de expansão do SSIS no CTP 2.1
- Aplicativo de gerenciamento de expansão do SSIS
  - Exibir informações básicas sobre o mestre de expansão.
  - Adicione facilmente um trabalho à implantação escalável.
  - Exibir todos os trabalho de expansão e informações básicas sobre eles, além de poder habilitar ou desabilitá-los facilmente.

### <a name="bug-fixes"></a>Correções de bugs
- Always On:
  - Correção de um problema em que as propriedades de uma réplica de disponibilidade sempre eram exibidas como o modo de “Failover automático” para AGs do WSFC.
  - Correção de um problema em que a lista de roteamento somente leitura era substituída ao atualizar o Grupo de Disponibilidade
- Always Encrypted: foi corrigido um problema em que o arquivo de log gerado não continha as informações geradas por DacFx.
- Plano de execução: foi corrigido um problema em que a interface do usuário sempre mostrava o atributo de tipo de junção Real para operadores de junção Não adaptáveis.
- Programa de instalação:
  - Correção de um problema em que o SSMS 17.0 estava interrompendo o SSDT no Visual Studio 2013 [Conectar Item 3133479]
  - Correção de um problema em que a clicar em “Reiniciar” no final da instalação não estava reiniciando o computador
- Script: para impedir temporariamente que o SSMS exclua acidentalmente objetos de banco de dados do Azure ao tentar usar script na exclusão, tal opção foi desabilitada.  Uma correção apropriada será incluída em uma versão futura do SSMS.
- Pesquisador de Objetos: foi corrigido um problema em que o nó “Bancos de dados” não era expandido quando conectado a um Banco de Dados do Azure criado usando “AS COPY”

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de build: 14.0.17099.0

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>Aprimoramentos 

- Pacote de atualização e WSUS (Windows Software Update Services) 
    - Versões futuras do 17.X incluem um pacote de atualização cumulativa menor 
  - O pacote de atualização também será publicado no catálogo do WSUS  
- Atualizações de ícone
    - Os ícones foram atualizados para serem consistentes com os ícones fornecidos pelo VS Shell e compatibilidade com resoluções de alto DPI
    - Novos ícones de programa SSMS e Criador de Perfil para diferenciar entre as versões 16.X e 17.X
- Módulo do PowerShell no SQL
  - O módulo do SQL Server PowerShell foi removido do SSMS e agora é fornecido por meio da Galeria do PowerShell (o PowerShell 5.0 agora é necessário para compatibilidade com o controle de versão do módulo)
  - Diversas melhorias na “apresentação” (formatação) de alguns objetos SMO (por exemplo, agora os bancos de dados mostram o tamanho e o espaço disponível, enquanto as tabelas mostram a contagem de linhas e o uso de espaço)
  - Colorização adicionada quando o prompt de comando do PowerShell é invocado no menu “Iniciar o PowerShell” do OE
  - Adição do parâmetro -ClusterType e -RequiredCopiesToCommit aos cmdlets do AG (New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup e Set-SqlAvailabilityGroup)
  - Adição de parâmetros -ActiveDirectoryAuthority e -AzureKeyVaultResourceId ao cmdlet Add-SqlAzureAuthenticationContext
  - Foram adicionados os cmdlets Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase e Set-SqlAvailabilityReplicaRoleToSecondary
  - Foi adicionado o parâmetro -SeedingMode aos cmdlets Set-SqlAvailabilityReplica e New-SqlAvailabilityReplica
  - Foi adicionado o parâmetro -ConnectionString a Get-SqlDatabase
- SQL Server no Linux
    - Melhorias gerais e correções para o Envio de Logs
  - Foi adicionado suporte para caminhos de Linux nativo para bancos de dados de Anexação, Restauração e Backup
  - Foi adicionado suporte para caminhos de Linux nativo para a pasta de destino do log de auditoria
- Analysis Services
  - Janela de Consulta DAX:
    - Correspondência de parênteses no editor
    - Suporte à sintaxe DEFINE MEASURE e DEFINE VAR
    - Diversas melhorias do IntelliSense
  - Autenticação Universal
    - Permite que os usuários especifiquem um nome de usuário sem nenhuma senha e a Caixa de Diálogo de Logon do Azure tratará a conexão
  - Integração do SSMS PQ: 
    - Scripts de trabalhos de fontes de dados estruturadas 
    - Exibição e edição de fontes de dados estruturadas na interface do usuário de PQ
- Novo modelo "Adicionar Restrição Exclusiva"
- Showplan
    - Mostre o máximo em vez da soma nos threads na janela de propriedades do tempo decorrido
    - Exponha novas propriedades de operador de concessão de memória
    - Habilitação do botão "Editar Consulta" nas estatísticas de consulta em tempo real
    - Suporte para a execução intercalada
  - Nova opção para “Analisar o plano de execução real”
  - Melhorias gerais na comparação do plano de execução
  - Introdução da funcionalidade do recurso de Comparação do Plano de Execução para encontrar diferenças significativas na Estimativa de Cardinalidade entre os nós correspondentes de dois planos de consulta e executar a análise básica das possíveis causas raízes
- Remoção do Gerenciador de Configuração do Gerenciador de Servidores Registrados
- Habilitação da leitura logs de auditoria do Armazenamento de Blobs do Azure
- Parametrização adicionada para Always Encrypted, consulte [esta página](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) para obter mais detalhes 
- A conexão de autenticação AAD Universal para Banco de Dados SQL do Azure dá suporte à ID de locatário personalizada 
- Geração de scripts para o Banco de Dados SQL do Azure, agora scripts de texto completo, regras e banco de dados
- Correções de identidade visual em telas de abertura para SSMS e Criador de Perfil
- A interface do usuário do ponto de controle do utilitário foi removida do SSMS
- Agora o SSMS pode criar Bancos de Dados SQL do Azure “PremiumRS” edition
- Grupos de Disponibilidade AlwaysOn
  - Foi adicionado suporte a novos tipos de cluster: EXTERNAL e NONE
    - Foi adicionado suporte ao SQL Server no Linux
    - Foi adicionada a propagação automática como uma opção de sincronização de dados inicial
    - Correção de alguns defeitos, por exemplo, de manuseio de URL de ponto de extremidade, atualização de BD e layout de interface do usuário
    - Remoção de recursos relacionados à réplica do Azure
  - O IntelliSense foi melhorado para várias palavras-chave do Grupo de Disponibilidade
- Monitor de Atividade
  - Foi adicionado o novo painel “Monitor de Atividades” à janela de saída do SSMS
  - Alteração da mensagem de erro/tempo limite de conexão para registrar informações na janela de saída em vez de uma mensagem de pop-up
  - Remoção de um gráfico vazio (5º gráfico) na seção Visão geral
  - Foi adicionado “(em pausa)” ao título da Visão geral se a coleta de dados do Monitor de Atividades estiver em pausa
  - Extensões de gráfico para o SQL Server 
    - Novos ícones para nó de gráfico e tabelas de borda
    - Nó de gráfico e tabelas de borda serão exibidos na pasta Tabelas de gráfico
    - Modelos para criar nó de gráfico e tabelas de borda disponíveis
- Modo de Apresentação
    - Três novas tarefas disponíveis por meio do Início Rápido (Ctrl+Q)
    - PresentOn - Ativar o modo de apresentação
    - PresentEdit - Editar os tamanhos de fonte de apresentação para o modo de apresentação.  "Fonte do Editor de texto" para o Editor de Consultas.  "Fonte de ambiente" para outros componentes.
    - RestoreDefaultFonts - Reverter para as configurações padrão.
    - *Observação: no momento, não há um comando PresentOff.  Use RestoreDefaultFonts para desativar o Modo de Apresentação*

### <a name="bug-fixes"></a>Correções de bugs

- Correção de um problema em que o SSMS falhou ao rolar o plano de execução pelo touchpad do surfacebook
- Correção de um problema em que o SSMS travava por um longo tempo ao obter as propriedades de um banco de dados que estava sendo restaurado ou offline 
- Correção de um problema em que não era possível abrir o “Visualizador da Ajuda” em builds RC
- Correção de um problema em que os itens da “Caixa de ferramentas das tarefas dos planos de manutenção” podiam estar ausentes no SSMS.
- Correção de um problemas no SSMS em que o usuário não podia reduzir um banco de dados quando o nome dele continha chaves. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Correção de um problema em que o SSMS estava tentando executar scripts à exclusão de um banco de dados do Azure e que, na verdade, causava a exclusão do próprio banco de dados. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- Correção de um problema em que os valores padrão não foram colocados em script para os tipos de tabela definidos pelo usuário. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- Outra rodada de melhorias de desempenho no menu de contexto em índices. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- Correção do problema que estava causando cintilação excessiva ao posicionar o mouse sobre um índice ausente no plano de execução. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- Correção de um problema no qual o SSMS estava colocando o banco de dados no modo offline ao executar o script [item do Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- Correções diversas na interface do usuário em versões localizadas (não inglês) do SSMS.
- Correção do problema no qual o nó "Chaves do Always Encrypted" estava ausente durante o direcionamento do SQL 2016 SP1 Standard Edition.
- Always Encrypted
    - Menu "Always Encrypted" incorretamente habilitado ao direcionar o SQL 2016 RTM Standard Edition ou qualquer servidor do SQL 2014 (e abaixo)
    - Correção de um problema em que o IntelliSense relata um erro quando a sintaxe CREATE ou ALTER é usada
    - Correção do problema em que a criptografia falha caso CMK/CEK contenha caracteres que devem ser escapados, ou seja, entre colchetes
    - Quando ocorre uma exceção de Memória Insuficiente no SSMS, o usuário recebe um erro que sugere, em vez disso, o uso do PowerShell nativo (64 bits).
    - Correção do problema em que o assistente do AE falha caso o usuário esteja usando assinaturas do Gerenciador de Grupo de Recursos em vez de assinaturas do Azure clássico
    - Correção do problema em que o assistente do AE mostra um erro incorreto quando o usuário não tiver permissão nas assinaturas ou não tiver um Azure Key Vault em qualquer um delas.
    - Problema corrigido no assistente do AE em que a página de entrada do Azure Key Vault não mostrava as assinaturas do Azure em caso de vários AAD
    - Problema corrigido no assistente do AE em que a página de entrada do Azure Key Vault não mostrava as assinaturas do Azure para as quais o usuário tinha permissão de leitura
  - Correção de um problema em que os arquivos de recurso podiam não ser carregados corretamente, resultando em mensagens de erro incorretas
- Contraste aprimorado de hiperlinks na página de Configuração do SSMS
- Correção de um problema em que os nós Polybase não eram exibidos quando conectado ao SQL Server Express (2016 SP1)
- Correção de um problema em que o SSMS não conseguia alterar o Nível de Compatibilidade do BD SQL do Azure para v140
- Desempenho aprimorado do Pesquisador de Objetos ao expandir a lista de bancos de dados do Azure [item do Connect](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- Correção de um problema em que o item de menu de contexto "Exibir Log do SQL Server" aparecia incorretamente para tipos de servidor não relacionais (AS\RS\IS) 
- Correção de um problema em que a verificação de sintaxe de uma consulta de partição do Analysis Services usando a autenticação do SQL podia resultar em uma mensagem de falha de logon
- Correção de um problema em que a renomeação de modelo de tabela do AS com nível de compatibilidade de visualização 1400 falhava no SSMS
- Correção de um problema de "falha de operação no modelo" que poderia ocorrer após a tentativa de uma operação inválida no servidor do AS em circunstâncias raras, reversão de alterações locais após uma gravação sem êxito no modelo
- Correção de um erro de digitação na caixa de diálogo de pop-up Sincronizar Banco de Dados do Analysis Services
- Caixas de diálogo de contêiner de backup/restauração surgem fora da tela em configurações com vários monitores. 
- A criação de SecurityPolicy falhará se o objeto de destino tiver ] em seu nome.
- O menu "Abrir recente" do SSMS 2016 não mostra arquivos salvos recentemente. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- Reinicialização removida das configurações do usuário quando o VS Shell é atualizado.
- Correção de um problema que impedia o usuário de alterar o Nível de Compatibilidade de um banco de dados do SQL Server 2017.
- Janelas de consulta usando a autenticação do AAD Universal não podem atualizar a consulta após uma hora.
- A interface do usuário do ponto de controle do utilitário foi removida do SSMS.
- Conexões de autenticação do AD Universal falham ao consultar dados após a expiração do token inicial.
- Não é possível escrever script de regras do Banco de Dados SQL do Azure para Banco de Dados SQL do Azure.
- Corrigido o problema foram SQL PowerShell não era capaz de se conectar a instâncias do SQL herdadas (2014 e anteriores). [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- Corrigido um problema que estava causando pane do SSMS quando este falhava ao importar servidores registrados.
- Corrigido um problema que estava causando falha do SSMS se um usuário tinha determinadas permissões em um banco de dados. 
- SSMS – tabelas desaparecem da área de design ao visualizar novamente determinadas exibições. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- A barra de rolagem de tabela não permite que o usuário role o conteúdo da tabela, somente a seta para cima/para permite isso. O também é possível rolar o conteúdo da tabela depois de tentar rolar usando a barra de rolagem, o que é um bug. [Conectar Item](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- Servidores registrados não exibindo ícones depois de atualizar o nó raiz.
- O botão de script para criar o banco de dados em servidores v12 do Azure executa o script e exibe a mensagem "Nenhuma ação para receber scripts".
- SSMS, a caixa de diálogo Conectar-se ao Servidor não limpa a guia "Propriedades Adicionais" para cada nova conexão.
- O script Gerar Tarefas não gera scripts de Criar Banco de Dados para um Banco de Dados SQL do Azure.
- A barra de rolagem no Designer de Exibição aparece desabilitada.
- Os caminhos de chave AVK Always Encrypted não incluem IDs de versão.
- Número reduzido de consultas do mecanismo de edição na janela de consulta. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- Erros do Always Encrypted causados pela atualização de módulos após a criptografia são manipulados incorretamente.
- Alterado tempo limite de conexão padrão para OLTP e OLAP de 15 para 30 segundos para corrigir uma classe de falhas de conexão ignoradas. 
- Corrigida uma falha no SSMS quando o relatório personalizado era iniciado. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Corrigido um problema em que "Gerar Script..." falhava para Bancos de Dados SQL do Azure.
- Corrigido "Escrever Script Como" e "Assistente de Gerar Script" para não adicionar novas linhas extras ao escrever script de objetos, por exemplo procedimentos armazenados. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- O provedor SQLAS PowerShell: adicione a propriedade LastProcessed às pastas Dimension e MeasureGroup. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- Estatísticas de consulta em tempo real: corrigido o problema em que apenas a primeira consulta em um lote era mostrada. [Connect Item] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Plano de execução: na janela Propriedades, mostrar o máximo em vez da soma nos threads.
- Repositório de consultas: adicione novo relatório em consultas com alta variação de execução.
- Problemas de desempenho do Pesquisador de Objetos: [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - O menu de contexto para tabelas trava momentaneamente
    - O SSMS está lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota (Internet)). 
    - Evitar emitir consultas de tabela que são classificadas no servidor
- Removido o Assistente de Implantação do Azure (implantar banco de dados em VM do Azure) do SSMS
- Corrigido o problema em que os índices ausentes não eram mostrados nos planos de execução no SSMS [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- Corrigido um problema comum de falha no desligamento no SSMS
- Corrigido um problema no Pesquisador de Objetos em que ocorria um erro ao abrir o menu de contexto no Polybase | Nós de grupo de expansão [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- Corrigido um problema em que o SSMS poderia falhar ao tentar exibir as permissões em um banco de dados
- Repositório de consultas: aprimoramentos gerais em itens de menu de contexto para grades de resultados do relatório do repositório de consultas
- Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [Connect Item] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [Connect Item] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.
- Corrigido um problema de truncamento da interface do usuário na caixa de diálogo "Registro de Novo Servidor"
- Corrigida a interface do usuário da condição DMF, que atualizava incorretamente expressões que continham valores de constante de cadeia de caracteres com aspas
- Corrigido um problema que pode fazer com que o SSMS falhe ao executar relatórios personalizados
- Adicionar item de menu "Execução ao Escalar Horizontalmente..." no nó da pasta
- Correção de um problema com o recurso de endereço IP da lista de permissões do firewall do BD SQL do Azure
- Correção de um problema no SSMS que causava uma exceção de referência de objeto não definida ao editar a origem da partição multidimensional do AS
- Correção de um problema no SSMS que causava uma exceção de referência de objeto não definida ao excluir um assembly de cliente do servidor multidimensional do AS
- Correção de um problema que causava uma falha ao renomear um bd de tabela 1400 do AS
- Correção de um problema com o script de uma fonte de dados de tabela do AS com nível de compatibilidade 1400 da caixa de diálogo de propriedades de conexão
- Remoção da suposição de que as tabelas em um modelo no nível de compatibilidade 1400 do AS têm pelo menos uma partição
- CTRL-R agora alterna o painel de resultados no editor de consultas do SSMS DAX


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de build: 13.0.16106.4

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

Os seguintes problemas foram corrigidos nesta versão:

* Corrigido um problema introduzido no SSMS 16.5.2 que estava causando a expansão do nó 'Table' quando a tabela tinha mais de uma coluna esparsa.

* Os usuários podem implantar pacotes do SSIS contendo o Gerenciador de Conexões do OData, que se conectam a um recurso do Microsoft Dynamics AX/CRM Online para o catálogo do SSIS. Para obter mais informações, consulte [Gerenciador de Conexões do OData](../integration-services/connection-manager/odata-connection-manager.md).

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


## <a name="ssms-1651"></a>SSMS 16.5.1
Disponibilidade geral | Número de build: 13.0.16100.1

* Corrigido um problema em que Invoke-Sqlcmd erroneamente insere várias linhas quando ocorre a restrição check. [Item do Microsoft Connect: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Corrigido um problema em que as versões de idioma de não ENU não funcionam completamente durante a criação de grupos de disponibilidade.

* Corrigido um problema em que o plano de consulta XML não abre a interface do usuário de SSMS adequada.


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de build: 13.0.16000.28


[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 16.4.1 (setembro de 2016)](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de versão: 13.0.15900.1

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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
[Item nº 1231091 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Corrigido um problema em que o Assistente de Restauração do Banco de Dados não aceita nomes de arquivos com espaços em branco à esquerda:   
[Item do Microsoft Connect nº2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS 16.3 (agosto de 2016)](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de versão: 13.0.15700.28


[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* Versões mensais do SSMS agora são sinalizadas numericamente.

* [Nova opção de autenticação **'Autenticação Universal do Active Directory'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Esse é um mecanismo de autenticação baseada em token orientado pelo Azure Active Directory que dá suporte a mecanismos de autenticação multifator, de senha e integrada.

* Novos modelos de eventos estendidos correspondentes à funcionalidade dos modelos do SQL Server Profiler [(Item nº 2543925 do Microsoft Connect)](../tools/sql-server-profiler/sql-server-profiler-templates.md).

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
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [atualização de hotfix de julho de 2016 do SSMS](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de versão: 13.0.15600.2

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* **Correção de bug no SSMS para habilitar os itens de menu de atalho ausentes**.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item do Microsoft Connect nº2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Item do Microsoft Connect nº2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Item do Microsoft Connect nº2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016"></a>SSMS de julho de 2016 
Disponibilidade geral | Número de versão: 13.0.15500.91

* *Edição, 5 de julho:* suporte aprimorado para bancos de dados de tabela do SQL Server 2016 (nível de compatibilidade 1200) na caixa de diálogo Processo do Analysis Services e no assistente de Implantação do Analysis Services.

* *Edição, 5 de julho:* nova opção na caixa de diálogo 'opções de execução de consulta' no SSMS para definir 'XACT_ABORT'. Essa opção será habilitada por padrão nessa versão do SSMS e instruirá o SQL Server a reverter a transação inteira e anular o lote se ocorrer um erro em tempo de execução.

* Suporte para SQL Azure Data Warehouse no SSMS.

* Atualizações importantes para o módulo PowerShell do SQL Server. Isso inclui um novo [módulo SQL PowerShell e novos CMDLETs para Always Encrypted, SQL Agent e Logs de Erros do SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update).

* Suporte para a geração de script do PowerShell no assistente Always Encrypted.

* Tempos de conexão significativamente aprimorados para bancos de dados do SQL Azure.

* Nova caixa de diálogo “Backup em URL” para dar suporte à criação de credenciais de armazenamento do Azure para backups de banco de dados do SQL Server 2016. Essa caixa de diálogo fornece uma experiência mais simplificada para armazenar os backups de banco de dados em uma conta de armazenamento do Azure.
 
* Diálogo Nova Restauração para simplificar a restauração de um backup de banco de dados do SQL Server 2016 do serviço de armazenamento do Microsoft Azure.
 
* Correção de bugs no designer de consulta do SSMS para permitir a adição de tabelas ao designer se um usuário não tiver permissões SELECT.

* Correção de bug para adicionar suporte do IntelliSense para as funções 'TRY_CAST()' e 'TRY_CONVERT()'.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2453461 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* Correção de bug no módulo do PowerShell para habilitar o carregamento da extensão 'SQLAS' do Analysis Services.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2544902 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* Correção de bug na janela do editor SSMS para permitir as ações de arrastar e soltar de abertura para arquivos do Sql.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2690658 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* Correção de bugs no criador de perfil para corrigir falhas de criador de perfil ao sair.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2616550 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Item nº 2319968 do Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* Correção de bug no SSMS para evitar falha ao tentar editar um link de associação no designer de tabela SSMS.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2721052 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* Correção de bugs no SSMS para habilitar a geração de script de banco de dados para membros da função db_owner.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2869241 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* Correção de bugs no editor do SSMS para remover o atraso no fechamento de uma guia de consulta se o servidor ficar offline.  
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2656058 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* Correção de bug para habilitar a opção de Backup em bancos de dados SQL Server Express. 
*Solicitações vinculadas de bugs dos clientes:*  
[Item nº 2801910 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Item nº 2874434 do Microsoft Connect](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* Correção de bugs no Analysis Services para mostrar corretamente o provedor de Feed de Dados para modelos multidimensionais do Analysis Services.

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>![baixar](../ssdt/media/download.png) [SSMS de junho de 2016](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponibilidade geral | Número de versão: 13.0.15000.23

[Chinês (República Popular da China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chinês (Taiwan)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* O SSMS tem disponibilidade geral a partir da versão de junho de 2016.

* Nova caixa de diálogo de localização rápida no SSMS integrada de forma melhor ao documento atual e que permite pesquisar por meio de expressões regulares. 
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* Aprimoramentos no instalador do SSMS para que você possa acompanhar o progresso da instalação e processas códigos de saída para instalações autônomas por meio de scripts.

* Correção de bug na ajuda F1 contextual do SSMS para exibir corretamente artigos e documentos de ajuda.

* Correção de bug no modo de exibição de 'Consultas Retornadas' do Repositório de Dados de Consulta que causou a falha do SSMS durante a rolagem.

* Correção de bug no conector OLEDB do Excel Analysis Services para permitir conexões do Excel 2016 ao SQL Server Analysis Services.

* Correção de bug na caixa de diálogo de conexão do SSMS para mostrar a caixa de diálogo de conexão no mesmo monitor que a janela principal do SSMS em sistemas de vários monitores.  
*Solicitações vinculadas de bugs dos clientes:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* Correções de bugs na experiência do Always Encrypted. Foi corrigido um bug em que a opção de menu Always Encrypted não era habilitada corretamente para Stretch Databases. Também foi corrigido um bug no assistente do Always Encrypted em que ele não usava corretamente o provedor HSM da SafeNet (Luna SA).


## <a name="additional-downloads"></a>Downloads adicionais  
Para obter uma lista de todos os downloads do SQL Server Management Studio, veja o [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obter a versão mais recente do SQL Server Management Studio, veja [Baixar o SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
