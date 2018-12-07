---
title: SQL Server Management Studio – Changelog (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db6f79e16f65494bdb45b297324541668d69d567
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712727"
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este artigo fornece detalhes sobre atualizações, aprimoramentos e correções de bug para as versões atuais e anteriores do SSMS. Baixe [versões anteriores do SSMS](#previous-ssms-releases).

## <a name="ssms-180-preview-5download-sql-server-management-studio-ssmsmd"></a>[SSMS 18.0 (versão prévia 5)](download-sql-server-management-studio-ssms.md)

Número de build: 15.0.18068.0<br>
Data de lançamento: 15 de novembro de 2018

A versão prévia 5 é a segunda versão prévia pública do SSMS 18.0. Para a versão de GA (disponibilidade geral) mais recente do SSMS, [baixe e instale o SSMS 17.9](#ssms-179-latest-ga-release).

### <a name="whats-new"></a>Novidades

**SSMS geral**

- O "tamanho máximo para arquivos de log de erros" foi exposto em "Configurar os logs de erro do SQL Server". Para obter detalhes, veja [Definir o tamanho máximo dos logs de erros do SQL Server](https://feedback.azure.com/forums/908035/suggestions/33624115).  

Pesquisador de Objetos:

- A lógica foi estendida para solicitar confirmação ao renomear um banco de dados para todos os objetos de esquema (a configuração pode ser definida e isso pode ser desabilitado).

Script de objeto:

- Novos itens de menu foram adicionados para 'CRIAR OU ALTERAR' ao gerar script de objetos.

Atualização de nível de compatibilidade do banco de dados:

-  Uma nova opção foi adicionada em <Database name> > **Tarefas** > **Atualização de banco de dados**. Essa opção inicia o novo *Assistente de Ajuste de Consulta* para orientar os usuários pelo processo de:
   - Coleta de uma linha de base de desempenho antes de atualizar o nível de compatibilidade do banco de dados.  
   - Atualização para o nível de compatibilidade do banco de dados desejado.
   - Coleta de uma segunda passagem de dados de desempenho sobre a mesma carga de trabalho.
   - Detectar regressões de carga de trabalho e fornecer recomendações testadas para melhorar o desempenho da carga de trabalho.

Esse recurso é semelhante ao processo de atualização de banco de dados documentado em [Manter a estabilidade do desempenho durante a atualização para um SQL Server mais recente](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade), exceto pela última etapa, na qual o QTA não se baseia em um estado válido anteriormente conhecido para gerar recomendações.

Repositório de Consultas:

- A usabilidade de alguns relatórios (consumos gerais de recursos) foi aprimorada, adicionando um separador de milhar a números a serem exibidos no eixo y dos gráficos.
- Um novo relatório de estatísticas de espera de consulta foi adicionado.

Avaliação de vulnerabilidades:

- O menu de tarefas de avaliação de vulnerabilidades foi habilitado no SQL Data Warehouse do Azure.

Mascaramento de dados:

- A Máscara de Dados Estáticos foi adicionada. A Máscara de Dados Estáticos é uma ferramenta de proteção de dados que permite aos usuários criar uma cópia do seu Banco de Dados SQL e mascarar dados confidenciais na cópia. O recurso mostra-se útil para aqueles que compartilham seu banco de dados de produção com usuários de não produção, tais como a equipe de desenvolvimento/teste ou a equipe de análise. Para obter mais informações, confira [Máscara de Dados Estáticos para Banco de Dados SQL do Azure e SQL Server](https://azure.microsoft.com/blog/static-data-masking-preview/).

SMO:

- A nova propriedade ProductUpdateLevel foi exposta no objeto de servidor, que mapeia para o nível de manutenção para a versão do SQL em uso (por exemplo, CU12, RTM, etc.).
- A nova propriedade LastGoodCheckDbTime foi exposta no objeto de banco de dados, que mapeia para a propriedade de banco de dados "lastgoodcheckdbtime". Se essa propriedade não estiver disponível, um valor padrão de 1/1/1900 12:00:00 AM será retornado.

Suporte à Instância Gerenciada:

- Suporte adicionado à replicação lógica.

Integração com Azure Data Studio:

- Item de menu **Iniciar o Azure Data Studio** adicionado ao Pesquisador de Objetos.

SSIS:

- Suporte adicionado para permitir aos clientes agendar pacotes do SSIS nos Azure-SSIS IRs que estão na nuvem do Azure Governamental.

### <a name="bug-fixes"></a>Correções de bugs

Panes/travamentos:

- Corrigida uma falha no SSMS ao tentar usar servidores do Banco de Dados SQL do Azure e do Servidor de Gerenciamento Central. Para obter detalhes, confira [falha ao usar o Servidor de Gerenciamento Central](https://feedback.azure.com/forums/908035/suggestions/33374884).  
- Corrigido um travamento no Pesquisador de Objetos ao otimizar a maneira como a propriedade IsFullTextEnabled é recuperada.
- Corrigido um travamento no 'Assistente para Copiar Banco de Dados', evitando-se a compilação de consultas desnecessárias para recuperar propriedades de banco de dados.

Opções do SSMS:

- Restaurado CTRL + D como o atalho, assim como era na versão mais antiga do SSMS. Para obter detalhes, confira [Restaurar atalho CTRL-D para ResultsToGrid no SSMS](https://feedback.azure.com/forums/908035/suggestions/35544754).

Pesquisador de Objetos:

- Corrigido um problema em que a caixa de diálogo 'Nova agenda de trabalho' não renderizava corretamente em monitores com alto DPI.
- Corrigida/melhorada a maneira como o tamanho de banco de dados ("Tamanho (MB)") é exibido no Pesquisador de Objetos. Apenas 2 dígitos decimais e formatado usando o separador de milhar. Para obter detalhes, confira [Excesso de casas decimais na propriedade de Tamanho (MB)](https://feedback.azure.com/forums/908035/suggestions/34379308).
- Corrigido um problema que fazia com que a criação de um 'índice espacial' falhasse com um erro como 'Para realizar esta ação, defina a propriedade PartitionScheme'.
- Melhorias de desempenho secundárias no Pesquisador de Objetos para evitar a emissão de consultas extras, quando possível.

AS (Analysis Services):

- Corrigido um problema em que a análise de DAX gera uma exceção de o arquivo não encontrado.
- Atalho de voltar ao "Assistente de Implantação" adicionado ao Menu Iniciar.

Integration Services (IS):

- Corrigido um problema de lado a lado em que o Assistente de Implantação falha ao conectar-se ao SQL Server se o SQL Server 2019 e o SSMS 18.0 estão instalados no mesmo computador.
- Corrigido um problema em que a tarefa do plano de manutenção não pode ser editada durante a criação do plano de manutenção.
- Corrigido um problema em que o Assistente de Implantação trava quando o projeto em implantação é renomeado.
- Configuração de ambiente habilitada no recurso de agendamento do Azure-SSIS IR.


HADR/grupos de disponibilidade:

- Corrigido um problema em que as funções no Assistente de Grupos de Disponibilidade de Failover eram sempre exibidas como "Resolvendo".
- Corrigido um problema em que o SSMS mostrava avisos truncados no "Painel de AG".

Fazer backup/restaurar/anexar/desanexar o banco de dados:

- Corrigido um problema em que o Assistente "Anexar banco de dados" não exibia arquivos secundários que eram renomeados. Agora, o arquivo é exibido e um comentário sobre ele é adicionado (por exemplo, "Não encontrado"). Para obter detalhes, confira [anexo de banco de dados não exibindo arquivos secundários](https://feedback.azure.com/forums/908035/suggestions/32897434).


Suporte à Instância Gerenciada:

- Suporte aprimorado para logons do AAD (no Gerenciador do SSMS).
- Geração de script aprimorada para objetos de grupos de arquivos do SQL Server Management Objects.
- Interface do usuário aprimorada para credenciais e auditorias.


Assistente de Importação de DAC:

- Corrigido um problema em que o Assistente de importação de DAC não estava funcionando quando conectado usando o AAD.

Visualizador do XEvent:

- Corrigido um problema em que o Visualizador de XEvent falhava ao tentar agrupar os eventos usando as *Opções da Barra de ferramentas de Evento Estendido*.

Avaliação de Vulnerabilidades:

- Corrigido um problema em que os resultados da verificação não eram carregados corretamente.




## <a name="ssms-180-preview-4"></a>SSMS 18.0 (versão prévia 4)

Número de build: 15.0.18040.0<br>
Data de lançamento: 24 de setembro de 2018

A versão prévia 4 é a primeira versão prévia pública do SSMS 18.0. Para a versão de GA (disponibilidade geral) mais recente do SSMS, [baixe e instale o SSMS 17.9](#ssms-179-latest-ga-release).

### <a name="whats-new"></a>Novidades

**SSMS geral**

Menor tamanho de download:

- O tamanho atual do pacote é menor que a metade do tamanho do SSMS 17.x (~400 MB). Em algum momento, o tamanho aumentará quando os componentes do IS (Integration Services) forem adicionados de volta, mas ele não deve ser tão grande como costumava ser.

O SSMS 18.x é baseado no novo Shell Isolado do Visual Studio 2017:

- Essa alteração significa que se trata de um shell moderno (escolhemos o Visual Studio 2017 15.6.4). O novo shell desbloqueia todas as correções de acessibilidade que ocorreram no SSMS e no Visual Studio.

Melhorias de acessibilidade:

- Foi trabalhoso solucionar problemas de acessibilidade em todas as ferramentas (SSMS, DTA e Criador de Perfil).

O SSMS pode ser instalado em uma pasta personalizada:

- Atualmente, isso só está disponível na instalação da linha de comando. Passe esse argumento extra para SSMS-Setup-ENU.exe:

  `SSMSInstallRoot=C:\MySSMS18`

  Por padrão, o novo local de instalação do SSMS é: `%ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`
  
  > [!NOTE]
  > Isso não significa que o SSMS tem várias instâncias.

O SSMS não mais compartilha componentes com o mecanismo do SQL:

- Empenhamos muito esforço para evitar o compartilhamento de componentes do mecanismo de SQL, que frequentemente resultava em problemas de facilidade de manutenção do SQL ou instalações do SSMS substituindo arquivos instalados pelo outro.

Agora, o SSMS requer o NetFx 4.7.2 ou superior:

- Atualizamos nosso requisito mínimo do NetFx4.6.1 para NetFx4.7.2: essa alteração permite tirar proveito das novas funcionalidades expostas pela nova estrutura.

Não há suporte para o SSMS no Windows 8. O Windows 10/Windows Server 2016 requer a versão 1607 (10.0.14393) ou posterior:
  
- Devido à nova dependência no NetFx 4.7.2, o SSMS 18.0 não é instalado no Windows 8, nas versões mais antigas do Windows 10 e do Windows Server 2016. A configuração do SSMS é bloqueada nesses sistemas operacionais. Ainda há suporte para o Windows 8.1.

O SSMS não é adicionado à variável de ambiente PATH:

- O caminho para SSMS. EXE (e ferramentas em geral) não é mais adicionado ao caminho. Os usuários podem adicionar por conta própria ou, se usarem um Windows moderno, confiar no menu Iniciar.

Compatível com [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

- Esta é a primeira versão do SSMS totalmente *ciente* do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (compatLevel 150, etc).
- Compatível com "BATCH_STARTED_GROUP" e "BATCH_COMPLETED_GROUP" no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] e na Instância Gerenciada no SSMS.
- GraphDB: adicione o sinalizador no plano de execução para a sequência de TC do Graph.
- Always Encrypted: foi adicionado suporte para [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).
  - A caixa de diálogo Conexão tem uma nova guia "Always Encrypted" quando o usuário clica no botão "Opções" para habilitar e configurar o suporte de enclave.

IDs de pacote não são mais necessárias para desenvolver extensões do SSMS:

- O SSMS estava carregando seletivamente apenas os pacotes conhecidos, exigindo que os desenvolvedores registrem seus próprios pacotes. Esse não é mais o caso.

Melhor suporte de SQL do Azure:

- Agora, as propriedades de banco de dados de SLO/edição/MaxSize aceitam nomes personalizados, facilitando o suporte a edições futuras do Banco de Dados SQL do Azure.
- Suporte adicionado para SKUs do vCore (Uso Geral e Comercialmente Crítico): Gen4_24 e todas da Gen5.

SMO:

- Estenda o suporte do SMO para a criação de índice retomável.
- Adicionado novo evento em objetos SMO ("PropertyMissing") para ajudar os autores de aplicativos a detectar problemas de desempenho do SMO mais rapidamente.
- A nova propriedade *DefaultBackupChecksum* foi exposta no objeto de configuração que mapeia para a configuração do servidor "padrão de soma de verificação de backup".

SSMS:

- Expor a opção de configuração AUTOGROW_ALL_FILES para grupos de arquivos no SSMS
- As opções de risco "lightweight pooling" e "aumento de prioridade" foram removidas da GUI do SSMS (https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended).
- O Editor SQL respeita o atalho **CTRL+D** para duplicar linhas (https://feedback.azure.com/forums/908035-sql-server/suggestions/32896594).
- Novo menu e associações de teclas para criar arquivos: **CTRL+ALT+ N**. **CTRL+N** continua a criar uma nova consulta.
- Agora, a caixa de diálogo **Nova Regra de Firewall** permite que o usuário especifique um nome de regra, em vez de gerar um automaticamente (https://feedback.azure.com/forums/908035-sql-server/suggestions/32902039).
- Classificação de dados: recomendações atualizadas.
- IntelliSense aperfeiçoado no Editor, especialmente para v140 T-SQL.
- Suporte a todos os idiomas da camada 1.
- Adicionado suporte na interface do usuário do SSMS para UTF-8 na caixa de diálogo de ordenação.
- Alterado para "Gerenciador de credenciais do Windows" para senhas MRU da caixa de diálogo de conexão. Isso resolve um problema antigo em que a persistência de senhas nem sempre era confiável (https://feedback.azure.com/forums/908035-sql-server/suggestions/32896486).
- O suporte para DPI alto é habilitado por padrão.
- Suporte aprimorado para sistemas com vários monitores, garantindo que cada vez mais caixas de diálogo e janelas sejam exibidas no monitor esperado.
- A configuração do servidor "padrão de soma de verificação de backup" foi exposta na nova página de configurações do banco de dados da caixa de diálogo Propriedades do Servidor. (https://feedback.azure.com/forums/908035-sql-server/suggestions/34634974).


SSMS/ShowPlan:

- Adicionado tempo real decorrido, linhas reais versus estimativa no nó do operador ShowPlan se elas estiverem disponíveis. Essa alteração faz com que o plano real pareça consistente com o plano de Estatísticas de Consulta ao Vivo.
- Dica de ferramenta modificada e comentário adicionado ao clicar no botão Editar Consulta para um ShowPlan, para indicar ao usuário que o ShowPlan poderá ser truncado pelo mecanismo do SQL se a consulta tiver mais de 4.000 caracteres.
- Adicionada lógica para exibir o "operador Materializer (seleção externa)".
- Adicione o atributo BatchModeOnRowStoreUsed de plano de execução para identificar facilmente as consultas que estão usando o recurso "verificação de modo de lote em rowstores". Sempre que uma consulta executa a verificação de modo de lote em rowstores, um novo atributo (BatchModeOnRowStoreUsed="true") é adicionado ao elemento StmtSimple.

Always On:

- RTO de nova operação de hash (tempo de recuperação estimado) e RPO (perda de dados estimada) no painel Always On do SSMS. Para obter detalhes, confira [Monitorar o desempenho de Grupos de Disponibilidade Always On](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md).

Arquivos de auditoria:

- O método de autenticação foi alterado de Chave de Conta de Armazenamento para a autenticação baseada no Azure AD.

Always Encrypted:

- Adicionada uma guia Always Encrypted na caixa de seleção *Habilitar Always Encrypted* (na caixa de diálogo *Conectar ao Servidor*), que agora fornece uma maneira fácil de habilitar/desabilitar o Always Encrypted para uma conexão de banco de dados.
- Várias melhorias foram feitas para dar suporte ao Always Encrypted com enclaves seguros:
  - Um campo de texto para especificar a URL de atestado de enclave na caixa de diálogo Conectar ao Servidor (a nova guia Always Encrypted).
  - A nova caixa de seleção na caixa de diálogo Nova Chave Mestra da Coluna para controlar se uma nova chave mestra da coluna permite cálculos de enclave.
  - Outras caixas de diálogo de gerenciamento de chaves do Always Encrypted agora expõem as informações sobre quais chaves mestras da coluna permitem cálculos de enclave.
  - Para conhecer detalhes, consulte [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).

        
### <a name="bug-fixes"></a>Correções de bugs

Panes/travamentos:

- Corrigida uma fonte de panes comuns do SSMS relacionados a objetos GDI
- Corrigida uma fonte comum de travamentos e desempenho ruim ao selecionar "Script como Criar/Atualizar/Soltar" (buscas desnecessárias removidas dos objetos SMO)
- Corrigido um travamento que ocorria ao se conectar a um BD SQL do Azure usando MFA enquanto rastreamentos ADAL estão habilitados
- Corrigido um travamento (ou travamento percebido) nas Estatísticas de Consulta ao Vivo quando invocadas do Monitor de Atividade (o problema manifestado ao usar a autenticação do SQL Server com nenhum conjunto de "Informações de Persistência de Segurança").
- Corrigido um travamento ao selecionar "Relatórios" no Pesquisador de Objetos que pode se manifestar em conexões de alta latência ou não acessibilidade temporária dos recursos.

Caixa de diálogo Conexão:

- Habilitada a remoção de nomes de usuário da lista anterior de nome de usuário quando é pressionada a tecla DEL (https://feedback.azure.com/forums/908035/suggestions/32897632).

XEvent:

- Adicionadas duas colunas "action_name" e "class_type_desc" que mostram os campos de ID da ação e tipo de classe como cadeias de caracteres legíveis.
- Removido o limite de 1.000.000 eventos do Visualizador de XEvent do evento.

Tabelas externas:

- Suporte adicionado para `Rejected_Row_Location` na grade de modelo, SMO, IntelliSense e propriedade.

Opções do SSMS:

- Corrigido um problema em que a página **Ferramentas > Opções > Pesquisador de Objetos do SQL Server > Comandos** não era redimensionada corretamente.


Editor do SSMS:

- Corrigido um problema na "Tabela do sistema SQL" em que restaurar as cores padrão estava mudando a cor para verde-limão, em vez de verde padrão, dificultando a leitura em uma tela de fundo branco (https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906).
- Correção o problema em que o IntelliSense não estava funcionando quando conectado ao SQL DW do Azure usando a autenticação do AAD.
- IntelliSense corrigido no Azure quando o usuário não tem acesso mestre.
- Correção de trechos de código para criar "tabelas temporais" que foram perdidas quando a ordenação do banco de dados de destino diferenciava maiúsculas de minúsculas.

Pesquisador de Objetos:

- Corrigido um problema em que o SSMS gerava uma exceção como "Não foi possível converter o objeto de DBNull para outros tipos" ao tentar expandir o nó "Gerenciamento" no OE (DataCollector configurado incorretamente)
- Corrigido um problema em que a tecla DEL não estava funcionando ao renomear um nó (https://feedback.azure.com/forums/908035/suggestions/32910247 e outras duplicatas).
- Corrigido um problema em que o OE não estava ignorando aspas antes de invocar "Editar Top N...", causando confusão
- Corrigido um problema em que o assistente para "Importar Aplicativo da Camada de Dados" estava falhando ao iniciar da árvore de Armazenamento do Azure.
- Corrigido um problema em "Configuração do Database Mail" em que o status da caixa de seleção SSL não era persistente (https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541).
- Corrigido um problema em que o SSMS esmaecia a opção para fechar conexões existentes ao tentar restaurar o banco de dados com is_auto_update_stats_async_on
- Corrigido um problema em que clicar com o botão direito do mouse em nós no Pesquisador de Objetos (por exemplo, em "Tabelas", e esperar para executar uma ação, como filtrar tabelas acessando **Filtro > Configurações de Filtro**, o formulário de configurações de filtro podia aparecer na outra tela, em vez de onde o SSMS está ativo no momento) (https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106).
- Corrigido um problema antigo em que a tecla DELETE não estava funcionando no Pesquisador de Objetos durante a tentativa de renomear um objeto (https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510).
- Ao exibir as propriedades de arquivos de banco de dados existentes, o tamanho é exibido em uma coluna "Tamanho (MB)" em vez de "Tamanho inicial (MB)", que é o exibido durante a criação de um banco de dados (https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024).
- Item de menu de contexto "Design" desabilitado em "Tabelas de Grafo", pois não há suporte para esse tipo de tabela na versão atual do SSMS.

        
Visualizador da Ajuda:

- Melhoria da lógica para respeitar os modos online/offline.
- Correção de "Exibir Ajuda" para respeitar as configurações online/offline (https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791).
    
Script de objeto:

- Em geral, melhorias de desempenho – gerar scripts de WideWorldImporters leva metade do tempo em comparação com o SSMS 17.7.
- Ao executar o script de objetos, a configuração no escopo do banco de dados que tem valores padrão é omitida.
- Não gere o T-SQL dinâmico ao executar o script (https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391).
- Omita a sintaxe de grafo "como borda" e "como nó" ao executar script de uma tabela no SQL Server 2016 e anteriores.


Designer de Tabela:

- Corrigida uma falha em "Editar 200 linhas".
- Corrigido um problema em que o designer permitia adicionar uma tabela quando conectado a um Banco de Dados SQL do Azure.

SMO:

- Corrigido um problema em que o SMO/ServerConnection não conseguia tratar conexões baseadas em SqlCredential corretamente (https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941).

AS:

- Corrigido um problema em que as "Configurações Avançadas" na interface do usuário de AS XEvent estavam cortadas

Assistente de Importação de arquivo simples:

- Corrigido um problema em que o "Assistente Importar arquivo simples" não estava manipulando aspas duplas corretamente (ignorando).
- Corrigido um problema relacionado ao tratamento incorreto de tipos de ponto flutuante (em localidades que usam um delimitador diferente para pontos flutuantes)
- Corrigido um problema relacionado à importação de bits quando os valores são 0 ou 1 (https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535).
- Corrigido um problema em que as flutuações foram inseridas como valores nulos.
        
Classificação de dados:

- Corrigido um problema de instalação que fazia com que a parte de recomendação de classificação de dados não funcionasse com a nova instalação.

Fazer backup/restaurar/anexar/desanexar o banco de dados:

- Corrigido um problema em que o usuário não conseguia anexar um banco de dados quando o nome do arquivo físico do arquivo .mdf não coincide com o nome do arquivo original.
- Corrigido um problema em que o SSMS podia não encontrar um plano de restauração válido ou podia encontrar um abaixo do ideal (https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752).
- Corrigida uma falha no SSMS ao tentar restaurar um backup de URL.

Monitor de Atividade de Trabalho:

- Falha corrigida ao usar o Monitor de Atividade do Trabalho (com filtros).
        
Suporte à Instância Gerenciada no SSMS:

- Melhoria no suporte para Instâncias Gerenciadas: opções sem suporte desabilitadas na interface do usuário e uma correção na opção Exibir Logs de Auditoria para lidar com o destino de auditoria da URL.
- O assistente "Gerar e publicar scripts" executa scripts de cláusulas CREATE DATABASE sem suporte.
- As Estatísticas de Consulta ao Vivo foram desabilitadas para instâncias de CL.
- Propriedades de banco de dados -> Arquivos estava executando incorretamente scripts ALTER DB ADD FILE.
- Corrigida a regressão com o agendador do SQL Agent em que o agendamento ONIDLE era escolhido, mesmo quando algum outro tipo de agendamento era escolhido.
- Ajuste de MAXTRANSFERRATE, MAXBLOCKSIZE para fazer backups no Armazenamento do Azure.
- O problema em que o backup da parte final do log é inserido no script antes da operação RESTORE (não há suporte para isso no CL).
- O Assistente para Criar Banco de Dados não executava script corretamente da instrução CREATE DATABASE.
- Corrigido um problema em que um erro era exibido durante a tentativa de usar o "Monitor de Atividade" quando conectado a Instâncias Gerenciadas.


Banco de Dados SQL do Azure:

- Corrigido um problema em que a lista de banco de dados não era preenchida corretamente para a janela de consulta de BD SQL do Azure quando conectado a um banco de dados de usuário no BD do SQL do Azure em vez de conectado ao mestre.
- Corrigido um problema em que não era possível adicionar uma "tabela temporal" a um Banco de Dados SQL do Azure.


Suporte geral de SQL do Azure:

- Problemas corrigidos em controle comum da interface do usuário do Azure que impedia o usuário de exibir as assinaturas do Azure (se houvesse mais de 50). Além disso, a classificação foi alterada para ser por nome em vez de usar ID de assinatura. O usuário pode usar essa opção ao tentar restaurar um backup de URL, por exemplo.
- Corrigido um problema no controle comum de interface do usuário do Azure ao enumerar as assinaturas que poderiam emitir um erro de "Índice fora do intervalo. Deve ser não negativo e menor que o tamanho da coleção." quando o usuário não tinha nenhuma assinatura em alguns locatários. O usuário pode usar essa opção ao tentar restaurar um backup de URL, por exemplo.

Grade de resultados:

- Corrigido um problema que usava o modo de Alto Contraste (números de linha selecionada não visível).

XEvent Profiler:

- Corrigido um problema em que o XEvent Profiler falhava ao iniciar quando conectado a um SQL Server de 96 núcleos.


### <a name="deprecated-features"></a>Recursos preteridos

Os seguintes recursos não estão mais disponíveis no SSMS:

- Depurador do T-SQL
- Diagramas de banco de dados
- OSQL.EXE
- Interface do usuário de administrador de Dreplay
- Ferramentas do Configuration Manager:
  - O SQL Server Configuration Manager e o Reporting Server Configuration Manager não mais fazem parte da instalação do SSMS.

- Políticas padrão de DMF
  - As políticas não são mais instaladas com o SSMS. Elas são movidas para o Git. Se desejarem, os usuários poderão contribuir e baixar/instalar as políticas.

- Opção de linha de comando -P do SSMS removida
  - Devido a questões de segurança, a opção para especificar senhas de texto não criptografado na linha de comando foi removida.

- Gerar scripts | O recurso Publicar no serviço Web removido. Este recurso (preterido) foi removido da interface do usuário do SSMS.

- Nó "manutenção | herdado" removido no Pesquisador de Objetos. Em Gerar e publicar scripts | A opção Publicar no serviço Web foi removida. Os nós "Plano de manutenção de banco de dados" e "SQL Mail" *antigos* não estarão mais acessíveis. Os nós "Database Mail" e "Planos de manutenção" modernos continuam funcionando normalmente.

### <a name="known-issues"></a>Problemas conhecidos

Os seguintes problemas são conhecidos na versão atual:

> [!IMPORTANT]
> Ao usarem a autenticação do *Active Directory – Universal com suporte MFA* com o editor de consultas SQL, os usuários podem enfrentar um problema em que a conexão é fechada e reaberta a cada invocação de consulta. Os efeitos colaterais desse fechamento incluem tabelas temporárias globais que são descartadas inesperadamente e, às vezes, um novo SPID fornecido para a conexão. Esse fechamento não ocorrerá se houver uma transação em aberto na conexão. Para contornar esse problema, os usuários podem definir `persist security info=true` nos parâmetros de conexão.

SSMS

- Clicar duas vezes em um arquivo .sql inicia o SSMS, mas não abre o script real.
  - Solução alternativa: arraste e solte o arquivo .sql para o editor do SSMS.

SSIS

- O pacote não pode ser implantado nem executado com êxito quando tem como alvo o SQL Server da versão antiga e contém o componente de Tarefa Script/Script ao mesmo tempo.
- O SSMS não pode se conectar ao Integration Services remoto.


## <a name="ssms-1791-latest-ga-release"></a>SSMS 17.9.1 (versão mais recente de GA)

![baixar](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- Número da versão: 17.9.1<br>
- Número de build: 14.0.17289.0<br>
- Data de lançamento: 21 de novembro de 2018

A versão 17.9.1 é uma pequena atualização da versão 17.9 com as seguintes correções de bug:

- Corrigido um problema em que ao usarem a autenticação do "Active Directory – Universal com suporte MFA" com o editor de consultas SQL, a conexão é fechada e reaberta a cada invocação de consulta. Os efeitos colaterais do fechamento da conexão incluem tabelas temporárias globais que são descartadas inesperadamente e, às vezes, um novo SPID fornecido para a conexão.
- Corrigido um problema antigo em que o plano de restauração não localiza um plano de restauração ou gera um plano de restauração ineficiente em determinadas condições.
- Corrigido um problema no assistente "Importar Aplicativo da Camada de Dados", que poderia resultar em um erro quando conectado a um Banco de Dados SQL do Azure.



> [!NOTE]
> Versões do SSMS 17.x não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)








## <a name="ssms-179"></a>SSMS 17.9

![baixar](../ssdt/media/download.png) [SSMS 17.9](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409)

Número de build: 14.0.17285.0<br>
Data de lançamento: 4 de setembro de 2018

> [!NOTE]
> Versões do SSMS 17.x não localizadas para o inglês exigem o [pacote de atualização de segurança da base de dados 2862966](https://support.microsoft.com/kb/2862966) se a instalação for realizada em: Windows 8, Windows 7, Windows Server 2012 e Windows Server 2008 R2.

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40a)


### <a name="whats-new"></a>Novidades

**SSMS geral**


Plano de execução:

- O Plano de Execução Gráfico agora mostra os novos atributos de comentários de concessão de memória do modo de linha quando o recurso está ativado para um plano específico: IsMemoryGrantFeedbackAdjusted e LastRequestedMemory adicionados ao elemento XML de plano de consulta MemoryGrantInfo. Para saber mais sobre comentários de concessão de memória do modo de linha, confira [Processamento de consultas adaptável em bancos de dados SQL](https://docs.microsoft.com/sql/relational-databases/performance/adaptive-query-processing).

SQL do Azure: 

- Adição de suporte para SKUs vCore na criação de banco de dados do Azure. Para saber mais, confira [Modelo de compra baseado em vCore](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers#vcore-based-purchasing-model).
 

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**
    
Replication Monitor:

- Corrigido um problema que fazia com que o Replication Monitor (SqlMonitor.exe) não fosse iniciado (item Voz do usuário: https://feedback.azure.com/forums/908035-sql-server/suggestions/34791079).

Assistente Importar Arquivo Simples:

- Corrigido o link para a página de ajuda do diálogo "Assistente de Arquivo Simples" 
- Corrigido o problema em que o assistente não permitia alteração na tabela de destino quando a tabela já existia: isso permite aos usuários tentar outra vez sem precisar sair do assistente, excluir a tabela com falha e, em seguida, inserir novamente as informações no assistente (item Voz do Usuário: https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186).

Importar/Exportar o Aplicativo da Camada de Dados:

- Corrigido um problema (em DacFx) que causava falha na importação de um .bacpac, com uma mensagem como “Error SQL72014: .Net SqlClient Data Provider: Msg 9108, Level 16, State 10, Line 1 This type of statistics is not supported to be incremental. ” ao lidar com tabelas com partições definidas e sem índices.

IntelliSense:

- Corrigido um problema em que o preenchimento do intellisense não funcionava ao usar o AAD com MFA.

Pesquisador de Objetos:

- Corrigido um problema em que o “Diálogo Filtrar” era exibido em monitores aleatórios em vez de ser mostrado no monitor onde o SSMS estava em execução (sistemas com vários monitores).

SQL do Azure:

- Corrigido um problema relacionado à enumeração de bancos de dados em "Bancos de Dados Disponíveis", em que "mestre" não era exibido na lista suspensa quando conectado a um banco de dados específico.
- Corrigido um problema em que ocorria falha ao tentar gerar um script ("Dados" ou "Esquema e Dados") e, em seguida, havia conexão com o Banco de Dados SQL do Azure usando AAD com MFA.
- Corrigido um problema no Designer de Exibição (Exibições) em que não era possível selecionar "Adicionar Tabelas" na interface do usuário quando conectado a um Banco de Dados SQL do Azure.
- Corrigido um problema em que o Editor de Consultas do SSMS fechava e reabria conexões silenciosamente durante a renovação de tokens do MFA. Isso impede a ocorrência de efeitos colaterais desconhecidos para o usuário (como fechar uma transação e não reabri-la). A alteração adiciona o tempo de expiração do token à janela Propriedades. 
- Corrigido um problema em que o SSMS não forçava solicitações de senha para contas MSA importadas para o AAD com logon de MFA. 

Monitor de Atividade: 

- Corrigido um problema que fazia com que "Estatísticas de Consultas ao Vivo" parasse de responder quando eram iniciadas pelo Monitor de Atividade e a Autenticação do SQL era usada. 

Integração do Microsoft Azure: 

- Corrigido um problema em que o SSMS mostrava somente as primeiras 50 assinaturas (caixas de diálogo Always Encrypted, diálogos Fazer backup/Restaurar da URL etc…). 
- Corrigido um problema em que o SSMS lançava uma exceção ("Índice fora do intervalo") ao tentar entrar em uma conta do Microsoft Azure que não tivesse nenhuma conta de armazenamento (na caixa de diálogo Restaurar Backup da URL). 

Script de objeto: 

- Ao executar o script "Drop and Create", o SSMS agora evita gerar T-SQL dinâmico.
- Ao executar o script de um objeto de banco de dados, o SSMS agora não gerará script para definir as configurações com escopo do banco de dados se elas estiverem definidas como valores padrão.

Ajuda:

- Corrigido um problema pendente há muito tempo em que "Help on Help" não respeitava o modo online/offline.
- Ao clicar em “Ajuda | Projetos e Exemplos da Comunidade”, o SSMS agora abre o navegador padrão que aponta para uma página do Git e não mostra erros/avisos devido ao uso de um navegador antigo.

### <a name="known-issues"></a>Problemas conhecidos


> [!IMPORTANT]
> Ao usarem a autenticação do *Active Directory – Universal com suporte MFA* com o editor de consultas SQL, os usuários podem enfrentar um problema em que a conexão é fechada e reaberta a cada invocação de consulta. Os efeitos colaterais desse fechamento incluem tabelas temporárias globais que são descartadas inesperadamente e, às vezes, um novo SPID fornecido para a conexão. Esse fechamento não ocorrerá se houver uma transação em aberto na conexão. Para contornar esse problema, os usuários podem definir `persist security info=true` nos parâmetros de conexão.




## <a name="previous-ssms-releases"></a>Versões anteriores do SSMS

Baixe versões anteriores do SSMS clicando nos links de título nas seções a seguir:

## <a name="downloadssdtmediadownloadpng-ssms-1781httpsgomicrosoftcomfwlinklinkid875802"></a>![baixar](../ssdt/media/download.png) [SSMS 17.8.1](https://go.microsoft.com/fwlink/?linkid=875802)
*Um bug foi descoberto em 17.8, relacionado ao provisionamento de bancos de dados SQL, Portanto, o SSMS 17.8.1 substitui o 17.8.*

Número de build: 14.0.17277.0<br>
Data de lançamento: 26 de junho de 2018

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40a)


### <a name="whats-new"></a>Novidades

**SSMS geral**

Propriedades do banco de dados:

- Essa melhoria expõe a opção de configuração **AUTOGROW_ALL_FILES** para grupos de arquivos. Essa nova opção de configuração é adicionada em Propriedades de Banco de Dados > janela Grupos de Arquivos na forma de uma nova coluna (Crescimento Automático de Todos os Arquivos) das caixas de seleção para cada Grupo de arquivos disponível (exceto Filestream e Grupos de Arquivos com Otimização de Memória). O usuário pode habilitar/desabilitar AUTOGROW_ALL_FILES para determinado Grupo de arquivos ativando/desativando a caixa de seleção Autogrow_All_Files correspondente. Do mesmo modo, as opções **AUTOGROW_ALL_FILES** têm scripts corretamente aplicados ao usar scripts no banco de dados para criar/gerar scripts para o banco de dados (SQL2016 e posterior).
    
Editor SQL:

- Experiência aprimorada com o Intellisense no Banco de Dados SQL quando o usuário não tem acesso mestre.

Script:

- Melhorias de desempenho gerais, especialmente em conexões de alta latência.
    
**AS (Analysis Services)**

- Bibliotecas de cliente de Analysis Services e provedores de dados atualizados para a versão mais recente, que adicionou suporte para a nova autoridade do AAD Azure Governamental (login.microsoftonline.us).



### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**
    
Planos de manutenção:

- Foi corrigido um problema ao editar planos de manutenção com a Autenticação do Sql em que "Tarefa de Notificação do Operador" falhava ao usar a autenticação do SQL.
    
Script:

- Foi corrigido um problema em que ações PostProcess no SMO levam ao esgotamento de recursos e a falhas de logon do SQL
    
SMO:

- Foi corrigido um problema em que Table.Alter() falhará se for adicionada uma coluna com uma restrição padrão e a tabela já tiver dados. Para obter detalhes, confira [smo do sql server gerando restrição padrão embutida ao adicionar uma coluna a uma tabela contendo dados](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895625).
    
Always Encrypted:

- Foi corrigido um problema (em DacFx) que estava causando um erro de tempo limite de bloqueio ao habilitar Always Encrypted em uma tabela particionada
    

**AS (Analysis Services)**

- Foi corrigido um problema que ocorria ao ser modificada uma fonte de dados OAuth em um modelo de compatibilidade de nível de 1400 de Tabela do Analysis Services, que fazia com que as alterações em tokens OAuth não fossem atualizadas na fonte de dados.
- Foi corrigida uma falha no SSMS que pode ter ocorrido ao serem usadas algumas credenciais da fonte de dados inválidas ou editadas fontes de dados que não dão suporte à migração de Alterar Fonte de Dados no Power Query (por exemplo, Oracle) em modelos de compatibilidade de nível 1400 de Tabela do Analysis Services.


### <a name="known-issues"></a>Problemas conhecidos

- Clicar no botão *Script* após modificar qualquer propriedade do grupo de arquivos na janela *Propriedades* gera dois scripts: um script com uma instrução *USE <database>* e um segundo script com uma instrução *USE master*.  O script com *USE master* é gerado com erro e deve ser descartado. Execute o script que contém a instrução *USE <database>*.
- Algumas caixas de diálogo exibem um erro de edição inválida ao trabalhar com novas edições *Uso Geral* ou *Comercialmente Crítico* do Banco de Dados SQL do Azure.
- Pode ser observada alguma latência no visualizador XEvents. Este é um [problema conhecido no .NET Framework](https://github.com/Microsoft/dotnet/blob/master/releases/net472/dotnet472-changes.md#sql). Considere a possibilidade de atualizar para o NetFx 4.7.2.




## <a name="downloadssdtmediadownloadpng-ssms-177httpsgomicrosoftcomfwlinklinkid873126"></a>![baixar](../ssdt/media/download.png) [SSMS 17.7](https://go.microsoft.com/fwlink/?linkid=873126)

Número de build: 14.0.17254.0<br>
Data do lançamento: 09 de maio de 2018

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40a)


### <a name="whats-new"></a>Novidades

**SSMS geral**

Replication Monitor:   
- Agora, o Replication Monitor dá suporte ao registro de um ouvinte para cenários nos quais o banco de dados publicador e/ou o banco de dados distribuidor faz parte do grupo de disponibilidade. Agora você pode monitorar ambientes de replicação nos quais o banco de dados publicador e/ou o banco de dados de distribuição faz parte do Always On. 
 
SQL Data Warehouse do Azure: 
- Adicione suporte de localização da linha rejeitada a tabelas externas no SQL Data Warehouse do Azure. 

**IS (Integration Services)**

- Inclusão de um recurso de agendamento de pacotes SSIS implantado no Banco de Dados SQL do Azure. Ao contrário do SQL Server local e da Instância Gerenciada do Banco de Dados SQL, que tem o SQL Server Agent como um agendador de trabalhos de primeira classe, o Banco de Dados SQL não tem um agendador interno. Esse novo recurso do SSMS fornece uma interface do usuário familiar que é semelhante ao SQL Server Agent para agendar pacotes implantados no Banco de Dados SQL. Se você estiver usando o Banco de Dados SQL para hospedar o banco de dados de catálogo SSIS, o SSISDB, poderá usar esse recurso do SSMS para gerar os pipelines de data factory, as atividades e os gatilhos necessários para agendar pacotes do SSIS. Em seguida, você pode editar e estender esses objetos no data factory. Para obter mais informações, veja [Agendar execução de pacote SSIS no Banco de Dados SQL do Azure com SSMS](../integration-services/lift-shift/ssis-azure-schedule-packages-ssms.md). Para saber mais sobre pipelines do Azure Data Factory, atividades e gatilhos, veja [Pipelines e atividades no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities) e [Execução de pipelines e gatilhos no Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers).
- Suporte para o agendamento do pacote SSIS no SQL Agent na instância gerenciada do SQL. Agora é possível criar trabalhos do SQL Agent para executar pacotes SSIS na instância gerenciada. 

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral** 

Plano de manutenção:   
- Corrigido um problema em que a tentativa de alterar o agendamento de um plano de manutenção existente lançava uma exceção. Para obter detalhes, veja [Falha do SSMS 17.6 ao clicar em um agendamento em um plano de manutenção](https://feedback.azure.com/forums/908035-sql-server/suggestions/33712924).

Always On: 
- Corrigido um problema em que o painel de latência Always On não estava funcionando com o SQL Server 2012.
 
Script: 
- Corrigido um problema em que o script de procedimento armazenado no SQL Data Warehouse do Azure não está funcionando para o usuário não administrador.
- Corrigido um problema em que o script de um banco de dados no Banco de Dados SQL do Azure não gerava scripts das propriedades *SCOPED CONFIGURATION*.
 
Telemetria: 
- Corrigido o problema de falha no SSMS ao tentar se conectar a um servidor, depois de recusar sem enviar telemetria.
 
Banco de Dados SQL do Azure: 
- Corrigido um problema em que o usuário não conseguia definir nem alterar o nível de compatibilidade (na lista suspensa de vazio). Observação: para definir o nível de compatibilidade como 150, o usuário ainda precisa usar o botão *Script* e editar manualmente o script. 
 
SMO: 
- A configuração de tamanho do log de erros foi exposta no SMO. Para obter detalhes, veja [Definir o tamanho máximo dos logs de erros do SQL Server](https://feedback.azure.com/forums/908035-sql-server/suggestions/33624115).  
- Corrija o script de avanço de linha no SMO no Linux.
- Melhoria do desempenho de diversos ao recuperar propriedades usadas raramente.  

IntelliSense: 
- Melhoria do desempenho: volume reduzido de consultas do IntelliSense para dados de coluna. Isso é especialmente útil ao trabalhar em tabelas com grande número de colunas. 

Configurações do usuário do SSMS:
- Corrigido um problema em que a página de opções não era redimensionada corretamente.

Diversos:  
- Melhoria na exibição do texto na página *Detalhes de estatísticas*. 

**IS (Integration Services)**

- Melhor suporte à Instância Gerenciada do Banco de Dados SQL do Azure.
- Corrigido um problema em que o usuário não conseguia criar um catálogo para o SQL Server 2014 ou anterior.
- Dois problemas foram corrigidos com relatórios:
   - Nome do computador removido para servidores do Azure.
   - Melhor manipulação do nome de objeto localizada.


### <a name="known-issues"></a>Problemas conhecidos

Algumas caixas de diálogo exibem um erro de edição inválida ao trabalhar com novas edições *Uso Geral* ou *Comercialmente Crítico* do Banco de Dados SQL do Azure.

## <a name="downloadssdtmediadownloadpng-ssms-176httpsgomicrosoftcomfwlinklinkid870039"></a>![baixar](../ssdt/media/download.png) [SSMS 17.6](https://go.microsoft.com/fwlink/?linkid=870039)

Número de build: 14.0.17230.0<br>
Data do lançamento: 20 de março de 2018

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40a)

### <a name="whats-new"></a>Novidades

**SSMS geral**

Instância Gerenciada do Banco de Dados SQL:

- Suporte adicionado à [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance). A Instância Gerenciada do Banco de Dados SQL do Azure fornece quase 100% de compatibilidade com o SQL Server local, uma implementação [VNet (rede virtual)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) nativa que aborda questões comuns de segurança e um [modelo empresarial](https://azure.microsoft.com/pricing/details/sql-database/) favorável para clientes do SQL Server local.
- Suporte para cenários comuns de gerenciamento, como:
   - Criar e alterar bancos de dados.
   - Faça backup e restaure os bancos de dados.
   - Importar, exportar, extrair e publicar Aplicativos da Camada de Dados.
   - Exibir e alterar as propriedades do servidor.
   - Suporte completo para o Pesquisador de Objetos.
   - Gerando scripts de objetos de banco de dados.
   - Suporte para trabalhos do SQL Agent.
   - Suporte para servidores vinculados.
- Saiba mais sobre Instâncias Gerenciadas [aqui](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/).

Pesquisador de Objetos:
- Configurações adicionadas para não forçar colchetes em volta de nomes ao arrastar e soltar do Pesquisador de Objetos para a Janela de Consulta. (Sugestões do usuário [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) e [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051).)

Classificação de dados:
- Melhorias e correções de bug gerais.

**IS (Integration Services)**

- Suporte adicionado para implantar pacotes em uma [Instância Gerenciada do Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

Classificação de dados:

- Foi corrigido um problema na *Classificação de Dados que fazia com que classificações recém-adicionadas fossem exibidas com o *tipo de informação* e o *rótulo de confidencialidade* obsoletos.
- Foi corrigido um problema em que a *Classificação de Dados* não funcionava quando o objetivo era um servidor definido para uma ordenação que diferencia maiúsculas de minúsculas.
        
Always On:

- Foi corrigido um problema no Painel AG Show no qual clicar em *Coletar Dados de Latência* poderia causar um erro quando o servidor estava definido para uma ordenação que diferencia maiúsculas de minúsculas.
- Foi corrigido um problema em que o SSMS relatava incorretamente um AG como *Distribuído* quando o Serviço de cluster é desligado.
- Foi corrigido um problema ao criar o AG usando a caixa de diálogo *Criar Grupo de Disponibilidade* em que *ReadOnlyRoutingUrl* era obrigatório.
- Foi corrigido um problema em que quando o primário está inoperante e o failover para o secundário é feito manualmente, uma NullReferenceException é lançada.
- Foi corrigido um problema ao criar o Grupo de Disponibilidade usando backup/restauração para inicializar um banco de dados em réplicas secundárias, os arquivos de banco de dados são criados no diretório padrão. A correção inclui:
   - Adicionar o validador do diretório de dados/log.
   - Faça somente a realocação de arquivos quando a réplica está em um sistema operacional diferente da réplica primária.
- Foi corrigido um problema em que o Assistente do SSMS não gera a opção *CLUSTER_TYPE*, causando uma falha na junção secundária.

Programa de instalação:
- Foi corrigido um problema em que a tentativa de atualizar o SSMS instalando o “pacote de atualização” falhava quando o SSMS era instalado em um local diferente do padrão.

SMO:
- Foi corrigido um problema de desempenho no qual criar o script de tabelas no SQL Server 2016 e superior poderia levar até 30 segundos (agora leva menos de um segundo).

Pesquisador de Objetos:
- Foi corrigido um problema em que o SSMS poderia gerar uma exceção como “Não foi possível converter o objeto de DBNull para outros tipos” ao tentar expandir o nó *Gerenciamento* no Pesquisador de Objetos.
- Foi corrigido um problema em que *Iniciar PowerShell* não detectava o módulo SQLServer quando o perfil do PS definido pelo usuário emitia a saída.
- Foi corrigido um travamento intermitente que poderia ocorrer ao clicar com o botão direito do mouse em um nó Tabela ou Índice no Pesquisador de Objetos.

Database Mail:
- Foi corrigido um problema em que o *Assistente de Configuração do Database Mail* lançava uma exceção ao tentar exibir/gerenciar mais de 16 perfis.


**AS (Analysis Services)**

- Foi corrigido um problema no qual, ao modificar uma fonte de dados em um modelo de nível de compatibilidade 1400 no SSMS, as alterações não eram salvas no servidor.

**IS (Integration Services)**

- Foi corrigido um problema em que o SSMS não mostrava o nó de catálogo do SSIS e os relatórios quando conectado à Instância Gerenciada do Banco de Dados SQL

### <a name="known-issues"></a>Problemas conhecidos

> [!WARNING]
> Há um problema conhecido em que o SSMS 17.6 se torna instável e falha ao usar [Planos de Manutenção](../relational-databases/maintenance-plans/maintenance-plans.md). Se você usa Planos de Manutenção, não instale o SSMS 17.6. Faça downgrade para o SSMS 17.5 se você já tiver instalado o 17.6 e esse problema estiver afetando você. 



## <a name="downloadssdtmediadownloadpng-ssms-175httpsgomicrosoftcomfwlinklinkid867670"></a>![download](../ssdt/media/download.png) [SSMS 17.5](https://go.microsoft.com/fwlink/?linkid=867670)
Já disponível | Número de build: 14.0.17224.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40a)

### <a name="whats-new"></a>Novidades

**SSMS geral**

Descoberta e classificação de dados:

- Foi adicionado um novo recurso de descoberta e classificação de dados SQL para descobrir, classificar, rotular e relatar dados confidenciais nos bancos de dados. 
- A descoberta e a classificação automáticas dos dados mais confidenciais (de negócios, financeiros, de serviços de saúde, PII, etc.) podem desempenhar um papel fundamental na dimensão da proteção de informações organizacionais.
- Saiba mais em [SQL Data Discovery & Classification](../relational-databases/security/sql-data-discovery-and-classification.md) (Descoberta e classificação de dados SQL).

Editor de consultas:

- Foi adicionado o suporte para a opção SkipRows no Formato de arquivo externo de texto delimitado para o SQL DW do Azure. Esse recurso permite que os usuários ignorem um número especificado de linhas ao carregar arquivos de texto delimitados no SQL DW. Também foi adicionado o suporte do IntelliSense/SMO correspondente para a palavra-chave FIRST_ROW. 

Plano de execução:

- Foi habilitada a exibição do botão de plano estimado para o SQL Data Warehouse
- Foi adicionado um novo atributo de plano de execução *EstimateRowsWithoutRowGoal* e também foram adicionados novos atributos de plano de execução para *QueryTimeStats*: *UdfCpuTime* e *UdfElapsedTime*. Para obter mais informações, confira [Informações de meta de linha do otimizador no plano de execução de consulta adicionadas no SQL Server 2017 CU3](https://support.microsoft.com/help/4051361).



### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

Plano de execução:

- Foi corrigido o tempo decorrido das Estatísticas de Consultas Dinâmicas, para mostrar o tempo de execução do mecanismo em vez do tempo decorrido da conexão com as LQS.
- Foi corrigido um problema no qual o plano de execução não era capaz de reconhecer os operadores lógicos Apply, como GbApply e InnerApply.
- Foi corrigido um problema relacionado ao ExchangeSpill.

Editor de consultas:

- Foi corrigido um problema relacionado a SPIDs no qual o SSMS podia gerar um erro como "A cadeia de caracteres de entrada não estava no formato correto. (mscorlib)" ao executar uma consulta simples precedida por um "SET SHOWPLAN_ALL ON". 


SMO:

- Foi corrigido um problema em que o SMO não conseguia buscar as propriedades AvailabilityReplica quando a ordenação do servidor diferenciava maiúsculas de minúsculas (como resultado, o SSMS podia exibir uma mensagem de erro como "O identificador de várias partes ‘a.delimited’ não pôde ser associado".
- Foi corrigido um problema na classe DatabaseScopedConfigurationCollection, em que as ordenações eram tratadas incorretamente (como resultado, um SSMS em execução em um computador com um código de localidade turca podia exibir um erro como "A estimativa de cardinalidade herdada não é uma configuração de escopo válida" ao clicar com o botão direito do mouse em um banco de dados em execução em um servidor com uma ordenação com diferenciação de maiúsculas e minúsculas).
- Foi corrigido um problema na classe JobServer, no qual o SMO não conseguia buscar as propriedades do SQL Agent em um SQL Server 2005 (como resultado, o SSMS gerava um erro como, "Não é possível atribuir um valor padrão a uma variável local. É necessário declarar a variável escalar "\@ServiceStartMode", e, por fim, o nó do SQL Agent não era exibido no Pesquisador de Objetos).

Modelos: 

- “Database Mail”: foram corrigidos alguns erros de digitação [(https://feedback.azure.com/forums/908035/suggestions/33143512)](https://feedback.azure.com/forums/908035/suggestions/33143512).  

Pesquisador de Objetos:
- Foi corrigido um problema em que a Compactação Gerenciada falhava para os índices (https://feedback.azure.com/forums/908035-sql-server/suggestions/32610058-ssms-17-4-error-when-enabling-page-compression-o).

Auditoria do:
- Foi corrigido um problema com o recurso *Mesclar arquivos de auditoria*.
<br>

### <a name="known-issues"></a>Problemas conhecidos

Classificação de dados:
- Remover uma classificação e, em seguida, adicionar manualmente uma nova classificação para a mesma coluna resulta na atribuição do tipo de informações e do rótulo de confidencialidade antigos à coluna na exibição principal.<br>
*Solução alternativa*: atribuir o tipo de informações e rótulo de confidencialidade novos depois que a classificação for adicionada novamente à exibição principal e antes de salvar.


## <a name="downloadssdtmediadownloadpng-ssms-174httpsgomicrosoftcomfwlinklinkid864329"></a>![baixar](../ssdt/media/download.png) [SSMS 17.4](https://go.microsoft.com/fwlink/?linkid=864329)
Geralmente disponível| Número de build: 14.0.17213.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40a)


### <a name="whats-new"></a>Novidades

**SSMS geral**

Avaliação de Vulnerabilidades:
- Adicionado um novo serviço de Avaliação de Vulnerabilidade de SQL para verificar seus bancos de dados para possíveis vulnerabilidades e desvios das práticas recomendadas, como configurações incorretas, excesso de permissões e dados confidenciais expostos. 
- Os resultados da avaliação incluem etapas práticas para resolver cada problema e scripts de correções personalizadas quando aplicável. O relatório de avaliação pode ser personalizado para cada ambiente e ajustado de acordo com requisitos específicos. Saiba mais em [Avaliação de Vulnerabilidades SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Correção do problema no qual *HasMemoryOptimizedObjects gerava exceção no Azure.
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
- Adicionada uma nova opção de linha de comando ("-G") que pode ser usada para fazer com que o SSMS se conecte automaticamente a um servidor/banco de dados usando a Autenticação do Active Directory ("Integrado" ou "Senha"). Para obter detalhes, consulte [Utilitário de Ssms](ssms-utility.md).

Assistente Importar Arquivo Simples:
- Adicionada uma maneira de escolher um nome de esquema diferente do padrão ("dbo") ao criar a tabela.

Repositório de Consultas:
- Restaurado o relatório "Consultas Regredidas" ao expandir a lista de relatórios disponíveis do Repositório de Consultas.

**IS (Integration Services)**
- Função de validação de pacote adicionada no Assistente de Implantação, o que ajuda o usuário a descobrir componentes dentro de pacotes do SSIS que não têm suporte no Azure SSIS IR.

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

- Pesquisador de Objetos: corrigido um problema em que o nó de função com valor de tabela não aparecia para instantâneos de banco de dados – [Connect 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161).
Desempenho melhorado ao expandir o nó de *bancos de dados* quando o servidor tem bancos de dados de fechamento automático.
- Editor de consultas: corrigido um problema em que o IntelliSense falhava para usuários que não têm acesso ao banco de dados mestre.
Corrigido um problema que estava fazendo com que o SSMS falhasse em alguns casos, quando a conexão com um computador remoto era fechada – [Connect 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557).
- Visualizador de XEvent: funcionalidade habilitada novamente para exportar para XEL.
Problemas corrigidos em que, em alguns casos, o usuário não conseguia carregar um arquivo XEL inteiro.
- XEvent Profiler: corrigido um problema que estava fazendo com que o SSMS falhasse quando o usuário não tinha as permissões *VIEW SERVER STATE*.
Corrigido um problema em que fechar a janela de Dados dinâmicos do XE Profiler não parava a sessão subjacente.
- Servidores registrados: corrigido um problema em que o comando "Mover para..." parava de funcionar – [Connect 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) e [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/).
- SMO: corrigido um problema em que o método TransferData no objeto Transferir não estava funcionando.
Corrigido um problema em que os bancos de dados do Servidor lançavam a exceção para bancos de dados SQL DW em pausa.
Corrigido um problema em que o script de banco de dados SQL no SQL DW gerava valores incorretos de parâmetro T-SQL.
Corrigido um problema em que o script de um banco de dados ampliado emitia incorretamente a opção *DATA\_COMPRESSION*.
- Monitor de Atividade do Trabalho: corrigido um problema em que o usuário recebia o erro "O índice está fora do intervalo. Deve ser não negativo e menor que o tamanho da coleção. 
      Nome do parâmetro: índice (System.Windows.Forms) "ao tentar filtrar por categoria – [Connect 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691).
- Caixa de diálogo Conexão: corrigido um problema em que os usuários de domínio sem acesso a um controlador de domínio de Leitura/Gravação não podiam fazer conectar-se a um SQL Server usando a autenticação do SQL – [Connect 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381).
- Replicação: corrigido um problema em que um erro semelhante a "Não é possível aplicar o valor 'null' à propriedade ServerInstance" era exibido ao olhar as propriedades de uma assinatura pull no SQL Server.
- Instalação do SSMS: corrigido um problema em que a instalação do SSMS fazia com que todos os produtos instalados no computador fossem reconfigurados incorretamente.
- Configurações do Usuário:
   - Com essa correção, os usuários de nuvem soberana do governo dos EUA têm acesso ininterrupto a seus recursos de Banco de Dados SQL do Azure e Azure Resource Manager com SSMS por meio de autenticação Universal e logon do Azure Active Directory.  Os usuários de versões anteriores do SSMS precisavam abrir Ferramentas|Opções|Serviços do Azure e, em Gerenciamento de Recursos, alterar a configuração da propriedade “Autoridade do Active Directory” para https://login.microsoftonline.us.

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



## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>![baixar](../ssdt/media/download.png) [SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904)
Geralmente disponível| Número de build: 14.0.17199.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


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
  - Agora a interface do usuário do Repositório de Consultas expõe a categorização de esperas em todos os relatórios existentes. Isso permite que os clientes desbloqueiem os cenários das Principais consultas de espera e muitos outros.
- Realização da inclusão dos cabeçalhos dos parâmetros de script opcionais (desativada por padrão; pode ser habilitada nas configurações do usuário em “Ferramentas > Opções > Pesquisador de Objetos do SQL Server > Script > Incluir cabeçalho dos parâmetros de script”) – [Item do Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Marca "RC" removida.

### <a name="bug-fixes"></a>Correções de bugs

**SSMS geral**

- XEvent: 
   - Correção do problema em que o SSMS abre apenas parte dos eventos no arquivo .xel.
   - Melhoria na experiência "Observar dados dinâmicos" quando o banco de dados padrão não é "mestre" – [Item do Connect 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582).
- Always On: correção do problema em que "Restaurar backups de log" pode falhar com o erro "O sinal deste conjunto de backup termina em LSN x, o que é muito cedo para ser aplicado ao banco de dados".
- Monitor de atividade de trabalho: correção de ícones inconsistentes – [Item do Connect 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100).
- Repositório de Consultas: correção do problema em que o usuário não pode escolher o intervalo de datas "personalizado" para relatórios do Repositório de Consultas. Vinculado aos itens do Connect abaixo.
   - [Item do Connect 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Item do Connect 3139399](https://connect.microsoft.com/SQLServer/feedback/details/3139399)
- Correção do problema no qual a caixa de diálogo de conexão não “limpa” o banco de dados usado mais recentemente quando as informações salvas têm um banco de dados nomeado e quando o usuário seleciona <default>.
- Script de objeto: correção de um problema no qual "Gerar script de banco de dados" não está funcionando e está gerando um erro quando o usuário tem um banco de dados DW em pausa no servidor, mas selecionou outro banco de dados que não é do DW e tentou gerar o script dele.
Correção de um problema no qual o cabeçalho dos Procedimentos armazenados com script não estava correspondendo às configurações do script, resultando em um script incorreto – [Item do Connect 3139784](https://connect.microsoft.com/SQLServer/feedback/details/3139784).
Habilitação nova do "botão de Script" ao direcionar objetos do SQL Azure.
  Correção do problema no qual o SSMS não estava permitindo scripts para "Alterar" ou "Executar" em alguns objetos (UDF, Exibição, SP, Gatilho) quando conectado a um Banco de Dados SQL do Azure – [Item do Connect 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386).
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
- Correção de um problema com a classe de Transferência do SMO no qual ela não transferia os objetos da Fonte de Dados Externa nem do Formato de Arquivo Externo. Agora, os objetos desses tipos devem ser corretamente incluídos na transferência.
- Servidores registrados:
   - Habilitação da consulta multisservidor para servidores do agente do usuário (ela tenta usar o mesmo token para todo servidor do agente do usuário no grupo).
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
- Agora o Assistente de implantação pode ser implantado no AS Azure ao ser executado na linha de comando.
- Ao usar a Autenticação do Windows no AS Azure, agora o usuário verá o nome da conta de usuário no Pesquisador de Objetos corretamente.


### <a name="known-issues-in-this-173-release"></a>Problemas conhecidos nesta versão 17.3:

**SSMS geral**

- A funcionalidade SSMS a seguir não é compatível com a autenticação do Azure AD usando o agente do usuário com MFA:
   - O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com a autenticação do Azure AD. Há um problema conhecido em que a mensagem de erro apresentada ao usuário está um pouco ambígua "Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…" em vez da esperada "O Orientador de Otimização do Mecanismo de Banco de Dados não é compatível com o Banco de Dados SQL do Microsoft Azure. (DTAClient)”.
- A tentativa de analisar uma consulta nos resultados do DTA resulta em erro: "o objeto deve implementar IConvertible. (mscorlib)".
- *Consultas retornadas* está ausente na lista de relatórios do Repositório de Consultas no Pesquisador de Objetos.
   - Solução alternativa: clique com o botão direito do mouse no nó **Repositório de Consultas** e selecione **Exibir consultas retornadas**.

**IS (Integration Services)**

- O [execution_path] em [catalog]. [event_messagea] não está correto para execuções de pacote no Scale Out. O [execution_path] começa com "\Package" em vez do nome do objeto do executável do pacote. Ao exibir o relatório de visão geral de execuções de pacote no SSMS, o link do "Caminho de Execução" na Visão Geral de Execução não funciona. A solução alternativa é clicar em "Exibir Mensagens" no relatório de visão geral para verificar todas as mensagens do evento.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![baixar](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
Disponibilidade geral | Número de build: 14.0.17177.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

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
- Além disso, uma nova interface de CLI foi entregue com suporte para a configuração de administrador do Azure AD para o Banco de Dados SQL e SQL Data Warehouse.

 Para obter mais informações sobre os métodos de autenticação do Active Directory, consulte [Autenticação universal com o banco de dados SQL e SQL Data Warehouse (suporte de SSMS para MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) e [configure a autenticação multifator do Banco de Dados SQL do Azure para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- A janela de saída tem entradas para consultas executadas durante a expansão de nós do Pesquisador de Objetos do SQL Server
- Designer de exibição do Banco de dados SQL do Azure habilitado
- As opções de script padrão para gerar scripts de objetos no Pesquisador de Objetos do SQL Server no SSMS foram alteradas:
  - Anteriormente, o padrão em uma nova instalação era que o script gerado utilizava a versão mais recente do SQL Server (atualmente SQL Server 2017).
  - No SSMS 17.2, uma nova opção foi adicionada: *Corresponder configurações de script com a origem*. Quando definido como *True*, o script gerado utiliza a mesma versão, o tipo de mecanismo e edição do mecanismo que o servidor de onde o objeto que está sendo inserido no script veio.
  - O valor de *Corresponder configurações de script com a origem* é definido como *True* por padrão, portanto, novas instalações do SSMS serão automaticamente padronizadas para sempre gerar scripts de objetos com o mesmo destino do servidor original.
  - Quando o valor de *Corresponder configurações de Script com a origem* estiver definido como *False*, as opções de destino do script normal serão habilitadas e funcionarão como antes.
Além disso, todas as opções de script foram movidas para sua própria seção – *Opções de versão*. Elas não estão mais em *Opções Gerais de Script*.

- Suporte adicionado para as Nuvens nacionais em "Restaurar de URL"
- Os relatórios do QueryStoreUI agora dão suporte a métricas adicionais (RowCount, DOP, CLR Time etc.) do sys.query_store_runtime_stats.
- Agora há suporte para o IntelliSense para o Banco de Dados SQL do Azure https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
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
  - Não há suporte para o **Orientador de Otimização do Mecanismo de Banco de Dados** para autenticação do Azure AD. Há um problema conhecido em que a mensagem de erro apresentada ao usuário não ajuda muito: *Não foi possível carregar o arquivo ou assembly 'Microsoft.IdentityModel.Clients.ActiveDirectory,…* em vez da esperada *O Orientador de Otimização do Mecanismo de Banco de Dados não dá suporte ao Banco de Dados SQL do Microsoft Azure. (DTAClient)*.

**AS (Analysis Services)**

- Pesquisador de Objetos do SQL Server no SSAS não mostrará o nome de usuário de autenticação do Windows nas propriedades de conexão do AS Azure.

### <a name="bug-fixes"></a>Correções de bugs

- Corrigido um problema ao tentar imprimir os resultados de uma consulta (como texto).  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- Corrigido um problema em que o SSMS descartava incorretamente tabelas e outros objetos ao gerar o script de exclusão desses objetos em um banco de dados do SQL Azure.
- Corrigido um problema em que o SSMS ocasionalmente se recusava a iniciar com um erro como "Não é possível localizar um ou mais componentes. Reinstale o aplicativo"
- Foi corrigido um problema em que o SPID na interface do usuário do SSMS poderia ficar obsoleto e fora de sincronia. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- Corrigido um problema na instalação do SSMS (silencioso) em que o argumento /passive era tratado como /quiet.
- Corrigido um problema em que o SSMS ocasionalmente gera um erro de "Referência de objeto não definida para uma instância do objeto" na inicialização. https://connect.microsoft.com/SQLServer/feedback/details/3134698
- Corrigido um problema no "Assistente de compactação de dados" que estava fazendo com que o SSMS falhasse ao pressionar 'Calcular' na Tabela de gráfico
- Corrigido um problema de desempenho ao clicar com o botão direito do mouse em um índice para uma tabela (com uma conexão lenta com a Internet). https://connect.microsoft.com/SQLServer/feedback/details/3120783
- Corrigido um problema em que o SSMS não enumerava arquivos de backup em servidores com uma ordenação que diferencia maiúsculas de minúsculas. https://connect.microsoft.com/SQLServer/feedback/details/3134787 e https://connect.microsoft.com/SQLServer/feedback/details/3137000
- Diversas correções de plano de execução e comparação de plano de execução
- Corrigido um problema em que a caixa de diálogo de Conexão não permitia que o usuário especificasse o "Protocolo de rede" a ser usado para a conexão, a menos que o SQL Server estivesse instalado no computador que executa o SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- Suporte aprimorado para as configurações de vários monitores em que algumas caixas de diálogo do SSMS apareciam em locais "aleatórios". Adicionada uma nova opção de "Caixas de diálogo de tarefa" nas configurações do usuário "Pesquisador de Objetos do SQL Server | Comandos"para permitir lembrar a posição da caixa de diálogo de uma tarefa ou folha de propriedades quando ela for fechada. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- Corrigido um problema em que o SSMS não conseguia alterar as propriedades de banco de dados para o banco de dados SQL criptografado do Azure
- Opção "Descartar resultados após a execução" melhorada. https://connect.microsoft.com/SQLServer/feedback/details/1196581
- Melhorado/corrigido o problema em que os usuários não conseguiam acessar as assinaturas do Azure para as quais eles não são administradores.
- Assistente "Restauração de banco de dados" aprimorado para manter o banco de dados de destino selecionado no OE independentemente da seleção de banco de dados de origem. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- Corrigido um problema em que o Pesquisador de Objetos do SQL Server não classificava "procedimentos armazenados compilados nativamente" recém-adicionados incorretamente. https://connect.microsoft.com/SQLServer/feedback/details/3133365
- Corrigido um problema em que "SELECT TOP n ROWS" não incluía a cláusula "TOP". Para Azure SQLDW. https://connect.microsoft.com/SQLServer/feedback/details/3133551 e https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: corrigido o problema em que intervalos de tempo não personalizados não funcionavam corretamente para todos os relatórios.
- Always Encrypted: melhoria das mensagens para status de permissão do AKV nas dicas de ferramenta Adicionado da caixa de diálogo Novo CMK à lista suspensa CEK para facilitar a distinção de CEKs com nomes longos. Corrigido um problema em que alguns provedores de repositório da chave CNG não seriam exibidos na caixa de diálogo Nova Chave Mestra da Coluna para Always Encrypted
- Corrigido "Nome do aplicativo" inconsistente para conexões de SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3135115
- Corrigido um problema em que SSMS não gerava scripts corretos para o SQL Azure (tabelas e índices com opção DATA_COMPRESSIONS). https://connect.microsoft.com/SQLServer/feedback/details/3133148
- Corrigido um problema em que o usuário não podia usar o atalho CTRL + Q para Início rápido (Observação: as novas associações de tecla para alternar a opção "IntelliSense habilitado" no Editor de consultas agora são CTRL + B, CTRL + I. https://connect.microsoft.com/SQLServer/feedback/details/3131968
- Corrigido um problema em "Restaurar banco de dados" em que o SSMS lançava uma exceção ao tentar selecionar uma conta de armazenamento de uma assinatura que tinha contas com domínios personalizados definidos
- Corrigido um problema em "Diagrama de banco de dados" em que o SSMS gerava um erro externo "O índice estava fora dos limites da matriz"; Além disso, o usuário não conseguia alterar a "Exibição de tabela" para qualquer, exceto padrão. https://connect.microsoft.com/SQLServer/feedback/details/3133792 e https://connect.microsoft.com/SQLServer/feedback/details/3135326
- Corrigido um problema em "Backup/restauração de URL" em que o SSMS não enumerava contas de armazenamento clássicas.
- Corrigido um problema em que uma exceção era lançada ao tentar adicionar protegíveis associados a esquema a funções de banco de dados. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- Corrigido um problema em que o SSMS exibia intermitentemente o erro "Dados são Null. Não é possível chamar este método ou esta propriedade em valores Null”. ao expandir um nó de tabela https://connect.microsoft.com/SQLServer/feedback/details/3136283
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

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>![baixar](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819)
Disponibilidade geral | Número de build: 14.0.17119.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

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

## <a name="downloadssdtmediadownloadpng-ssms-170httpsgomicrosoftcomfwlinklinkid847722"></a>![baixar](../ssdt/media/download.png) [SSMS 17.0](https://go.microsoft.com/fwlink/?LinkID=847722)
Disponibilidade geral | Número de build: 14.0.17099.0

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40a)

### <a name="enhancements"></a>Aprimoramentos 

- O pacote de atualização e as versões do WSUS (Windows Software Update Services) Future 17.X incluem um pacote de atualização cumulativa menor 
  - O pacote de atualização também será publicado no catálogo do WSUS  
- Ícones de atualizações foram atualizados para serem consistentes com ícones fornecidos do VS Shell e dar suporte a resoluções de alto DPI SSMS e ícones de programa do novo SSMS e Profiler para diferenciar entre as versões 16.X e 17.X
- Módulo do PowerShell no SQL
  - O módulo do SQL Server PowerShell foi removido do SSMS e agora é fornecido por meio da Galeria do PowerShell (o PowerShell 5.0 agora é necessário para compatibilidade com o controle de versão do módulo)
  - Diversas melhorias na “apresentação” (formatação) de alguns objetos SMO (por exemplo, agora os bancos de dados mostram o tamanho e o espaço disponível, enquanto as tabelas mostram a contagem de linhas e o uso de espaço)
  - Colorização adicionada quando o prompt de comando do PowerShell é invocado no menu “Iniciar o PowerShell” do OE
  - Adição do parâmetro -ClusterType e -RequiredCopiesToCommit aos cmdlets do AG (New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup e Set-SqlAvailabilityGroup)
  - Adição de parâmetros -ActiveDirectoryAuthority e -AzureKeyVaultResourceId ao cmdlet Add-SqlAzureAuthenticationContext
  - Foram adicionados os cmdlets Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase e Set-SqlAvailabilityReplicaRoleToSecondary
  - Foi adicionado o parâmetro -SeedingMode aos cmdlets Set-SqlAvailabilityReplica e New-SqlAvailabilityReplica
  - Foi adicionado o parâmetro -ConnectionString a Get-SqlDatabase
- Melhoria gerais no SQL Server em Linux e correções para o Envio de Logs
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
- Plano de execução Mostre o máximo em vez da soma nos threads na janela Propriedades de tempo decorrido Exponha novas propriedades de operador de concessão de memória Habilitação do botão "Editar Consulta" nas estatísticas de consulta em tempo real para execução intercalada
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
  - Adicionar suporte para novos tipos de cluster: EXTERNAL e NONE Adicionar suporte para SQL Server em Linux Adicionar a propagação automática como uma opção de sincronização de dados inicial Correção de alguns defeitos, por exemplo, de manuseio de URL de ponto de extremidade, atualização de banco de dados e layout da interface do usuário Removidos os recursos relacionados à réplica do Azure
  - O IntelliSense foi melhorado para várias palavras-chave do Grupo de Disponibilidade
- Monitor de Atividade
  - Foi adicionado o novo painel “Monitor de Atividades” à janela de saída do SSMS
  - Alteração da mensagem de erro/tempo limite de conexão para registrar informações na janela de saída em vez de uma mensagem de pop-up
  - Remoção de um gráfico vazio (5º gráfico) na seção Visão geral
  - Foi adicionado “(em pausa)” ao título da Visão geral se a coleta de dados do Monitor de Atividades estiver em pausa
  - Extensões Gráficas para o SQL Server Novos ícones para nó de grafo e tabelas de borda O nó de grafo e as tabelas de borda serão exibidos na pasta Tabelas de Grafo Modelos para criar nó de grafo e tabelas de borda estão disponíveis
- Modo de apresentação com três novas tarefas disponíveis por meio de Início Rápido (CTRL+Q) PresentOn – ativar o modo de apresentação PresentEdit – editar os tamanhos de fonte da apresentação no modo de apresentação.  "Fonte do Editor de texto" para o Editor de Consultas.  "Fonte de ambiente" para outros componentes.
RestoreDefaultFonts - Reverter para as configurações padrão.
*Observação: no momento, não há um comando PresentOff.  Use RestoreDefaultFonts para desativar o Modo de Apresentação*

### <a name="bug-fixes"></a>Correções de bugs

- Correção de um problema em que o SSMS falhava ao rolar o plano de execução pelo touchpad do Surface Book
- Correção de um problema em que o SSMS travava por um longo tempo ao obter as propriedades de um banco de dados que estava sendo restaurado ou offline 
- Correção de um problema em que não era possível abrir o “Visualizador da Ajuda” em builds RC
- Correção de um problema em que os itens da “Caixa de ferramentas das tarefas dos planos de manutenção” podiam estar ausentes no SSMS.
- Correção de um problemas no SSMS em que o usuário não podia reduzir um banco de dados quando o nome dele continha chaves. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Correção de um problema em que o SSMS estava tentando executar scripts à exclusão de um banco de dados do Azure e que, na verdade, causava a exclusão do próprio banco de dados. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- Correção de um problema em que os valores padrão não foram colocados em script para os tipos de tabela definidos pelo usuário. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- Outra rodada de melhorias de desempenho no menu de contexto em índices. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- Correção do problema que estava causando cintilação excessiva ao posicionar o mouse sobre um índice ausente no plano de execução. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- Correção de um problema no qual o SSMS estava colocando o banco de dados no modo offline ao executar o script [item do Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- Correções diversas na interface do usuário em versões localizadas (não inglês) do SSMS.
- Correção do problema no qual o nó "Chaves do Always Encrypted" estava ausente durante o direcionamento do SQL 2016 SP1 Standard Edition.
- Always Encrypted Menu "Always Encrypted" incorretamente habilitado ao direcionar o SQL 2016 RTM Standard Edition ou qualquer servidor do SQL 2014 (e abaixo) Correção de um problema em que o IntelliSense relata um erro quando a sintaxe CREATE ou ALTER é usada Correção de um o problema em que a criptografia falha caso CMK/CEK contenha caracteres que devem ser ignorados, ou seja, colocados entre colchetes Quando ocorre uma exceção de Memória Insuficiente no SSMS, o usuário recebe um erro que sugere o uso do PowerShell nativo (64 bits).
Correção do problema em que o assistente do AE falha caso o usuário esteja usando assinaturas do Gerenciador de Grupo de Recursos em vez de assinaturas do Azure clássico Correção do problema em que o assistente do AE mostra um erro incorreto quando usuário não tem permissão nas assinaturas ou não tem um Azure Key Vault em qualquer uma delas.
Problema corrigido no assistente do AE em que a página de entrada do Azure Key Vault não mostrava as assinaturas do Azure em caso de vários AAD Problema corrigido no assistente do AE em que a página de entrada do Azure Key Vault não mostrava as assinaturas do Azure para as quais o usuário tinha permissão de leitura
  - Correção de um problema em que os arquivos de recurso podiam não ser carregados corretamente, resultando em mensagens de erro incorretas
- Contraste aprimorado de hiperlinks na página de Configuração do SSMS
- Correção de um problema em que os nós PolyBase não eram exibidos quando conectado ao SQL Server Express (2016 SP1)
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
- Corrigido o problema em que o SQL PowerShell não era capaz de se conectar a instâncias do SQL herdadas (2014 e anteriores). [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- Corrigido um problema que estava causando pane do SSMS quando este falhava ao importar servidores registrados.
- Corrigido um problema que estava causando falha do SSMS se um usuário tinha determinadas permissões em um banco de dados. 
- SSMS – tabelas desaparecem da área de design ao visualizar novamente determinadas exibições. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- A barra de rolagem de tabela não permite que o usuário role o conteúdo da tabela, somente a seta para cima/para permite isso. O também é possível rolar o conteúdo da tabela depois de tentar rolar usando a barra de rolagem, o que é um bug. [Conectar Item](
https://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- Servidores registrados não exibindo ícones depois de atualizar o nó raiz.
- O botão de script para criar o banco de dados em servidores v12 do Azure executa o script e exibe a mensagem "Nenhuma ação para receber scripts".
- SSMS, a caixa de diálogo Conectar-se ao Servidor não limpa a guia "Propriedades Adicionais" para cada nova conexão.
- O script Gerar Tarefas não gera scripts de Criar Banco de Dados para um Banco de Dados SQL do Azure.
- A barra de rolagem no Designer de Exibição aparece desabilitada.
- Os caminhos de chave AVK Always Encrypted não incluem IDs de versão.
- Número reduzido de consultas do mecanismo de edição na janela de consulta. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3113387)
- Erros do Always Encrypted causados pela atualização de módulos após a criptografia são manipulados incorretamente.
- Alterado tempo limite de conexão padrão para OLTP e OLAP de 15 para 30 segundos para corrigir uma classe de falhas de conexão ignoradas. 
- Corrigida uma falha no SSMS quando o relatório personalizado era iniciado. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Corrigido um problema em que "Gerar Script..." falha para bancos de dados SQL do Azure.
- Corrigido "Escrever Script Como" e "Assistente de Gerar Script" para não adicionar novas linhas extras ao escrever script de objetos, por exemplo procedimentos armazenados. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3115850)
- O provedor SQLAS PowerShell: adicione a propriedade LastProcessed às pastas Dimension e MeasureGroup. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3111879)
- Estatísticas de consulta em tempo real: corrigido o problema em que apenas a primeira consulta em um lote era mostrada. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Plano de execução: na janela Propriedades, mostrar o máximo em vez da soma nos threads.
- Repositório de consultas: adicione novo relatório em consultas com alta variação de execução.
- Problemas de desempenho do Pesquisador de Objetos: [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3114074) O menu de contexto para tabelas trava momentaneamente O SSMS é lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota [Internet]). Evitar emitir consultas de tabela que são classificadas no servidor
- Removido o Assistente de Implantação do Azure (implantar banco de dados em VM do Azure) do SSMS
- Corrigido o problema em que os índices ausentes não eram mostrados nos planos de execução no SSMS [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3114194)
- Corrigido um problema comum de falha no desligamento no SSMS
- Correção de um problema no Pesquisador de Objetos em que ocorria um erro ao abrir o menu de contexto no PolyBase | Nós de grupo de expansão [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3115128)
- Corrigido um problema em que o SSMS poderia falhar ao tentar exibir as permissões em um banco de dados
- Repositório de consultas: aprimoramentos gerais em itens de menu de contexto para grades de resultados do relatório do repositório de consultas
- Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3103181)
- Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3109591)
- O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.
- Corrigido um problema de truncamento da interface do usuário na caixa de diálogo "Registro de Novo Servidor"
- Corrigida a interface do usuário da condição DMF, que atualizava incorretamente expressões que continham valores de constante de cadeia de caracteres com aspas
- Corrigido um problema que pode fazer com que o SSMS falhe ao executar relatórios personalizados
- Adicionar item de menu "Execução no Scale Out..." ao nó de pasta
- Correção de um problema com o recurso de endereço IP da lista de permissões do firewall do BD SQL do Azure
- Correção de um problema no SSMS que causava uma exceção de referência de objeto não definida ao editar a origem da partição multidimensional do AS
- Correção de um problema no SSMS que causava uma exceção de referência de objeto não definida ao excluir um assembly de cliente do servidor multidimensional do AS
- Correção de um problema que causava uma falha ao renomear um bd de tabela 1400 do AS
- Correção de um problema com o script de uma fonte de dados de tabela do AS com nível de compatibilidade 1400 da caixa de diálogo de propriedades de conexão
- Remoção da suposição de que as tabelas em um modelo no nível de compatibilidade 1400 do AS têm pelo menos uma partição
- CTRL-R agora alterna o painel de resultados no editor de consultas do SSMS DAX


## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![baixar](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
Disponibilidade geral | Número de build: 13.0.16106.4

[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

Os seguintes problemas foram corrigidos nesta versão:

* Corrigido um problema introduzido no SSMS 16.5.2 que estava causando a expansão do nó 'Table' quando a tabela tinha mais de uma coluna esparsa.

* Os usuários podem implantar pacotes do SSIS contendo o Gerenciador de Conexões do OData, que se conectam a um recurso do Microsoft Dynamics AX/CRM Online para o catálogo do SSIS. Para obter mais informações, consulte [Gerenciador de Conexões do OData](../integration-services/connection-manager/odata-connection-manager.md).

* Configurar Always Encrypted para uma tabela existente falha com erros em objetos não relacionados. [ID de Conexão 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* Configurar Always Encrypted para um banco de dados com vários esquemas não funciona. [ID de Conexão 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* O assistente de coluna Always Encrypted, Encrypted falha devido a banco de dados contendo exibições que referenciam exibições de sistema. [ID de Conexão 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Ao criptografar usando Always Encrypted, erros de atualização de módulos após a criptografia são manipulados incorretamente.

* O menu *Abrir recente* não mostra arquivos salvos recentemente. [ID de Conexão 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* O SSMS está lento ao clicar com o botão direito do mouse em um índice para uma tabela (mais de uma conexão remota (Internet)). [ID de Conexão 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Corrigido um problema com a barra de rolagem do Designer do SQL. [ID de Conexão 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* O menu de contexto para tabelas trava momentaneamente 
 
* Ocasionalmente, o SSMS lança exceções no Monitor de Atividade e falha. [ID de Conexão 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* O SSMS 2016 falha com o erro "O processo foi terminado devido a um erro interno no Tempo de Execução do .NET no IP 71AF8579 (71AE0000) com código de saída 80131506"


## <a name="uninstall-and-reinstall-ssms-17x"></a>Desinstalar e reinstalar o SSMS 17.x

Se a instalação do SSMS estiver tendo problemas e uma desinstalação e reinstalação padrão não os resolver, primeiro tente [reparar](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs) o IsoShell do Visual Studio 2015. Se reparar o IsoShell do Visual Studio 2015 não resolver o problema, as etapas a seguir poderão corrigir diversos problemas aleatórios:

1.  Desinstale o SSMS da mesma forma que desinstala qualquer aplicativo (usando *Aplicativos e recursos*, *Programas e recursos* etc. dependendo da versão do Windows).

2.  Desinstale o IsoShell do Visual Studio 2015 **de um prompt de comando com privilégios elevados**:
   
    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3.  Desinstale o Pacote Redistribuível do Microsoft Visual C++ 2015 da mesma maneira que desinstala qualquer aplicativo. Desinstale a versão x86 e a x64 se estiverem no computador.

4.  Reinstale o IsoShell do Visual Studio 2015 **de um prompt de comando com privilégios elevados**:  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  
 
    ```vs_isoshell.exe /PromptRestart```

5.  Reinstale o SSMS.

6.  Atualize para a [versão mais recente do Pacote Redistribuível do Visual C++ 2015](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) se você não estiver atualizado.


## <a name="additional-downloads"></a>Downloads adicionais  
Para obter uma lista de todos os downloads do SQL Server Management Studio, veja o [Centro de Download da Microsoft](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obter a versão mais recente do SQL Server Management Studio, veja [Baixar o SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
