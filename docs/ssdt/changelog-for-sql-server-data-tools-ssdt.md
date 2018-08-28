---
title: Log de mudanças para o SSDT (SQL Server Data Tools) | Microsoft Docs
ms.custom: ''
ms.date: 07/02/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssdt
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 9cf2952b907da3dc44046e57796de761e62336de
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43096115"
---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>Log de mudanças para o SSDT (SQL Server Data Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este log de alterações é para o [SSDT (SQL Server Data Tools)](download-sql-server-data-tools-ssdt.md).  
  
Para ver postagens detalhadas sobre as novidades e alterações, visite [o blog da Equipe do SSDT](https://blogs.msdn.microsoft.com/ssdt/)


## <a name="ssdt-for-visual-studio-2017-1571"></a>SSDT para Visual Studio 2017 (15.7.1)
Número de build: 14.0.16167.0  
Data do lançamento: 02 de junho de 2018  
  
### <a name="whats-new"></a>Novidades

**SSIS:**

- Adicione suporte para a nova autoridade do AAD Azure Governamental (login.microsoftonline.us) para uso com Tarefas AS.
- Foi corrigido um problema em a interface do usuário da tarefa de processamento de AS mostra "Método não encontrado" quando a versão do servidor de destino é o SQLServer2016.
- Foi corrigido um problema em que alguns componentes do pipeline não podem ser executados quando a versão do servidor de destino é o SQLServer2012.

**Instalador:**

- Filtre a lista de instâncias do VS para excluir as instâncias que não podem instalar o SSDT.

### <a name="known-issues"></a>Problemas conhecidos:

- A Tarefa Executar Pacote do SSIS não é compatível com a depuração quando ExecuteOutOfProcess está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.
- Ao instalar o SSDT no Windows 10 e escolher "Instalar novas Ferramentas de Dados do SQL Server para a instância do Visual Studio 2017", a instalação falhará em "Não há suporte para a operação de metarquivo solicitada". Reinicialize o computador e inicie o instalador novamente para continuar a instalação do SSDT.



## <a name="ssdt-for-visual-studio-2017-1570"></a>SSDT para Visual Studio 2017 (15.7.0)
Número de build: 14.0.16165.0  
Data do lançamento: 4 de junho de 2018  
  
### <a name="whats-new"></a>Novidades

**SSIS:**

- Corrigir um problema que a página *Designers do Integration Services* na caixa de diálogo Opções não pode ser exibida corretamente.  
- Corrigir um problema que a emissão da taxa de luminosidade do texto está sendo exibida no editor *Editor de transformação classificação*.  
- Corrigir um problema que a caixa de diálogo *Resolver referências* desaparece ao tentar editar um combobox.  
- Corrigir um problema que o link de ajuda F1 do *Gerenciador de conexões do Hadoop* não funciona.  
- Corrigir um problema que o código da tarefa de script será perdido se ele estiver em um contêiner durante o direcionamento do SQL Server 2016.  


**Instalador:**

- Corrigir um problema que o SSAS não pode ser instalado antes do SSRS e o SSIS é instalado no VS 15.7.2.

### <a name="known-issues"></a>Problemas conhecidos:

- A Tarefa Executar Pacote do SSIS não é compatível com a depuração quando *ExecuteOutOfProcess* está definido como *True*. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.


## <a name="ssdt-for-visual-studio-2017-1560"></a>SSDT para Visual Studio 2017 (15.6.0)
Número de build: 14.0.16162.0  
Data do lançamento: 10 de março de 2018
  
### <a name="whats-new"></a>Novidades

**SSIS:**

- Correção de um problema em que a tarefa de processamento AS não registra quaisquer etapas de processamento ao direcionar para o SQLServer2016 e SQLServer2017.
- Correção de um problema em que a violação de acesso acontecerá ao abrir o dtsx com nomes de tarefa muitos longos e que não estejam em inglês no SSDT.
- Correção de um problema em que, às vezes, uma lista variável de ScriptTask desaparecerá na interface do usuário da tarefa.
- Correção de um problema em que a adição de uma cópia de um pacote existente falhará quando o local do pacote for o SQL Server.
- Correção de um problema em que o foco fica paralisado ao acessar a caixa de combinação em uma caixa de diálogo do editor.
- Correção de um problema em que a tela de fundo não será alterada ao modificar o tema do VS.
- Correção de um problema em que os rótulos de anotação e carregamento ficam invisíveis no tema escuro.
- Correção de um problema em que a propriedade de estado não está definida corretamente para os itens desabilitados da caixa de ferramentas do SSIS.
- Correção de um problema em que sempre há falha ao executar WebServiceTask.
- Correção de um problema em que a implantação de pacote falhará se a cadeia de conexão estiver definida como variável com expressão dependente de parâmetros do projeto.

**Instalador:**

- Adicione o link do "Programa de Aperfeiçoamento da Experiência do Usuário para SQL Server Data Tools" ao aviso de isenção de responsabilidade de privacidade.
- Correção de um problema em que a janela de instalação do VS é exibida ao selecionar "Instale uma nova instância do SQL Server Data Tools para Visual Studio 2017".

### <a name="known-issues"></a>Problemas conhecidos:
- A Tarefa Executar Pacote do SSIS não é compatível com a depuração quando ExecuteOutOfProcess está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.



## <a name="ssdt-for-visual-studio-2017-1552"></a>SSDT para Visual Studio 2017 (15.5.2)
Número de build: 14.0.16156.0
  
### <a name="whats-new"></a>Novidades

**SSIS**
- Correção de um problema em que a migração de projetos do SSIS 2008 falha quando o SSAS e o SSIS são instalados na mesma instância do VS 2017.
- Correção de um problema em que projetos Rdlc não podem ser criados quando o designer de relatórios Rdlc e o SSIS são instalados na mesma instância do VS 2017.
- Correção de um problema em que não é possível atualizar a cor da anotação.
- Correção de um problema em que algumas cadeias de caracteres no Editor do Gerenciador de Conexões do Hadoop são truncadas em outros idiomas.
- Correção de um problema em que algumas cadeias de caracteres são truncadas no Editor do Gerenciador de Conexões do OData.
- Correção de um problema em que algumas cadeias de caracteres são truncadas na janela do Assistente de Importação de Projeto do Integration Services.
- Correção de um problema no título na janela de informações da caixa de ferramentas SSIS.
- Correção de um problema em que algumas cadeias de caracteres são truncadas na janela do Assistente de Implantação do Integration Services. 

**Instalador**
- Correção de um problema em que algumas vezes baixar o conteúdo falhará com o erro "O sistema não pode localizar o arquivo especificado (0x80070002)".  

### <a name="known-issues"></a>Problemas conhecidos
- A Tarefa Executar Pacote do SSIS não é compatível com a depuração quando *ExecuteOutOfProcess* está definido como *True*. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.




## <a name="ssdt-for-visual-studio-2017-1551"></a>SSDT para Visual Studio 2017 (15.5.1)
Número de build: 14.0.16148.0
  
### <a name="whats-new"></a>Novidades

O Visual Studio 2017 (15.5.1) é a mesma versão da versão 15.5.0, com exceção das seguintes correções de bug no instalador:

1.  Correção de um problema no qual o instalador trava na pós-instalação do SQL Server Integration Services.
2.  Correção de um problema no qual a instalação falha com a seguinte mensagem de erro: “Não há suporte para a operação de metarquivo solicitada (0x800707D3)”.

Além dessas duas correções de bug, os seguintes detalhes do 15.5.0 ainda se aplicam ao 15.5.1

## <a name="ssdt-for-visual-studio-2017-1550"></a>SSDT para Visual Studio 2017 (15.5.0)
Número de build: 14.0.16146.0
  
### <a name="whats-new"></a>Novidades

O SSDT para Visual Studio 2017 (15.5.0) passa da versão prévia para GA (disponibilidade geral).

**Instalador**
1. A interface do usuário da instalação está localizada.
1. Substitua o ícone por uma versão de qualidade superior.

**IS (Integration Services)**
1. Adição de uma etapa de validação de pacote no Assistente de Implantação ao implantar o Azure SSIS IR no ADF, que detecta problemas de compatibilidade potenciais em pacotes do SSIS a serem executados no Azure SSIS IR. Para obter mais informações, consulte [Validar pacotes do SSIS implantados no Azure](..\integration-services\lift-shift\ssis-azure-validate-packages.md).
1. A extensão do SSIS está localizada.

### <a name="bug-fixes"></a>Correções de bugs

**IS (Integration Services)**
1. Correção de um problema no qual o layout do gerenciador de conexões OLEDB e ADO.NET está corrompido.
2. Correção de um problema no qual um erro de assembly não encontrado é acionado durante a tentativa de editar uma Tarefa de Processamento de Dimensão.

### <a name="known-issues"></a>Problemas conhecidos

**IS (Integration Services)** A Tarefa Executar Pacote do SSIS não dá suporte à depuração quando ExecuteOutOfProcess está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.



## <a name="ssdt-174-for-visual-studio-2015"></a>SSDT 17.4 para Visual Studio 2015
Número de build: 14.0.61712.050

### <a name="whats-new"></a>Novidades

**Projetos do AS (Analysis Services)**
- Adição de três novas opções aos projetos de tabela (em Opções > Tabela do Analysis Services > Importação de Dados):
  - Habilitar fontes de dados herdadas – permite que o usuário crie fontes de dados mais antigas do “modo de compatibilidade 1200” nos modos de compatibilidade mais novos.
  - Detecção automática de tipo – quando essa opção estiver habilitada, o Editor de Consultas para fontes de dados modernas tentará detectar tipos de dados para consultas não estruturadas quando eles forem carregados. Se a detecção for bem-sucedida, uma nova etapa poderá ser adicionada à consulta.
  - Executar análise em segundo plano – quando essa opção estiver habilitada, o Editor de Consultas para fontes de dados modernas executará consultas na fonte de dados, conforme as consultas forem carregadas para analisar o esquema de saída da consulta.

**IS (Integration Services)**
- Adição de uma etapa de validação de pacote no Assistente de Implantação ao implantar o Azure SSIS IR no ADF, que detecta problemas de compatibilidade potenciais em pacotes do SSIS a serem executados no Azure SSIS IR. Para obter mais informações, consulte [Validar pacotes do SSIS implantados no Azure](..\integration-services\lift-shift\ssis-azure-validate-packages.md).


### <a name="bug-fixes"></a>Correções de bugs

**Projetos do AS (Analysis Services):**
- Correção de um problema que poderá causar uma exceção sem tratamento durante o check-in de alterações de modelo no TFS.
- Correção de um problema que poderá causar uma exceção ao adicionar uma tabela com uma expressão M complexa a um modelo 1400.
- Correção de um problema que poderá causar uma falha no Visual Studio durante a pesquisa de metadados na exibição de diagrama do modelo.
- Correção de um problema com modelos 1400 que poderá fazer com que as colunas calculadas sejam removidas da definição de tabela ao salvar alterações em consultas da partição M.
- Correção de um problema ao usar a opção Renomear Consulta em modelos 1400 na interface do usuário Obter Dados\Editor de Tabela que poderá congelar durante a validação de compatibilidade com o modelo de dados atual.
- Correção de um problema que fez com que uma referência de assembly Newtonsoft estivesse ausente ao implantar um modelo 1400 no Azure Analysis Services.
- Correção de um problema que causou um erro de importação de dados por meio de PQ em um modelo 1400 em alguns casos.
- Correção de um problema de dimensionamento nas caixas de diálogo da interface do usuário do PowerQuery que ocorre durante a definição do dimensionamento de Janelas.
- Correção de um problema com a renomeação de funções.
- Correção de problemas com as Configurações de Projeto que poderão ter causado alterações de não salvar\sincronizar corretamente em alguns casos.
- Correção de um problema no editor do PowerQuery que adicionava etapas “Alterar Tipo” automaticamente.
- Correção de um problema que causou um erro ao abrir o arquivo BIM depois de alternar entre o modo Espaço de Trabalho Integrado.
- A propriedade MaxConnections agora está visível para fontes de dados em modelos de tabela.
- Aumento do tamanho inicial da janela do editor do PowerQuery.
- Palavras-chave da Consulta M, como “Origem” no editor do PowerQuery, agora serão mostradas como localizadas.
- Credenciais de cache ao trabalhar com modelos 1400 e fontes de dados estruturadas para evitar a necessidade de inserir as mesmas credenciais para cada tabela editada.

**Projetos do RS:**
- Correção de um problema que impedia a implantação de um único relatório em um projeto de vários relatórios
- Correção de um problema com Fontes de Dados Compartilhadas que poderá ter causado um problema na implantação
- Correção de um problema que poderá falhar o Gerenciador de Desfazer ao alternar entre a exibição de código, o modo de exibição de Design e a janela do editor de consultas
- Correção de um problema que poderá ter feito com que o painel de parâmetros desaparecesse após um erro de tempo de execução
- Correção de um problema com os Projetos de Relatório que poderá ter causado a perda de mapeamentos do controle do código-fonte

**Integration Services:**
- Correção de um problema que poderá ter ocorrido ao alternar uma conexão em uma Tarefa de Processo do Analysis Services
- Correção de um problema no qual algumas tarefas/componentes não estão bem localizados.
- Correção de um problema no qual os componentes CDC são interrompidos após a aplicação de uma correção do SQL ao CDC que adiciona a coluna \__$command\_id.


## <a name="ssdt-for-visual-studio-2017-1540-preview"></a>SSDT para Visual Studio 2017 (versão prévia 15.4.0)
Número de build: 14.0.16134.0
  
### <a name="whats-new"></a>Novidades

Essa versão fornece um instalador da Web autônomo para projetos do Banco de Dados do SQL Server, Analysis Services, Reporting Services e Integration Services no Visual Studio 2017 15.4 ou posterior.

### <a name="installer"></a>Instalador

- Permita que o usuário defina seu apelido ao instalar um novo SSDT para a instância do VS2017.
- Oculte as caixas de seleção de recursos do instalador se nenhuma instância do VS estiver selecionada.
- Refine algumas mensagens do instalador com base nos comentários dos clientes.
- Corrija o problema que indica que o instalador não dá suporte à atualização.


### <a name="ssis"></a>SSIS

- Corrija o problema que indica que o Assistente para Importação/Exportação não pode listar a fonte de dados quando o feature pack do Azure é instalado.
- Corrija o problema que indica que a edição de uma Tarefa de Processo do Analysis Services do SSIS gera uma exceção ao alternar a conexão.
- Corrija o problema que indica quebras de componentes CDC após a aplicação da correção do SQL que adiciona a coluna __$command_id.
- Corrija o problema que indica que um pacote de terceiros não pode ser editado e executado ao direcionar o SQL Server antigo.
- Corrija o problema que indica que a caixa de diálogo Configurar Fonte de Arquivo Simples não é mostrada corretamente ao clicar duas vezes em DTSWizard.exe e selecionar Fonte de Arquivo Simples.
- Corrija o problema que indica que um pacote que contém o componente/tarefa do Feature Pack do Azure não pode ser executado ao direcionar o SQL Server 2017.


**Problemas conhecidos**

- O instalador não foi localizado.
- A Tarefa Executar Pacote do SSIS não dá suporte à depuração quando *ExecuteOutOfProcess* está definido como True. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.


## <a name="ssdt-173-for-visual-studio-2015"></a>SSDT 17.3 para Visual Studio 2015
Número de build: 14.0.61709.290

### <a name="whats-new"></a>Novidades

**AS (Analysis Services)**

- O Cosmos DB e o HDI Spark estão habilitados nos modelos 1400.
- Propriedades da fonte de dados de tabela.
- Agora a "Consulta em branco" é uma opção com suporte para a criação de uma nova consulta no Editor de consultas para modelos no nível de compatibilidade 1400.
- Agora o Editor de consultas para modelos de modo 1400 permite salvar consultas sem que novas tabelas sejam processadas automaticamente.

**RS (Reporting Services)**

- Agora, ao serem abertos, os projetos solicitam a atualização do formato para dar suporte ao uso do MSBuild para criar e implantar.

### <a name="known-issues"></a>Problemas conhecidos

**AS (Analysis Services)**

- Modelos de nível de compatibilidade 1400 no modo de Consulta direta que têm perspectivas falham ao consultar ou descobrir metadados.

**RS (Reporting Services)**

- O novo formato do Projeto de relatório não mantém a associação do controle do código-fonte e gera um erro semelhante à mensagem:

   *O arquivo de projeto C:\path não está associado ao controle do código-fonte, mas a solução contém informações de associação do controle do código-fonte nela.*
 
   Para contornar esse problema, clique em **Usar associação da solução** toda vez que a solução for aberta.

- Depois de atualizar seu projeto para o novo formato do MSBuild, pode haver falhar ao salvar com uma mensagem semelhante à seguinte:

   *"O Parâmetro "unevaluatedValue" não pode ser nulo."*

   Para contornar esse problema, atualize as *Configurações de projeto* e preencha a propriedade *Plataforma*.

### <a name="bug-fixes"></a>Correções de bugs

**AS (Analysis Services)**

- Grande melhoria no desempenho ao carregar o modo de exibição de diagrama de modelos tabulares.
- Inúmeros problemas corrigidos para melhorar a integração e a experiência com o PowerQuery nos modelos de nível de compatibilidade 1400.
   - Problema que impedia a edição de permissões para origens de arquivo corrigido.
   - Correção de um problema Não é possível alterar a origem de Origens de arquivo.
   - Correção de um problema Interface do usuário incorreta exibida para Origens de arquivo.
- Correção de um problema que fazia a propriedade "JoinOnDate" ser removida quando uma relação "Ingressar em data" se tornou inativa.
- Agora a nova opção de consulta no Construtor de Consultas permite a criação de uma nova consulta em branco.
- Correção de um problema que fazia as edições em uma consulta da fonte de dados existente não atualizarem a definição do modelo da tabela no nível de compatibilidade 1400.
- Correção de problemas com expressões de contexto personalizado que podem ter causado exceções.
- Ao importar a nova tabela com nome duplicado nos modelos tabulares do 1400, agora o usuário é notificado de que houve um conflito de nome e que o nome ajustado deve ser exclusivo.
- O modo de representação do usuário atual foi removido dos modelos no Modo de importação, porque ele não é um cenário compatível.
- Agora a integração com o PowerQuery é compatível com opções para fontes de dados adicionais (OData.Feed, Odbc.DataSource, Access.Database, SapBusinessWarehouse.Cubes).
- Agora as cadeias de caracteres de Opções do PowerQuery para fontes de dados mostrarão corretamente o texto localizado com base na localidade do cliente.
- Agora o modo de exibição de diagrama mostra colunas recém-criadas do Editor de consultas M nos modelos de nível de compatibilidade 1400.
- Agora o Editor do Power Query oferece a opção de não importar dados.
- Correção de um problema com a instalação de um cartucho de dados usado para importar tabelas do Oracle em modelos multidimensionais no VS2017.
- Correção de um problema que talvez tenha ocasionado uma falha quando o mouse cursor deixava a barra de fórmulas de tabela em casos raros.
- Correção de um problema na caixa de diálogo Editar propriedades da tabela, em que a alteração do nome da tabela alterava incorretamente o nome da tabela de origem, causando um erro inesperado.
- Correção de uma falha que poderia ocorrer no VS2017 ao tentar invocar Testar segurança do cubo no designer Funções e no designer de guia Dados da célula em projetos multidimensionais.
- SSDT: as propriedades não são editáveis para fontes de dados de tabela.
- Correção de um problema que pode ter feito os builds MSBuild e DevEnv não funcionarem corretamente em alguns casos com arquivos de solução.
- Grande melhoria no desempenho ao confirmar alterações de modelo (edições de DAX para medidas, colunas calculadas) quando um modelo tabular contém metadados maiores
- Correção de inúmeros problemas com a importação de dados usando o PowerQuery nos modelos de nível de compatibilidade 1400
   - A importação demora um pouco após clicar em Importar e a interface do usuário não mostra nenhum status
   - Grande lista de tabelas na Exibição de navegador ao tentar selecionar tabelas a serem importadas muito lentamente
   - Baixo desempenho do Editor de consultas que trabalham com uma lista de 35 consultas na exibição do Editor de consultas (problema na área de trabalho PBI também)
   - A importação de várias tabelas desabilitava a barra de ferramentas e nunca podia ser concluída em algumas situações 
   - O designer de modelo aparecia desabilitado e não mostrava nenhum dado após a importação de tabelas usando o PQ
   - Desmarcar "Criar nova tabela" na interface do usuário do PQ ainda resultava na criação de uma nova tabela
   - A fonte de dados da pasta não está solicitando credenciais 
   - A referência de objeto não definia uma exceção que podia ocorrer ao tentar obter credenciais atualizadas na fonte de dados estruturada
   - A abertura do gerenciador de partições com a expressão M era muito lenta
   - Selecionar Propriedades na tabela no editor do PQ não mostrava as propriedades
- Melhoria da robustez na integração da interface do usuário do Power Query para capturar exceções de nível superior ser mostrada na Janela de Saída
- Correção de um problema com ChangeSource na fonte de dados de estrutura que não mantinha alterações na expressão de contexto
- Correção de um problema no qual os erros de expressão M podiam causar falhas na atualização do modelo sem a exibição de uma mensagem de erro
- Correção de um problema que fechava o SSDT com o erro "O build precisa ser interrompido antes que a solução possa ser fechada"
- Correção de um problema no qual o VS talvez pareça ter parado de responder ao definir o modo de representação incorreto no modelo de nível de compatibilidade 1400 
- Agora a propriedade das linhas de detalhes apenas serão serializadas no JSON quando ele não estiver vazio (alterado de padrão)
- Agora o driver Oracle OLEDB está disponível na lista do modo de Consulta direta de tabela
- Agora adicionar expressões M nos modelos tabulares de compatibilidade 1400 agora é exibido/atualizado no TME (Gerenciador de Modelos Tabular)
- Correção de um problema que fazia o provedor MSOLAP não ser exibido no VS2017 ao tentar importar usando a fonte de dados “Outro” nos modelos de nível de compatibilidade pré-1400
- Correção de um problema no qual a adição de uma translação por meio do TME pode causar problemas 
- Correção de um problema na interface da Segurança em nível de objeto que fazia a guia ser exibida/oculta incorretamente em alguns casos
- Correção de um problema em que a falha poderia ocorrer ao tentar abrir um modelo multidimensional carregado previamente usando a caixa de diálogo Conectar ao banco de dados
- Correção de um problema que causava um erro ao adicionar assemblies personalizados a um modelo multidimensional

**RS (Reporting Services)**

- Correção de um problema com a compilação e o build do RDLC no VS 2017

## <a name="ssdt-for-visual-studio-2017-1530-preview"></a>SSDT para Visual Studio 2017 (versão prévia 15.3.0)
Número de build: 14.0.16121.0
  
### <a name="whats-new"></a>Novidades

Esta versão prévia é a primeira versão do SSDT para Visual Studio 2017. Essa versão apresenta uma experiência de instalação Web autônoma para projetos do Banco de Dados do SQL Server, do Analysis Services, do Reporting Services e do Integration Services no Visual Studio 2017 15.3 ou posterior.


**Problemas conhecidos**

- O instalador não foi localizado.
- O SSIS não foi localizado.
- A tarefa Executar Pacote do SSIS não dá suporte à depuração quando *ExecuteOutofProcess* está definido como *True*. Esse problema aplica-se somente à depuração. O salvamento, a implantação e a execução por meio do DTExec.exe ou do catálogo do SSIS não são afetados.
- Para obter uma lista completa das alterações, consulte o [log de mudanças](changelog-for-sql-server-data-tools-ssdt.md).
- Os pacotes do SSIS que contêm extensões de terceiros não poderão ser mudados para serem direcionados a outras versões do servidor.


## <a name="ssdt-172-for-visual-studio-2015"></a>SSDT 17.2 para Visual Studio 2015
Número de build: 14.0.61707.300

### <a name="whats-new"></a>Novidades


**Projetos do AS:**
- Agora a Segurança em nível de objeto pode ser configurada na caixa de diálogo *Funções* para segurança avançada em modelos tabulares de nível de compatibilidade 1400.
- Nova seleção de membro de função AAD para usuários sem endereços de email em modelos do AS Azure em projetos SSDT AS para VS2017.
- Nova propriedade de projeto "Sempre solicitar" do AS Azure em projetos de tabela do SSDT AS para personalizar o comportamento de armazenamento em cache de credenciais ADAL.


### <a name="bug-fixes"></a>Correções de bugs

**Geral**
- Referências de identidade visual atualizada para SQL Server 2017.

**Projetos do AS**
- Correções de desempenho significativas feitas para melhorar a experiência ao confirmar as alterações de medida DAX e outras edições no modelo.
- Correção de diversos problemas com a integração do Power Query em projetos do Analysis Services usando modelos de tabela de nível de compatibilidade 1400.
- Correção de um problema em projetos multidimensionais no VS2017 somente quando o designer do Design Aggregation não conseguir carregar.
- Correção de um problema ao arrastar um item no diagrama DSV multidimensional do Analysis Services que poderia causar falha no 2017 VS.
- Correção de um problema em projetos AS em que a caixa de diálogo Implantar nem sempre estava em primeiro plano na parte superior do Visual Studio.
- Remoção da importação do Analysis Services do Data Marketplace como fonte de dados, pois o serviço foi encerrado.
- Correção de um problema que deixava o designer de tabela desabilitado após Importar nova tabela da fonte de dados existente por meio do Gerenciador de modelos de tabela.
- Correção de um problema que pode fazer com que os itens do menu Modelo Importar da fonte de dados/Adicionar fonte de dados permaneçam ocultos no contexto errado.
- Melhoria da experiência ao criar uma medida do Gerenciador de modelos de tabela para evitar alternar o foco de volta para a coluna usada para criar uma medida.
- Ao mudar do espaço de trabalho integrado em projetor de tabela AS para o servidor explícito do espaço de trabalho, os arquivos de banco de dados antigos serão limpos.
- Correção de um problema em projetos de modelos de tabela 1400 do AS em que o estado da interface do usuário da caixa de seleção da Segurança em Nível de Linha inicialmente era exibido como desmarcado independentemente do estado real do objeto em questão.
- Correção de uma falha que poderia ocorrer ao importar o arquivo de texto ou o arquivo do Excel para o modelo de tabela de modo de compatibilidade com 1400 usando o Power Query e a exceção sem tratamento gerada.
- Correção de um problema que poderia ocorrer com a posição da barra de rolagem no controle de edição de fórmula do DAX no designer de modelo de tabela do AS.
- Correção de um problema que impedia a modificação de uma fonte de dados de mashup do PowerQuery quando ela continha uma autenticação de nome de usuário e senha.
- Correção de um problema que poderia impedir que uma fonte de dados se conectasse com propriedades adicionais definidas na cadeia de conexão.
- Correção de um problema que poderia causar a falha do VS com vários projetos de modelo de tabela do AS carregados e fechar o segundo designer de modelo sem interagir com nada no designer primeiro.
- Correção de um problema em que as edições feitas na formatação de KPI não persistiam em alguns casos.
- Correção de um problema com a Interface do usuário do PowerQuery que exibia o estado marcado do menu errado se a barra de fórmulas era exibida.
- Correção de um problema em projetos de nível de compatibilidade do AS Tabular 1400 com fontes de dados do PowerQuery que podem causar falha no VS ao selecionar o menu Alterar a fonte de dados do Gerenciador de modelos de tabela.
- Correção de um problema intermitente em que carregar um modelo de tabela do 1400 pode exibir o erro *'Não foi possível carregar arquivo ou assembly 'Microsoft.ProBI.MashupLibrary'*.

**Projetos do RS**
- As preferências do usuário para o estado de seleção das configurações da caixa Parâmetro e Régua de RS são lembradas corretamente entre as sessões.

**Projetos do IS**
- Correção de um problema em que o contêiner ForEachLoop do ADO/ADO.NET não era exibido corretamente
- Correção de um problema em que algumas tarefas, componentes e assistentes não são localizados
- Alteração do *TargetServerVersion* mais recente do "SQL Server vNext" para "SQL Server 2017"


## <a name="ssdt-171-for-visual-studio-2015"></a>SSDT 17.1 para Visual Studio 2015
Número de build: 14.0.61705.170

### <a name="whats-new"></a>Novidades
**Projetos do AS:**
- Os usuários podem definir dicas de codificação em colunas na interface do usuário em modelos 1400
- O IntelliSense não relacionados a modelos agora está disponível no modo offline
- O Gerenciador de Modelos de Tabela agora contém um nó para representar expressões M nomeadas disponíveis no modelo (modelos de tabela com nível de compatibilidade 1400)
- O Seletor de Pessoas do Azure Active Directory, semelhante ao IAM do Portal do Microsoft Azure, agora está disponível ao configurar os Membros de Função em Modelos de Tabela

**Projetos de bancos de dados:**
- Atualizado para DacFx 17.1

### <a name="bug-fixes"></a>Correções de bugs
- Correção de um problema em que o nome do grupo de Designers do Business Intelligence era exibido incorretamente nas Opções do Visual Studio no VS2017
- Correção de um problema em que uma falha poderia ocorrer ao gerar um mapa de códigos para uma solução com um projeto de relatório ou projeto do AS
- Correção de diversos problemas com a integração do PowerQuery para modelos de tabela de nível de compatibilidade 1400 do Analysis Services
- Correção de um problema na nova janela de ferramentas do editor DAX em que o operador de atribuição não podia ficar em uma linha separada ao definir uma medida
- Correção de um problema que impedia a atualização da exibição da medida de tabela ao renomear as medidas na perspectiva
- Atualização do mecanismo de espaço de trabalho integrado do Analysis Services e do Modelo de Objeto de Tabela que corrige uma regressão que causava uma falha em projetos de tabela 1200 que continham translações ao serem implantados para o servidor do SQL Server 2016 Analysis Services
- Correção de um problema de desempenho que causava lentidão na criação\exclusão de novas fontes de dados de tabelas 1400
- Correção de um problema em que a renderização do diagrama DSV em modelos multidimensionais poderia ser interrompida se a exibição fosse alterada rapidamente entre diferentes DSVs

## <a name="dacfx-171"></a>DacFx 17.1
- Correção de um problema ao criptografar uma coluna com tabelas com otimização de memória com outras colunas de identidade
- Suporte de SQLDOM para a opção CATALOG_COLLATION para CREATE DATABASE

## <a name="dacfx-1701"></a>DacFx 17.0.1 
- Correção para o problema com bancos de dados com uma chave assimétrica em um HSM com um provedor de EKM [Connect Item](https://connect.microsoft.com/SQLServer/feedback/details/3132749/sqlpackage-exe-fails-when-extracting-a-database-which-contains-an-asymmetric-key-using-an-ekm-provider)

## <a name="ssdt-170-for-visual-studio-2015-supports-up-to-sql-server-2017"></a>SSDT 17.0 para Visual Studio 2015 (dá suporte até ao SQL Server 2017)
Número de build: 14.0.61704.140

### <a name="whats-new"></a>Novidades
**Projetos de bancos de dados:**
- Corrigir um índice clusterizado em uma exibição não bloqueará mais a implantação
- As cadeias de caracteres de comparação de esquema relacionadas à criptografia de coluna usam o nome adequado em vez do nome da instância.   
- Adição de uma nova opção de linha de comando para SqlPackage: ModelFilePath.  Isso oferece uma opção para que os usuários avançados especifiquem um arquivo model.xml externo para importação, publicação e operações de script   
- A API do DacFx foi estendida para compatibilidade com a Autenticação Universal do Azure AD e MFA (Autenticação Multifator)

**Projetos do IS:**
- O Gerenciador de Fontes OData do SSIS e o Gerenciador de Conexões OData agora têm suporte para conexão aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online.
- O projeto SSIS agora é compatível com a versão do servidor de destino do “SQL Server 2017” 
- Compatibilidade com CDC Control Task, CDC Splitter e CDC Source quando direcionado para SQL Server 2017. 

**Projetos do AS:**
- Integração do Analysis Services PowerQuery (modelos de tabela do nível de compatibilidade 1400):
    - O DirectQuery está disponível para SQL Oracle e Teradata e se o usuário já tiver instalado drivers de terceiros
    - Adicionar colunas por exemplo no PowerQuery
    - Opções de acesso a dados em modelos 1400 (propriedades do nível de modelo usadas pelo mecanismo M)
        - Habilitar combinação rápida (o padrão é false; quando definido como true, o mecanismo de mashup ignora os níveis de privacidade de fonte de dados ao combinar dados)
        - Habilitar redirecionamentos herdados (o padrão é false; quando definido como true, o mecanismo de mashup segue redirecionamentos HTTP potencialmente não seguros.  Por exemplo, um redirecionamento de um HTTPS para um URI de HTTP)  
        - Retornar valores de erro como Null (o padrão é false; quando definido como true, os erros no nível da célula são retornados como null. Quando definido como false, uma exceção será gerada se a célula contiver um erro)  
    - Fontes de dados adicionais (fontes de dados de arquivo) usando o PowerQuery
        - Excel 
        - Texto/CSV 
        - Xml 
        - Json 
        - Pasta 
        - Banco de dados do Access 
        - Armazenamento de blobs do Azure 
    - Interface do usuário do PowerQuery localizada
- Janela de Ferramentas do Editor DAX
    - Experiência de edição aprimorada no DAX para medições, colunas calculadas e expressões de linhas de detalhes, disponíveis por meio dos menus Exibir e Outras Janelas no SSDT
    - Aprimoramentos para parser\IntelliSense do DAX


**Projetos do RS:**
- O controle de RVC incorporável agora está disponível com suporte ao SSRS 2016

### <a name="bug-fixes"></a>Correções de bugs
**Projetos do AS:**
- Correção da prioridade de modelo para projetos de BI, para que não aparecem na parte superior das categorias de Novos Projetos no VS
- Correção de um travamento do VS que pode ocorrer em circunstâncias raras durante a abertura de solução SSIS, SSAS ou SSRS
- Tabular: uma variedade de aprimoramentos e correções de desempenho para análise de DAX e barra de fórmulas.
- Tabular: o Gerenciador de Modelos de Tabela não estará visível se nenhum projeto Tabular do SSAS estiver aberto.
- Multidimensionais: corrigido um problema em que a caixa de diálogo de processamento não era utilizável em computadores com alto DPI.
- Tabular: correção de um problema em que o SSDT falha ao abrir qualquer projeto do BI quando o SSMS já está aberto. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3100900/ssdt-faults-when-opening-any-bi-project-when-ssms-is-already-open)
- Tabular: corrigido um problema em que hierarquias não estavam sendo corretamente salvas no arquivo bim em um modelo 1103.[Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3105222/vs-2015-ssdt)
- Tabular: corrigido um problema em que modo de espaço de trabalho integrado era permitido em computadores de 32 bits mesmo quando não havia suporte.
- Tabular: corrigido um problema em que clicar em qualquer coisa no modo de semisseleção (digitando uma expressão DAX mas clicando em uma medida, por exemplo) poderia causar falhas.
- Tabela: Corrigido um problema em que o Assistente de implantação redefiniria a propriedade .Name de volta para "Model". [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3107018/ssas-deployment-wizard-resets-modelname-to-model)
- Tabular: correção de um problema em que selecionar uma hierarquia em TME deveria exibir propriedades mesmo se a exibição de diagrama não estivesse selecionada.
- Tabular: corrigido um problema em que colar na barra de fórmula DAX colaria imagens ou outros tipos de conteúdo em vez de texto ao colar de determinados aplicativos.
- Tabular: corrigido um problema em que alguns modelos antigos no 1103 não podiam ser abertos devido à presença de medidas com uma definição específica.
- Tabular: corrigido um problema em que as sessões do XEvent não puderam ser excluídas.
- Correção de um problema que causa falha ao tentar compilar arquivos "smproj" do AS com devenv.com
- Correção de um problema que estava finalizando as alterações de texto com muita frequência ao usar o IME em coreano em títulos de guia de planilha de modelo de tabela do AS
- Correção de um problema no qual o intellisense para a função DAX Related() não estava funcionando corretamente para mostrar colunas de outras tabelas
- Aprimoramento da importação de projeto de tabela do AS da caixa de diálogo de banco de dados por meio da classificação da lista de bancos de dados do AS
- Correção de um problema ao criar tabelas calculadas no modelo de tabela do AS em que as Tabelas não eram listadas como os objetos sugeridos na expressão
- Correção de um problema de visualização de modelos do AS 1400 tentando abrir usando o servidor de Espaço de Trabalho Integrado após a visualização do código
- Correção de um problema que impedia algumas fontes de dados (sem suporte para o catálogo inicial) de funcionar corretamente em determinadas circunstâncias 
- O Assistente de Implantação deve aplicar as alterações em partições de tabela calculadas, mesmo quando a opção de manter as partições estiver habilitada
- Correção de um problema no qual a caixa de diálogo Propriedades Avançadas da Conexão do AS existente não mostrava a lista completa até a nova seleção
- Correção de alguns problemas com cadeias de caracteres de interface do usuário recortadas em alguns builds localizados
- Correção de diversos problemas com a integração do PowerQuery para modelos de tabela do AS com nível de compatibilidade 1400
- Correção de um problema com modelos de estilo do Assistente de Relatório que não apareciam corretamente
- Correção de um problema com o Assistente de Relatório que podia levar a configurações de fonte de dados incorretas durante a alteração do SQL para o AS
- Correção de um problema que causava falha de compilação de projeto (Tabela) do Analysis Services da linha de comando (devenv.com\exe)
- Correção de um problema com o analisador de medidas do DAX para mostrar a cor e realce corretos do texto ao iniciar com letras antes de :=
- Correção de um problema ao disparar um ObjectRefException se os caminhos fossem longos demais ao tentar Mostrar Todos os Arquivos em projetos de Tabela em um modo de espaço de trabalho integrado
- Correção de um problema com o Designer de Fonte de Dados para Compact 4.0 Client Data Provider em que ele parecia estar indisponível
- Correção de um problema que causava um erro ao tentar navegar pelo modelo de mineração do AS no VS2017
- Correção de um problema no modelo multidimensional do AS no VS2017 em que o diagrama DSV parava a renderização depois de alterar as exibições e atingir uma exceção
- Correção de um problema para visualizar relatórios com uma falha na conexão do AS no VS2017
 

**Projetos do RS:**
- Correção de um problema durante a criação de relatórios no SSDT em que o modo de exibição de árvore dos parâmetros, fontes de dados e conjuntos de dados eram recolhidos quando a maioria das alterações era feita 
- Corrigido um problema em que Salvar deveria salvar a versão do RDL e não a versão mais recente.
- Corrigido um problema em que o SSDT RS está fazendo backup de arquivos quando o backup é desativado, entre vários outros problemas.
- Corrigido um problema no construtor de relatórios em que um erro seria exibido quando você clicasse em "Dividir Células". [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3101818/ssdt-2015-ssrs-designer-error-by-matrix-cell-split)
- Corrigido um problema em que o cache pode gerar dados incorretos em um relatório. [Conectar Item](http://connect.microsoft.com/SQLServer/feedback/details/3102158/ssdtbi-14-0-60812-report-preview-data-is-frequently-wrong-due-to-bad-caching)

**Projetos do IS:**
- Corrigido um problema em que a configuração run64bitruntime não permanecia.
- Corrigido um problema em que DataViewer não salvava colunas exibidas.
- Corrigido um problema que Partes do Pacote oculta anotações. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3106624/package-parts-hide-annotations)
- Corrigido um problema que partes do pacote descarta as anotações e layouts de fluxo de dados. [Conectar Item](https://connect.microsoft.com/SQLServer/feedback/details/3109241/package-parts-discard-data-flow-layouts-and-annotations)
- Corrigido um problema em que o SSDT falha ao importar o projeto do SQL Server.
- Correção de um problema com a Tarefa do Sistema de Arquivos Hadoop TimeoutInMinutes padrão para 10 após abrir um pacote SSIS salvo e no tempo de execução.

**Projetos de bancos de dados:**
- Implantação do DACPAC SSDT adiciona configuração novamente para IgnoreColumnOrder [item do Connect](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)
- SSDT falha ao compilar se STRING_SPLIT for usado [item do Connect](http://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)
- Correção de problema em que DeploymentContributors tem acesso ao modelo público, mas o esquema de backup não foi inicializado [problema do Github](https://github.com/Microsoft/DACExtensions/issues/8)
- Correção temporária de DacFx para o posicionamento de FILEGROUP
- Correção do erro de "Referência não resolvida" para sinônimos externos. 
- Always Encrypted: a criptografia online não desabilita o controle de alterações em cancelamento e não funciona corretamente se o controle de alterações não tiver sido limpo antes de iniciar a criptografia


## <a name="ssdt-165-for-visual-studio-2015-supports-up-to-sql-server-2016"></a>SSDT 16.5 para Visual Studio 2015 (dá suporte até ao SQL Server 2016)
Lançamento: 20 de outubro de 2016

Número de build: 14.0.61021.0

**Novidades**


### <a name="connection-improvements"></a>Aprimoramentos de conexão

* A nova caixa de pesquisa na guia **Procurar** ajuda a filtrar seus servidores locais, servidores de rede e bancos de dados do SQL do Azure. Isso é útil se você tem um grande número de servidores ou bancos de dados que aparecem nessas listas.
* A guia **Histórico** tem opções de menu de clique com o botão direito do mouse para fixar/desafixar favoritos e uma nova opção para remover conexões do histórico.

### <a name="sqlpackage-and-dacfx-api-improvements"></a>Aprimoramentos da API SqlPackage e DacFx

Agora, ao usar as APIs SqlPackage.exe e DacFx, você pode gerar um relatório de implantação, um script de implantação e publicar em um banco de dados, tudo de uma só vez. Isso economiza tempo para qualquer pessoa que gosta de guardar um relatório do que foi publicado durante a implantação. Outra vantagem é que, para cenários do Azure, são criados scripts separados para o banco de dados mestre e para o banco de dados de destino de implantação. Até agora era criado um único script que não era útil para implantações repetidas.

Para ações de Publicação e de Script do SqlPackage, foram adicionados dois novos argumentos.

* DeployScriptPath (nome curto: dsp). Esse é um caminho opcional no qual gravar o script de implantação. Para implantação do Azure, se houvesse comandos de TSQL para criar ou modificar o banco de dados, um script mestre seria gravado no mesmo caminho, mas com "Filename_Master.sql" como o nome de arquivo de saída.
* DeployReportPath (nome curto: drp). Esse é um caminho opcional no qual gravar o relatório de implantação.

Observe que para a ação de Script, os argumentos de caminho de saída existentes ou os novos argumentos específicos de script/relatório devem ser usados, mas não ambos.

Exemplo de uso:

**Ação de publicação**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**Ação de script**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

No DacFx, foram adicionadas duas novas APIs: DacServices.Publish() and DacServices.Script(). Elas também dão suporte à realização de ações de publicação + script + relatório em uma única operação. Exemplo de uso:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services e Reporting Services**

O analisador DAX de designer tabular do SSAS teve o desempenho aprimorado ao trabalhar com grandes expressões DAX.
Para obter mais informações, leia a [Postagem de blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

### <a name="fixed--improved-this-month"></a>Corrigido/aprimorado neste mês

**Ferramentas de banco de dados**

* [Bug de conexão 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema) – colunas não podem ser selecionadas de CROSS APPLY OPENJSON com esquema explícito
* Corrigido – problema com índices de tabela de histórico gerados automaticamente, em que o DacFx soltava índices na reimplantação
* Corrigido – problema com o analisador de lote DacFx que não analisava caracteres colchete ']' de escape, o que fazia com que a publicação falhasse
* Aprimorado – agora o SqlPackage inclui descrições para cada ação na saída da ajuda
* Corrigido – a opção "Lembrar senha", na caixa de diálogo de conexão, não era preservada ao editar opções avançadas e ao editar uma cadeia de conexão salva em Publicar, Comparação de Esquemas e outros arquivos
* Corrigido – para mostrar conexões na guia Histórico com IntegratedAuthentication = true, o campo de Autenticação, nas propriedades de conexão, foi deixado em branco. Agora é mostrado "Autenticação do Windows" conforme o esperado
* Corrigido – as alterações nas configurações do IntelliSense das Ferramentas do SQL Server em Ferramentas -> Opções -> Editor de Texto não eram preservadas
* Aprimorado – o botão Fixar/Desafixar na guia Histórico da caixa de diálogo de conexão, agora é mais compacto, reduzindo a probabilidade de aparecimento de uma barra de rolagem
* Corrigido – vários problemas de acessibilidade na caixa de diálogo conexão foram corrigidos.

**Analysis Services e Reporting Services**

* Foi corrigido um problema no designer de tabela SSDT AS em que, ao clicar na miniatura de barra de rolagem da grade de dados, gerava falha em determinadas situações
* Foi corrigido um problema em que a opção para representar a conexão como o usuário atual no designer de tabela SSDT AS não estava disponível
* Foi corrigido um problema no designer de tabela SSDT AS em que ao expandir a barra de fórmulas para muito longe poderia fazer com que o projeto se tornasse impossível de reabrir
* Foi corrigido uma falha no designer de tabela SSDT AS que ocorreria ao pressionar uma tecla, se a guia Tabela estivesse selecionada
* Foi corrigido um problema em projetos SSDT AS em que Analisar no Excel não se conectaria a versões de servidor AS de nível inferior

**Serviço de integração**

* Bug de conexão [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks) corrigido: mover vários pacotes de tarefas do serviço de integração





## <a name="ssdt-164-for-visual-studio-2015-for-sql-server-2016"></a>SSDT 16.4 para Visual Studio 2015 (para SQL Server 2016)
Lançamento: 20 de setembro de 2016

Número de build: 14.0.60918

**Novidades**

Agora há suporte para a Comparação de Esquemas nas APIs SqlPackage.exe e DacFx (Data-Tier Application Framework). Para obter detalhes, consulte [Comparação de Esquemas na SqlPackage e na Data-Tier Application Framework](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/).

**Analysis Services – modo integrado de espaço de trabalho para SSDT Tabular (SSAS)**

O SSDT Tabular agora inclui uma instância do SSAS interna, que o SSDT Tabular inicia automaticamente em segundo plano se o modo de espaço de trabalho integrado estiver habilitado, para que você possa adicionar e exibir dados, tabelas e colunas no designer de modelo sem ter que fornecer uma instância de servidor de espaço de trabalho externo. Modo de espaço de trabalho integrado não será alterado quando SSDT Tabular trabalhar com um servidor de espaço de trabalho e o banco de dados. O que muda é onde o SSDT Tabular hospeda o banco de dados do espaço de trabalho. Para habilitar o modo de espaço de trabalho integrado, selecione a opção Espaço de Trabalho Integrado na caixa de diálogo Designer de Modelos de Tabela, exibida ao criar um novo projeto tabular. Para projetos tabulares existentes, que atualmente usam um servidor de espaço de trabalho explícito, você pode mudar para o modo de espaço de trabalho integrado, definindo o parâmetro Modo de Espaço de Trabalho Integrado como True na janela Propriedades, que é exibida quando você seleciona o arquivo Model.bim no Gerenciador de Soluções. Para obter detalhes, consulte a [Postagem de blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

**Atualizações e correções**
**Ferramentas de banco de dados:**

- [Problema de conexão 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775): tabelas temporais desfeitas em Ferramentas de Dados do VS, atualização 14.0.60629.0 de julho, "O valor não pode ser nulo. Nome do parâmetro: reportedElement "
- [Problema de conexão 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648): IsPersistedNullable mostrado como diferente na comparação do SSDT
- [Problema de conexão 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735): identidade é redefinida ao importar um BACPAC
- [Problema de conexão 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167): a execução de testes de unidade do SSDT deixa arquivos temporários para trás
- [Problema de conexão 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712): quebra de compatibilidade com versões anteriores – AppLocal e Nugetization

**Analysis Services e Reporting Services**

* Foi corrigido um problema no SSDT em que pop-ups de dicas de erros ficavam no meio do caminho ao editar colunas calculadas de DAX para DirectQuery.
* Foi corrigido um problema na grade tabular do SSDT AS em que o ícone do KPI não estava aparecendo na grade de medida quando o fator de dimensionamento do Windows era definido com alto DPI, acima de 200%.
* Foi corrigido um problema no SSDT AS em que colar dados de uma tabela grande poderia fazer com que o projeto tabular se tornasse sem resposta.
* Foi corrigido um problema no editor de modelo tabular do SSDT AS para marcar o modelo como necessário salvar as alterações, ao renomear o nome amigável da conexão.
* Foi corrigido um problema em projetos tabulares do SSDT AS em que a largura das colunas na caixa de diálogo Gerenciar Relações não podia ser redimensionada.
* Foi corrigido um problema nos modelos tabulares de nível de 1200 do SSDT AS em que colar dados do Excel com configurações de localidade, como alemão, não tratava corretamente a vírgula como um separador decimal.
* Foi corrigido um problema em projetos do SSDT AS com alguns conjuntos de ícones de KPI que poderiam produzir um erro "Não foi possível recuperar os dados para este visual".
* Foi corrigido um problema na caixa de diálogo de Propriedades do Projeto do SSDT AS para que seja corretamente ancorada ao ser redimensionada com o dimensionamento com alto DPI.
* Foi corrigido um problema em projetos do SSDT AS que pode ter causado um erro ao atualizar determinados modelos com tabelas coladas.
* Foi corrigido um problema no SSDT AS em que colar linhas de folha inteira do Excel era muito lento e criava muitas colunas indesejadas.
* Foi corrigido um problema no SSDT AS em que a análise e o realce de grandes expressões DataTable estáticas eram muito lentos ou parecia travar.
* Foi corrigido um problema no SSDT AS para adicionar medidas e valores de KPI à perspectiva atual selecionada no editor.
* Foi corrigido um problema no SSDT em que importar dados do SQL Azure para o projeto AS não dava suporte a tipos de esquema que não eram "dbo".



## <a name="ssdt-163-for-visual-studio-2015-for-sql-server-2016"></a>SSDT 16.3 para Visual Studio 2015 (para SQL Server 2016)
Lançamento: 15 de agosto de 2016

Número de build: 14.0.60812.0  

**Novidades**

- **Controle e numeração de versão:** as versões agora são rotuladas numericamente, em vez de por mês. Isso se alinha com a nova política do SSMS e simplifica os casos em que há várias versões ou hotfixes em um mês. Esta versão é a 16.3, que significa que é a terceira atualização após a versão RTM. Qualquer hotfix será 16.3.1 e assim por diante, com a nossa próxima atualização (planejada para o próximo mês) sendo a 16.4.
- **Analysis Services – Gerenciador de Modelos Tabular:** o Gerenciador de Modelos Tabular permite que você percorra convenientemente pelos diversos objetos de metadados em um modelo, como fontes de dados, tabelas, medidas e relações. Ele é implementado como uma janela de ferramentas separada que você pode exibir ao abrir o menu Exibir no Visual Studio, apontando para Outras Janelas e clicando em Gerenciador de Modelos Tabular. O Gerenciador de Modelos Tabular é exibido por padrão na área de Gerenciador de Soluções, em uma guia separada. O Gerenciador de Modelos Tabular organiza objetos de metadados em uma estrutura de árvore que se assemelha ao esquema de um modelo tabular de 1200 e tem muitos recursos novos.
- **Ferramentas de Banco de Dados – Always Encrypted**: esta versão oferece novas caixas de diálogo [Gerenciamento de Chaves Always Encrypted](../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) para adicionar facilmente Chaves Mestras da Coluna ou Chaves de Criptografia da Coluna ao seu projeto de banco de dados ou a um banco de dados ao vivo no Pesquisador de Objetos do SQL Server. Esta versão dá suporte a certificados no Repositório de Certificados do Windows. Em versões futuras, o Azure Key Vault e os provedores CNG terão suporte.
    - Ao criar a Chave Mestra da Coluna ou a Chave de Criptografia da Coluna, você poderá notar que as alterações não estão refletidas no Pesquisador de Objetos do SQL Server, logo depois de clicar em Atualizar Banco de Dados. Para solucionar esse problema, atualize o nó do banco de dados no Pesquisador de Objetos do SQL Server.
    - Se você tentar criptografar uma coluna em uma tabela com os dados do Pesquisador de Objetos do SQL Server, poderá enfrentar uma falha. Este recurso tem suporte apenas em projetos de banco de dados do SSDT e SSMS. Suporte para SQL Server Object Explorer será habilitado em uma versão posterior.


**Atualizações e correções**
* **Ferramentas de banco de dados:**
    - **SSDT:**
        - Bug de conexão 1898001 [Foi corrigido um problema de descrição de coluna com limitação de 128 caracteres](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters).
        - Foi corrigido um problema em que a publicação de um banco de dados do VS não aplicava a propriedade DatabaseServiceObjective no XML de perfil de publicação.
        - Bug de conexão 2900167 [Foi corrigido um problema de teste de unidade que deixava incorretamente arquivos temporários](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind).
        - Foi corrigido um problema em que a caixa de combinação Período de Retenção, em Configurações de Banco de Dados, ficava truncada.
        - Foi corrigido um problema de falta de verificação da senha antiga vazia nas propriedades do projeto CLR do SQL ao trocar de senha.
    - **DACFx:**
        - Foi corrigido um problema em que o nível de compatibilidade da DACFx não era atualizada para o erro SqlAzureV12.
        - Foi corrigido um problema em que propriedade IsAutoGeneratedHistoryTable era incorretamente excluída da comparação de modelos.

- **Analysis Services e Reporting Services**
    - **SSDT:**
        - Foi corrigido um problema no qual o modelo tabular não podia ser salvo quando a conexão do servidor era perdida.
        - Foi corrigido um problema no qual o SSDT se tornava sem resposta devido a um possível problema de loop infinito no AS.
        - Foi corrigido um problema de expressão DAX que causava comportamentos inconsistentes com base em como você confirmava a expressão.
        - Foi corrigido um problema de falha do VS ao criar KPIs.
        - Foi corrigido um problema que gerava relatórios inválidos para o SQL Server 2008 R2, 2012 e 2014.
        - Foi corrigido um problema de ordem de hierarquia que causava um erro de loop infinito para o projeto .dwpro.
        - Foi corrigido um problema do RDL RS em que fazer downgrade do RDL exigia uma recompilação completa, o que gerava confusão no usuário.
        - Foi corrigido um problema de KPI em que Ocultar das Ferramentas de Cliente não tinha nenhum efeito.
        

 
  
## <a name="ssdt-july-for-visual-studio-2015-for-sql-server-2016"></a>SSDT de julho para Visual Studio 2015 (para SQL Server 2016)  
Lançamento: 30 de junho de 2016  
  
Número de build: 14.0.60629.0  
  
**Novidades**  
* **Suporte para Always Encrypted:** para bancos de dados que contêm colunas Always Encrypted, essa versão adiciona suporte completo para o Always Encrypted por meio de nossas principais APIs e da ferramenta de linha de comando (SqlPackage.exe). Você pode criar e publicar projetos de banco de dados com suporte total para todos os recursos Always Encrypted.  
* **Suporte aprimorado a Tabelas Temporais:** a experiência foi simplificada através da desvinculação de tabelas temporais antes das alterações e nova vinculação, depois que as alterações eram concluídas. Isso significa que as Tabelas Temporais têm paridade com outros tipos de tabela (padrão, na memória) em termos das operações as quais elas têm suporte. 
* **Alterações de instalação e da SqlPackage.exe:** alterações para isolar o SSDT do mecanismo do SQL Server e das atualizações do SSMS. Para obter detalhes, consulte [Alterações na instalação e nas atualizações do SSDT e da SqlPackage.exe](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/).

 

**Atualizações e correções**
* **Ferramentas de banco de dados:**
    * De agora em diante o SSDT nunca desabilitará a TDE (Transparent Data Encryption) em um banco de dados. Anteriormente, uma vez que a opção de criptografia padrão nas configurações do banco de dados do projeto era desabilitada, a criptografia seria desligada. Com essa correção, a criptografia pode ser habilitada, mas nunca desabilitada durante a publicação. 
    * Aumento na contagem de novas tentativas e na resiliência para conexões de BD do SQL do Azure durante a conexão inicial.
    * Se o grupo de arquivos padrão não for PRIMARY, importar/publicar no Azure V12 falhará. Agora, essa configuração é ignorada durante a publicação.
    * Foi corrigido um problema em que ao exportar um banco de dados com um objeto com o Identificador entre Aspas ativado, a validação de exportação poderia falhar em alguns casos.
    * Foi corrigido um problema em que a opção TEXTIMAGE_ON era incorretamente adicionada para criações de tabela Hekaton, nas quais isso não é permitido.
    * Foi corrigido um problema em que a exportação de grande quantidade de dados demorava muito tempo, devido a uma gravação no arquivo model.xml depois da conclusão da fase de dados, o que fazia com que o conteúdo do arquivo .bacpac fosse regravado.
    * Foi corrigido um problema em que os usuários não apareciam na pasta Segurança para conexões de APS e SQL DW do Azure.


 * **Analysis Services e Reporting Services:**
    * Foi corrigido um problema de SxS com o provedor OLEDB do MSOLAP em que apenas o provedor de 32 bits era instalado, afetando o Excel 2016 de 64 bits ao se conectar ao SQL Server 2014 (foi não reproduzido com o instalações do ClickOnce do Office365, apenas em instalação do Excel de MSI).
    * Foi corrigido um problema de um caso incomum, para que fosse mais eficiente atualizar o modelo AS com tabelas coladas do nível de compatibilidade 1103 para o 1200, o que poderia resultar no erro "A relação usa uma ID de coluna inválida".
    * Foi corrigido um problema do SxS em que o SSDT-BI 2013, no mesmo computador, não podia mais importar dados em modelo AS após a desinstalação do SSDT 2015 (os cartuchos compartilhavam a configuração do Registro).
    * Robustez aprimorada para resolver problemas/falhas quando a conexão com o mecanismo AS era perdida (ou seja, o SSDT era deixado aberto durante a noite e o servidor AS reciclava ou outros casos em que a conexão era temporariamente perdida). 
    * Problemas corrigidos com caixas de diálogo abrindo em telas diferentes do VS em cenários de vários monitores. 
    * O suporte para colar de tabelas HTML (dados de grade) em tabelas coladas do modelo AS foi corrigido/habilitado. 
    * Foi corrigido o problema em que a atualização falhava ao atualizar uma tabela colada vazia no 1200 (usada somente como tabela de contêiner para medidas). 
    * Foi corrigido um problema com a atualização do modelo tabular AS com tabelas coladas no 1200 para solucionar um problema do mecanismo do AS com CalcTables (que são usadas para Tabelas Coladas no 1200), para realizar um processo completo em novas tabelas calc após a atualização. 
    * Foi corrigido um problema em que o cancelamento da criação de novos modelos de tabela calculada AS 1200 com a expressão DAX incompleta poderia falhar. 
    * Foi corrigido um problema ao importar o modelo 1200 do servidor AS no projeto SSDT AS, em que o nome do BD e um nome de tabela eram os mesmos. 
    * Foi corrigido um problema com a edição de medida do KPI no modelo tabular 1103. 
    * Foi corrigida uma referência de objeto que não definia a exceção encontrada ao colar uma medida de KPI na grade de um modelo 1200 do AS. 
    * Foi corrigido um problema em que uma coluna de uma tabela calculada não podia ser excluída da exibição de diagrama em modelos 1200. 
    * Foi corrigida uma referência de objeto que não definia exceção ao exibir as propriedades de arquivo de projeto model.bim enquanto estava na exibição de código. 
    * Foi corrigido um problema com a colagem de dados em uma grade de modelo AS para criar a tabela colada, que gerava valores incorretos em localidades internacionais, usando a vírgula como separador decimal. 
    * Foi corrigido um problema ao abrir o projeto do RS 2008 no SSDT e escolher não atualizá-lo. 
    * Problema corrigido na interface do usuário nas tabelas calculadas de modelos de nível de compatibilidade 1200 ao usar a formatação padrão para o tipo de coluna para permitir a alteração do tipo de formatação na interface do usuário. 
    

## <a name="ssdt-june-for-visual-studio-2015-for-sql-server-2016"></a>SSDT de junho para Visual Studio 2015 (para SQL Server 2016)  
Lançamento: 1 de junho de 2016  
  
Número de build: 14.0.60525.0 

A GA (Disponibilidade Geral) do SSDT foi lançada. A atualização GA do SSDT de junho de 2016 adiciona suporte para as atualizações mais recentes do SQL Server 2016 RTM e várias correções de bugs. Para obter detalhes, consulte [Atualização GA do SQL Server Data Tools de junho de 2016](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/).

  
  
## <a name="additional-resources"></a>Recursos adicionais
  
[Baixar o SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Versões anteriores do SQL Server Data Tools &#40;SSDT e SSDT-BI&#41;](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md)  
[Novidades do Mecanismo de Banco de Dados](https://msdn.microsoft.com/library/bb510411.aspx)  
[Novidades do Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)  
[Novidades do Integration Services](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
