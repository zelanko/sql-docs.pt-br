---
title: Notas de versão
titleSuffix: Azure Data Studio
description: Notas de versão Data Studio do Azure
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 07/11/2019
ms.openlocfilehash: 9b6fa6e7ec82853e05070a1675154f06091e5092
ms.sourcegitcommit: e366f702c49d184df15a9b93c2c6a610e88fa0fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67826511"
---
# <a name="release-notes-for-azure-data-studio"></a>Notas de versão do estúdio de dados do Azure

**[Baixe e instale a versão mais recente!](download.md)**

## <a name="july-2019"></a>Julho de 2019

11 de julho de 2019 &nbsp;  /  &nbsp; versão: 1.9.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Versão da extensão do Gerenciador de plano SentryOne | Nossa parceira importante da Microsoft, SentryOne, enviará suas [extensão SentryOne planejar Explorer para o Azure Data Studio](https://www.sentryone.com/products/sentryone-plan-explorer-extension-azure-data-studio). <br> Isso é uma extensão gratuita, que fornece diagramas de plano aprimorado para consultas é executada no estúdio de dados do Azure, com os algoritmos de layout otimizado e intuitiva codificação por cores para ajudar a identificar rapidamente os operadores mais caros que afetam o desempenho da consulta. Para saber mais sobre a extensão, confira a postagem do blog do SentryOne [aqui](https://sqlperformance.com/2019/07/sentryone/plan-explorer-extension-azure-data-studio). |
| Novos recursos que virão a comparação de esquemas | &bull; &nbsp; Suporte de arquivo de comparação de esquema (. SCMP) <br/>&bull; &nbsp; Cancelar o suporte a comparação de esquemas <br/>&bull; &nbsp; As alterações completas podem ser encontradas [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed+)|
| Aprimoramentos de bloco de anotações | &bull; &nbsp; Suporte do Python plotly <br/>&bull; &nbsp; Abrir o Notebook do navegador <br/> &bull; &nbsp; Caixa de diálogo gerenciamento de pacotes do Python <br/> &bull; &nbsp; Aprimoramentos de desempenho e Markdown <br/> &bull; &nbsp; Atualização de atalhos de teclado <br/>  &bull; &nbsp; Correções de bugs e recursos podem ser encontrados [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22+) |
| SQL Server 2019 Support |  Esta versão inclui suporte para recursos de Cluster de Big Data do SQL Server de 2019 adicionais, incluindo: <br/> &bull; &nbsp; Tabela de pontos de extremidade de serviço dentro do painel de gerenciamento do que lista todos os principais serviços no cluster. <br/> &bull; &nbsp; O bloco de anotações do cluster Status mostra como você pode consultar e solucionar problemas de status do cluster em todos os serviços e os pods.| 
| Pacotes de idiomas atualizado disponível| Agora há 10 pacotes de idiomas disponíveis no marketplace do Gerenciador de extensões. Simplesmente, pesquise o idioma específico usando o marketplace de extensão e instalar. Depois de instalar o idioma selecionado, o Studio de dados do Azure solicitará que você reiniciar com a nova linguagem. |
| Atualização do SQL Server Profiler | A extensão de perfil do SQL Server foi atualizada para incluir novos recursos, incluindo: <br/> &bull; &nbsp; Filtrando pelo nome do banco de dados <br/> &bull; &nbsp; Copie e cole o suporte <br/> &bull; &nbsp; Salvar/carregar filtro <br/>Encontre uma lista completa das melhorias para a extensão do SQL Server Profiler [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+SQL+Profiler%22+).  |
| Código do Visual Studio versão de maio de mesclagem 1.35 | Melhorias mais recentes podem ser encontradas [aqui](https://code.visualstudio.com/updates/v1_35). |
| Problemas e bugs resolvidos | Em versões anteriores do Studio de dados do Azure, se um banco de dados do usuário foi selecionado ao conectar-se a caixa de diálogo de Conexão, a entrada do Pesquisador de objetos resultante foi no escopo totalmente esse único banco de dados. Começando nesta versão, que o comportamento está sendo alterado para que as propriedades de nível de servidor também são mostradas no Pesquisador de objetos. <br/> Para obter uma lista completa de correções, consulte [Bugs e problemas no GitHub](https://github.com/microsoft/azuredatastudio/milestone/35?closed=1). |
| &nbsp; | &nbsp; |


## <a name="june-2019"></a>Junho de 2019

6 de junho de 2019 &nbsp;  /  &nbsp; versão: 1.8.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Versão da extensão de servidores de gerenciamento Central (CMS) | Servidores de gerenciamento central armazenam uma lista de instâncias do SQL Server que é organizado em um ou mais grupos de servidores de gerenciamento central. Os usuários podem se conectar a seus próprios servidores CMS existentes e gerenciar os servidores como adicionar e remover servidores. Para saber mais, você pode ler [aqui](https://docs.microsoft.com/sql/relational-databases/administer-multiple-servers-using-central-management-servers) |
| Versão das extensões de ferramenta de administração de banco de dados para Windows | Essa extensão inicia duas das experiências mais usadas no SQL Server Management Studio no Studio de dados do Azure. Usuários podem clicar em vários objetos diferentes (como bancos de dados, tabelas, colunas, exibições e muito mais) e selecione Propriedades para exibir a caixa de diálogo de propriedades do SSMS para esse objeto. Além disso, os usuários podem clique com botão direito em um banco de dados e selecione Gerar Scripts para iniciar o Assistente do SSMS gerar Scripts bem conhecido. 
| Aperfeiçoamentos de comparação de esquema | &bull; &nbsp; Adicionado exclui/inclui opções <br/>&bull; &nbsp; Gerar Script de script é aberto após o que está sendo gerado <br/>&bull; &nbsp; Removidas as barras de rolagem duplas  <br/>&bull; &nbsp; Melhorias de formatação e layout <br/>&bull; &nbsp; As alterações completas podem ser encontradas [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed)|
| Seção de mensagens movida para a própria guia | Quando os usuários executar consultas SQL, resultados e mensagens foram nos painéis de gráfico empilhados. Agora eles estão em guias separadas em um painel, como no SSMS. |
| Aprimoramentos de bloco de anotações do SQL | &bull; &nbsp; Agora, os usuários podem escolher usar suas próprias instalações de Python 3 ou Anaconda em blocos de anotações <br/>&bull; &nbsp; Vários estabilidade + correções de ajuste/término <br/> &bull; &nbsp; Exibir a lista completa de melhorias [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22)|
| Código do Visual Studio versão de maio de mesclagem 1.34 | Melhorias mais recentes podem ser encontradas [aqui](https://code.visualstudio.com/updates/v1_34) |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/microsoft/azuredatastudio/milestone/32?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas Conhecidos
- Extensões de ferramentas de administração de banco de dados para Windows
    - Não é possível iniciar as propriedades de nó de servidor desconectada
    - Não é possível inicializar as propriedades para os servidores do Azure
    - Nem todos os objetos têm caixas de diálogo de propriedade
    - Caixas de diálogo levar muito tempo para ser inicializado
    - Erros de inicialização servidores com alguns tipos de conexões (por exemplo, o AAD)
- Notebooks
    - [5838](https://github.com/microsoft/azuredatastudio/issues/5838) permitem que os usuários usem o sistema Python de blocos de anotações
- Comparação de esquemas
    - [5804](https://github.com/microsoft/azuredatastudio/issues/5804) tarefas de comparação de esquemas mostram menu de contexto de cancelamento padrão que não faz nada

## <a name="may-2019"></a>Maio de 2019

8 de maio de 2019 &nbsp;  /  &nbsp; versão: 1.7.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Versão da extensão de comparação de esquemas | Comparação de esquemas é um recurso conhecido no SSDT SQL Server Data Tools () e seu caso de uso principal é comparar e visualizar as diferenças entre os bancos de dados e arquivos. dacpac e para executar ações para fazer o mesmo. |
| Movido o modo de exibição de tarefas à janela de saída | Os usuários agora podem exibir o status das tarefas de longa execução, como Backup, restauração e comparação de esquemas na exibição de tarefa na janela de saída
| Página de boas-vindas adicionada | &bull; &nbsp; Links para ações comuns, como a nova consulta, o novo arquivo, novo Notebook <br/>&bull; &nbsp; Links para documentação e GitHub |
| Aprimoramentos de bloco de anotações do SQL | &bull; &nbsp; Aprimoramentos de renderização de markdown, incluindo melhor suporte para tabelas e anotações <br/>&bull; &nbsp; Aperfeiçoamentos na usabilidade para a barra de ferramentas <br/>&bull; &nbsp; Links de markdown para blocos de anotações confiáveis não exigem Ctrl/Cmd + clique e podem ser clicados diretamente <br/>&bull; &nbsp; Melhorias na limpeza dos processos de Jupyter depois de fechar os blocos de anotações e reduz os erros ao iniciar vários blocos de anotações simultaneamente <br/>&bull; &nbsp; Melhorias para conexões de bloco de anotações do SQL para garantir que os erros não ocorrerão quando executar blocos de 2 anotações no mesmo banco de dados <br/>&bull; &nbsp; Melhorias na rolagem automática de bloco de anotações para a célula em execução no momento ao clicar no botão Executar células da barra de ferramentas <br/>&bull; &nbsp; Melhorias gerais de estabilidade e desempenho |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/microsoft/azuredatastudio/milestone/31?closed=1). |
| &nbsp; | &nbsp; |

## <a name="april-2019"></a>Abril de 2019

18 de abril de 2019 &nbsp;  /  &nbsp; versão: 1.6.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Renomeado **servidores** pressionar tab até **conexões** | |
| Movido o Gerenciador de recursos do Azure como um viewlet do Azure em conexões | Os usuários agora podem exibir suas instâncias de SQL do Azure por meio do Azure viewlet na exibição de conexões e expanda para exibir objetos em cada servidor ou banco de dados.|
| Aprimoramentos de bloco de anotações do SQL | &bull; &nbsp; Adição de botão na barra de ferramentas para limpar a saída para todas as células <br/>&bull; &nbsp; Adição de botão na barra de ferramentas para executar todas as células <br/>&bull; &nbsp; Nome de conexão fixo em vez do nome do servidor (se definido) na anexar ao menu suspenso <br/>&bull; &nbsp; Correção para imagens em markdown não renderizar ao usar caminhos relativos de imagem <br/>&bull; &nbsp; Funcionalidade aprimorada em grades de bloco de anotações, adicionando duas vezes o tamanho da coluna de redimensionamento automático e melhoraram o suporte de mousewheel <br/>&bull; &nbsp; Melhorias para tratamento de erros e python instalem resiliência ao instalar o python por meio de blocos de anotações <br/>&bull; &nbsp; Aprimoramentos à funcionalidade "Selecionar tudo" ao selecionar células do bloco de anotações <br/>&bull; &nbsp; Melhorias para conexões de bloco de anotações para impedir que um bloco de anotações de fechamento e afetando uma conexão do Gerenciador de objeto <br/>&bull; &nbsp; Experiência de notebook aprimorado para exibir uma mensagem ao usuário quando desconectado de bloco de anotações e precisa de uma conexão para executar células<br/>&bull; &nbsp; Suporte aprimorado para blocos de anotações não salvos ao reidratar em anúncios quando anúncios for iniciado novamente |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1). |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>Março de 2019 (Hotfix)

22 de março de 2019 &nbsp;  /  &nbsp; versão: 1.5.2 &nbsp;  /  &nbsp; versão do Hotfix

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Correção de alguns problemas descobertos na 1.5.1. | Ver [março de versão do Hotfix, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/28).<br/> <br/>&bull; &nbsp; Corrigido um problema em que o usuário não foi possível fechar aberto da tarefa "Abrir Notebook" no painel de controle de bloco de anotações <br/>&bull; &nbsp; Corrigido o problema em que o bloco de anotações do JSON tem extra} depois de salvar <br/>&bull; &nbsp; Problema corrigido onde grades de notebook não estão respondendo às alterações de tema <br/>&bull; &nbsp; Correção do problema em que caminho completo do bloco de anotações foi exibido no cabeçalho da guia. Agora, somente o nome do arquivo é mostrado. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>Março de 2019

18 de março de 2019 &nbsp;  /  &nbsp; versão: 1.5.1

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Adicionado [extensão PostgreSQL para o Studio de dados do Azure](postgres-extension.md) | Recursos com suporte: <br/>&bull; &nbsp; Caixa de diálogo de Conexão <br/>&bull; &nbsp; Pesquisador de objetos <br/>&bull; &nbsp; Editor de consultas <br/>&bull; &nbsp; Criação de gráficos <br/>&bull; &nbsp; Painéis <br/>&bull; &nbsp; Trechos de código <br/>&bull; &nbsp; Editar dados <br/>&bull; &nbsp; Blocos de anotações |
| Blocos de anotações do SQL adicionado | Adicionado suporte do Kernel do SQL ao Visualizador interno de bloco de anotações: <br/>&bull; &nbsp; Dá suporte a T-SQL <br/>&bull; &nbsp; Suporte PGSQL |
| Extensão do PowerShell adicionada  | Traz o [extensão do PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) experiência do VS Code.  |
| Extensão de dacpac do SQL Server adicionada  | Remove Data-Tier Application Wizard da extensão de importação do SQL Server em uma nova extensão.  |
| Extensões de comunidade adicionada QueryPlan.show | Adiciona o suporte de integração para visualizar os planos de consulta  |
| Extensão de visualização do SQL Server de 2019 atualizado | &bull; &nbsp; Suporte de Jupyter Notebook, especificamente kernels de Python3 e Spark, foram movidos para a ferramenta de Azure Data Studio core. <br/>&bull; &nbsp; Correções de bugs para o Assistente de dados externa  |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas Conhecidos
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): Ao clicar em Run na célula antes de Kernel estiver pronta para resultados de Spark em um Erro Fatal **solução alternativa:** Aguarde até que os kernels são carregados até executar todas as células
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): ANÚNCIOS iniciados a partir do SSMS usando a autenticação do SQL - prompts de senha do usuário **solução alternativa:** Use a autenticação do Windows por enquanto. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): Não é possível instalar o recurso de bloco de anotações do SQL <br/>
**Solução alternativa:** Siga as etapas de solução [aqui](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832). 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): O estúdio de dados do Azure não pode ser aberto diretamente na pasta Downloads (Mac) <br />
**Solução alternativa:** Reinicie o computador depois de descompactar o aplicativo. Serão investigados. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  Salvar como do bloco de anotações perde o contexto de conexão <br />
**Solução alternativa:** Será corrigido na próxima versão. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): Extrair Dacpac falhar SqlToolsService se versão inválida for usada <br/>
**Solução alternativa:** Reiniciar o Studio de dados do Azure e verifique se a versão correta é usada.
- Novos ícones de bloco de anotações e abrir Notebook são perdidos <br/> 
**Solução alternativa:** O tipo de conexão herdado foi preterido. Recomendamos que você se conectar ao ponto de extremidade do SQL Server e você obterá todas as ações (novo bloco de anotações, o trabalho do Spark) conforme o esperado. 

## <a name="february-2019"></a>Fevereiro de 2019

13 de fevereiro de 2019 &nbsp;  /  &nbsp; versão: 1.4.5

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Adicionado **Admin pack para SQL Server** pacote de extensão. | Isso torna mais fácil de instalar as extensões relacionadas à administração do SQL Server. Isso inclui:<br/>&bull; &nbsp; [SQL Server Agent](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension)<br/>&bull; &nbsp; [SQL Server Import](sql-server-import-extension.md?view=sql-server-2017) |
| Suporte de evento na extensão do Profiler estendido de filtragem adicional. | &nbsp; |
| Salvar adicionado como recurso de XML que pode salvar os resultados do T-SQL como XML. | &nbsp; |
| Foram incluídos aperfeiçoamentos de Data-Tier Application Wizard. | &bull; &nbsp; Botão de script gerar adicionado<br/>&bull; &nbsp; Modo de exibição adicional para dar avisos de possível perda de dados durante a implantação. |
| Atualizações da extensão de visualização do SQL Server de 2019. | Ver [extensão de visualização do SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Resultados de streaming habilitado por padrão por muito tempo executando consultas. | &nbsp; |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1). |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>Janeiro de 2019 (Hotfix)

16 de janeiro de 2019 &nbsp;  /  &nbsp; versão: 1.3.9 &nbsp;  /  &nbsp; versão do Hotfix

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Correção de alguns problemas descobertos na 1.3.8. | Ver [versão do Hotfix de janeiro, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).<br/><br/>Para obter informações detalhadas, consulte:<br/>&bull; &nbsp; [Log de alterações, no GitHub](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).<br/>&bull; &nbsp; [Versões, no GitHub](https://github.com/Microsoft/azuredatastudio/releases). |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>Janeiro de 2019

09 de janeiro de 2019 &nbsp;  /  &nbsp; versão: 1.3.8

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Adicionado um novo instalador do usuário para Windows. | Ao contrário do instalador do sistema existente, o novo instalador do usuário não requer privilégios de administrador. Isso também permite uma experiência de atualização mais fácil para não administradores. |
| Adicionado suporte de autenticação do Active Directory do Azure. | &nbsp; |
| Anunciando a análise de desempenho de DM Idera SQL (versão prévia). | &nbsp; |
| Suporte de data-Tier Application Wizard na extensão do SQL Server Import. | &nbsp; |
| Atualize para a extensão de visualização do SQL Server de 2019. | Ver [extensão de visualização do SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Aprimoramentos do SQL Server Profiler. | &nbsp; |
| Resultados de Streaming para grandes consultas (visualização). | &nbsp; |
| Extensões de comunidade: sp_executesql to sql e o novo banco de dados. | &nbsp; |
| Bugs resolvidos e problemas. | Ver [Bugs e problemas no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1). |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>Novembro de 2018

6 de novembro de 2018 &nbsp;  /  &nbsp; versão: 1.2.4

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Atualize para a extensão de visualização do SQL Server de 2019. | Ver [extensão de visualização do SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Introdução ao colar a extensão de plano. | &nbsp; |
| Apresentando a extensão de consultas de High Color, incluindo o tema do editor SSMS. | &nbsp; |
| Correções no SQL Server Agent, Profiler e importação de extensões. | &nbsp; |
| Corrigir o.Net Core fazendo com que o soquete KeepAlive problema quedas de conexões inativas no macOS. | &nbsp; |
| Serviço de ferramentas de atualização do SQL para.Net Core 2.2 Preview 3 (para eventual suporte do AAD). | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Correções de bugs, novembro de 2018

- Corrigir [emitir #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexão perdida para BD SQL do Azure
- Corrigir [emitir #2914](https://github.com/Microsoft/azuredatastudio/issues/2914): Nó "Argumento inválido" exceção expansão OE banco de dados
- Corrigir [emitir #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Exibir mensagens de várias linhas corretamente nos resultados da consulta
- Corrigir [emitir #2906](https://github.com/Microsoft/azuredatastudio/pull/2906): Corrija o nome do documento de editar dados quando o nome da tabela contém caracteres especiais
- Corrigir [emitir #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): Compilado na extensão de log de alterações diz para verificar as notas de versão do VSCode para alterações
- Corrigir [emitir #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): Tema de alto contraste duplos/triplos de ícones
- Corrigir [emitir #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Adicionar uma interface de linha de comando para se conectar a um SQL Server
- Corrigir [emitir #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Adicionar suporte de tema do plano de consulta

## <a name="october-2018"></a>Outubro de 2018

29 de outubro de 2018 &nbsp;  /  &nbsp; versão: 1.1.4

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Apresentando o Azure Resource Explorer para procurar bancos de dados SQL do Azure. | &nbsp; |
| Aumentar a robustez de conectividade do Pesquisador de objetos e o Editor de consultas. | &nbsp; |
| Melhorias de extensões do SQL Agent. | &nbsp; |
| Atualize para a extensão de visualização do SQL Server de 2019. | Ver [extensão de visualização do SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Correções de bugs, de outubro de 2018

- Corrigir [emitir #2717](https://github.com/Microsoft/azuredatastudio/issues/2717): O resultado de coluna XML, clico em formatação
- Corrigir [emitir #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Windows de resultado da largura está incompleta
- Corrigir [emitir #2999](https://github.com/Microsoft/azuredatastudio/issues/2999): Não foi possível carregar o arquivo Tracing no Mac ao se conectar ao banco de dados
- Corrigir [emitir #2851](https://github.com/Microsoft/azuredatastudio/issues/2851): Gráfico de série temporal não sejam renderizadas corretamente
- Corrigir [emitir #2996](https://github.com/Microsoft/azuredatastudio/issues/2996): Tabela temporária perda devido a alteração repentina de sessão

Para obter informações detalhadas, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-ga-release"></a>Setembro de 2018 (versão de GA)

24 de setembro de 2018 &nbsp;  /  &nbsp; versão: 1.0 &nbsp;  /  &nbsp; versão GA

Versão de disponibilidade geral do estúdio de dados do Azure (anteriormente conhecido como o SQL Operations Studio).

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Grade de resultados melhorias no desempenho e experiência do usuário para um grande número de conjuntos de resultados de consulta. | &nbsp; |
| Código de origem do Visual Studio Code é atualizada de 1.23 para 1.26.1 com Layout de grade e o melhor Editor de configurações (visualização). | &nbsp; |
| Melhorias de acessibilidade para o leitor de tela, navegação por teclado e alto contraste. | &nbsp; |
| Adicionado `Connection name` permite que você forneça um nome de exibição alternativa que o modo de exibição de servidores-let. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>Anunciando a extensão de visualização do SQL Server de 2019

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Suporte para recursos de visualização do SQL Server 2019 incluindo [cluster de big data](../big-data-cluster/big-data-cluster-overview.md) dão suporte. | Conecte-se ao Gateway de HDFS/Spark que acompanha a versão prévia do SQL Server 2019.<br/><br/>Procurar HDFS, carregar arquivos, salvar arquivos e iniciar ações úteis, como analisar no bloco de anotações para arquivos CSV.<br/><br/>Enviar trabalhos do Spark no painel ou clique duas vezes em uma conexão de HDFS/Spark no Pesquisador de objetos. |
| Blocos de anotações do Studio dados do Azure. | Criar ou abrir Notebooks usando um visualizador de bloco de anotações integrado. Nesta versão, o bloco de anotações visualizador dá suporte à conexão para kernels locais e o cluster de big data 2019 do SQL Server somente.<br/><br/>Use as bibliotecas de PROSA acelerador de código no bloco de anotações para saber os tipos de dados e formato de arquivo para a preparação de dados rápido. |
| Gerenciador de recursos do Azure. | O modo de exibição do Gerenciador de recursos do Azure permite procurar pontos de extremidade relacionados a dados para suas contas do Azure e criar conexões para eles no Pesquisador de objetos. Nesta versão, servidores e bancos de dados SQL do Azure têm suporte. |
| PolyBase do SQL Server criar Assistente de tabela externa. | Crie uma tabela externa e suas estruturas de metadados de suporte com um assistente fácil de usar. Nesta versão, há suporte para servidores remotos do SQL Server e Oracle. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Correções de bugs, setembro de 2018

- Corrigir [emitir #2647](https://github.com/Microsoft/azuredatastudio/issues/143): Os gráficos fez um grande avanço com versões anteriores.
- Corrigir [emitir #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que retorna a coluna inteira de hyperlinks JSON.

Para obter informações detalhadas, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="august-2018"></a>Agosto de 2018

30 de agosto de 2018 &nbsp;  /  &nbsp; versão: 0.32.8 &nbsp;  /  &nbsp; visualização pública

O *agosto Public Preview* se concentra em correções de bugs, estabilização do produto e preenchendo as lacunas nos cenários existentes.

_0.32.8 contém correções para algumas regressões, encontradas no 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Anunciando a extensão de importação do SQL Server. | &nbsp; |
| Gerenciamento de sessão do SQL Server Profiler. | &nbsp; |
| Suporte de modelo de sessão do SQL Server Profiler. | &nbsp; |
| Aprimoramentos do SQL Server Agent. | &nbsp; |
| Nova extensão de comunidade: Kit de Respondente primeiro. | &nbsp; |
| Aprimoramentos de qualidade de vida: Cadeias de conexão | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Correções de bugs, agosto de 2018

- Analisar o SQL em uma janela do Editor de consultas usando o `Parse Syntax` comando.
- Corrigir [emitir #143](https://github.com/Microsoft/azuredatastudio/issues/143): Clique duas vezes não selecionando no nome da variável.
- Corrigir [emitir #387](https://github.com/Microsoft/azuredatastudio/issues/387): Ícone de banco de dados do SQL guia é vermelho.
- Corrigir [emitir #825](https://github.com/Microsoft/azuredatastudio/issues/825): Solicitação: Conexão automática para o servidor atual após o Script como... 
- Corrigir [emitir #1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [Entry da área de trabalho] – com redundância de valor para o nome do & comentário.
- Corrigir [emitir #1285](https://github.com/Microsoft/azuredatastudio/issues/1285): Atualizando o ícone do aplicativo faz com que seja removido/substituído no Windows.
- Corrigir [emitir #1317](https://github.com/Microsoft/azuredatastudio/issues/1317): Corrija o separador decimal.
- Corrigir [emitir #1474](https://github.com/Microsoft/azuredatastudio/issues/1474): Cancelar alteração conexão se desconecta a conexão atual.
- Corrigir [emitir #1497](https://github.com/Microsoft/azuredatastudio/issues/1497): Exibir como as opções são cortadas na parte inferior do gráfico.
- Corrigir [emitir #1524](https://github.com/Microsoft/azuredatastudio/issues/1524): Shell/Dashboard: Ícones de viewlet principal são arrastáveis e podem travar o aplicativo.
- Corrigir [emitir #1578](https://github.com/Microsoft/azuredatastudio/issues/1578): Não é possível expandir/recolher pasta do navegador de arquivos remoto clicando no nome.
- Corrigir [emitir #1620](https://github.com/Microsoft/azuredatastudio/issues/1620): Sugestão de recurso: Obtenha a cadeia de caracteres de Conexão para a conexão existente.
- Corrigir [emitir #1624](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox não muda de cor quando desabilitado.
- Corrigir [emitir #1728](https://github.com/Microsoft/azuredatastudio/issues/1728): Salve como JSON/EXCEL/CSV não funcionará.
- Corrigir [emitir #1744](https://github.com/Microsoft/azuredatastudio/issues/1744): Painel de resultados perde suas posições de rolagem ao alternar entre as guias.
- Corrigir [emitir #1748](https://github.com/Microsoft/azuredatastudio/issues/1748): Mensagem de erro ao salvar a hora de arquivo segunda (e subsequentes) do Excel.
- Corrigir [emitir #1782](https://github.com/Microsoft/azuredatastudio/issues/1782): Editar dados: célula não reverter para o valor original na pressionar a tecla ESC.
- Corrigir [emitir #1836](https://github.com/Microsoft/azuredatastudio/issues/1836): arquivos. SQL não está associados com o SQL Operations Studio.
- Corrigir [emitir #1850](https://github.com/Microsoft/azuredatastudio/issues/1850): Digitação N ' preenche automaticamente a N ' '.
- Corrigir [emitir #1985](https://github.com/Microsoft/azuredatastudio/issues/1985): Cópia da grade de resultados de consulta é desativada por 1 coluna.
- Corrigir [emitir #1998](htpts://github.com/Microsoft/azuredatastudio/pull/1998): Adicione a versão do VS Code para caixa de diálogo sobre.
- Corrigir [emitir #2042](https://github.com/Microsoft/azuredatastudio/pull/2042): Agente: Habilitação do botão Importar consultas de arquivos do sql.
- Corrigir [emitir #2091](https://github.com/Microsoft/azuredatastudio/issues/2091): Não pode usar o atalho Ctrl + C para copiar do painel de resultados.
- Corrigir [emitir #2099](https://github.com/Microsoft/azuredatastudio/pull/2099): Adição de mais opções de saveAsCsv.
- Corrigir [emitir #2107](https://github.com/Microsoft/azuredatastudio/issues/2107): Atualize ícone do documento para documentos de painel e o Profiler.
- Corrigir [emitir #2129](https://github.com/Microsoft/azuredatastudio/pull/2129): Salve a posição de rolagem de dados de edição ao alternar guias.
- Corrigir [emitir #2152](https://github.com/Microsoft/azuredatastudio/issues/2152): Indicador de linha de grade de resultados baseado em Zero.

### <a name="known-issues-august-2018"></a>Problemas conhecidos, agosto de 2018

- [Emitir #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Salvar como apenas salva primeira linha de dados do Excel
- [Emitir #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Não é possível conectar-se no Ubuntu 16.04 to SQL em um contêiner

## <a name="july-2018"></a>Julho de 2018

19 de julho de 2018 &nbsp;  /  &nbsp; versão: 0.31.4 &nbsp;  /  &nbsp; visualização pública

O *julho de visualização pública* se concentra nos seguintes itens:

- A versão inicial dos cenários de configuração do SQL Server Agent.
- Aprimoramentos de modelo de sessão e modo de exibição da SQL Server Profiler.
- Correções de bugs contínuas do cliente relatados problemas do GitHub.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| [SQL Server Agent para a extensão do SQL Operations Studio](sql-server-agent-extension.md) melhorias. | Adicionada a exibição de alertas, operadores e Proxies e ícones no painel esquerdo.<br/><br/>Caixas de diálogo adicionadas para o novo trabalho, nova etapa de trabalho, novo alerta e operador novo.<br/><br/>Adicionado Delete Job, excluir alerta e operador excluir (botão direito do mouse).<br/><br/>Visualização de execuções anteriores adicionada.<br/><br/>Filtros adicionados para cada nome de coluna. |
| [SQL Server Profiler para a extensão do SQL Operations Studio](sql-server-profiler-extension.md) melhorias. | Adicionado 5 modelos padrão para exibir eventos estendidos.<br/><br/>Nome de conexão de servidor/banco de dados adicionado.<br/><br/>Adicionado suporte para instâncias de banco de dados SQL.<br/><br/>Sugestão adicionado para sair do Profiler quando o guia é fechada quando o Profiler ainda está em execução. |
| Versão da extensão de Scripts de combinar. | &nbsp; |
| Pontos de extensibilidade de caixa de diálogo e Assistente adicionados para autores de extensão. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Correções de bugs, julho de 2018

- Corrigir [emitir 728](https://github.com/Microsoft/azuredatastudio/issues/728): Não há resposta para Adicionar Conexão no macOS
- Corrigir [emitir 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): Exibição de texto da grade de resultados é bagunçada por caracteres internacionais
- Corrigir [emitir 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): A caixa de diálogo de backup: Navegador de arquivos da interface do usuário é interrompida
- Corrigir [emitir 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): Número de linhas afetadas
- Corrigir [emitir 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): Não é possível conectar a qualquer fonte de dados
- Corrigir [emitir 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError ao se conectar ao servidor
- Corrigir [emitir 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): Caixas de diálogo de extensão tem parado de funcionar
- Corrigir [emitir 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): BUG: Obtém os dados HTML em uma coluna interpretados
- Corrigir [emitir 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): Extensibilidade: se você adicionar um provedor de conexão desinstalação nunca o removerá da lista
- Corrigir [emitir 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Extensões Sqlops: queryeditor.connect() se conecta ao banco de dados de destino, mas a interface do usuário não mostra que o editor está conectado
- Corrigir [emitir 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): Gráfico de tamanho de 10 DB superior não funciona em instâncias diferencia maiusculas de minúsculas
- Corrigir [emitir 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): definição de tipo de erro de digitação sqlops.d.ts causando 'any' implícito
- Corrigir [emitir 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Erro de Ortografia
- Corrigir [emitir 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): Definindo iconPath no ButtonComponent depois component() é chamado não altera o ícone
- Corrigir [emitir 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): Uma melhor organização de tabela

## <a name="june-2018"></a>Junho de 2018

20 de junho de 2018 &nbsp;  /  &nbsp; versão: 0.30.6 &nbsp;  /  &nbsp; visualização pública

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| **SQL Server Profiler para SQL Operations Studio _versão prévia_**  versão inicial da extensão. | &nbsp; |
| O novo **SQL Data Warehouse** extensão inclui widgets de painel personalizável avançado identificando insights ao seu data warehouse. | Isso desbloqueia os principais cenários de gerenciamento e ajuste seu data warehouse para garantir que ele é otimizado para desempenho consistente. |
| **Editar dados "Filtragem e classificação"** dão suporte. | &nbsp; |
| **SQL Server Agent para o SQL Operations Studio _versão prévia_**  aprimoramentos de extensão para trabalhos e o histórico de trabalho de modos de exibição. | &nbsp; |
| Aprimorado **Assistente de & estrutura do construtor de interface do usuário de caixa de diálogo** APIs de extensibilidade. | &nbsp; |
| Atualize o código-fonte de plataforma de código do VS. | Integrado as seguintes versões:<br/>&bull; &nbsp; [Março de 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [Abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>Correções de problemas do GitHub, junho de 2018

- Solicitação de recurso ([emitir 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Verifique os resultados da largura da coluna de ajuste automático de grade para dados e lembre-se de alterações manuais se a mesma consulta for executada novamente.
- Corrigir [emitir 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Deve mostrar adicione mensagem e botão conta quando a conta vinculada está vazia.
- Corrigir [emitir 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): Guia Conta vinculada é interrompido quando o modo de exibição é recolhido.
- Corrigir [emitir 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): Serviço de ferramentas do SQL Falha ao abrir o arquivo. SQL no disco.
- Corrigir [emitir 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Faltando "BETWEEN" palavra-chave SQL.
- Corrigir [emitir 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Palavra-chave de 'MATCH' falhas de serviço de ferramentas do SQL.
- Corrigir [emitir 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): "Novo Profiler" opção de menu de contexto no Pesquisador de objetos não faz nada.
- Corrigir [emitir 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): Plano de consulta de "Explain" de editor de consulta é interrompido.

## <a name="may-2018"></a>Maio de 2018

7 de maio de 2018 &nbsp;  /  &nbsp; versão: 0.29.3 &nbsp;  /  &nbsp; visualização pública

O *visualização pública podem* se concentra na estabilização e correções de bugs.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Anunciando a extensão do Redgate SQL Search disponível no Gerenciador de extensões. | &nbsp; |
| Localização da comunidade disponível para 10 idiomas. | Alemão, espanhol, francês, italiano, japonês, coreano, português, russo, chinês simplificado e chinês tradicional. |
| Alterações da coleção de telemetria. | &bull; &nbsp; Coleta de telemetria reduzido.<br/>&bull; &nbsp; Experiência aprimorada de recusá-la.<br/>&bull; &nbsp; Links do produto para declaração de privacidade. |
| Gerenciador de extensões tem Marketplace aprimorado de experiência. | Descobrir mais facilmente as extensões de comunidade. |
| Extensão do SQL Agent. | &bull; &nbsp; Trabalhos.<br/>&bull; &nbsp; Melhoria do modo de exibição de histórico do trabalho. |
| Atualizações para whoisactive e extensões do relatórios do servidor. | &nbsp; |
| Aprimorada a rolagem de gerenciar propriedades do painel. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>Corrigir problemas do GitHub

- Corrigir [execute 703](https://github.com/Microsoft/azuredatastudio/issues/703): Inserir texto do tipo HTML em dados de edição faz com que o valor a ser exibido incorretamente após atualização
- Corrigir [emitir 821](https://github.com/Microsoft/azuredatastudio/issues/821): dependência de pacote azuredatastudio.deb
- Corrigir [emitir 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palavra-chave 'distinct' não realçado
- Corrigir [emitir 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Editar dados reverter linha não funciona
- Corrigir [emitir 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensão do agente SQL e a barra de status
- Corrigir [emitir 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Redimensionamento do SQL Agent não depois altere o tamanho do windows

## <a name="april-2018"></a>Abril de 2018

25 de abril de 2018 &nbsp;  /  &nbsp; versão: 0.28.6 &nbsp;  /  &nbsp; visualização pública

O *abril de visualização pública* contém correções de bugs e melhorias.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Aprimoramentos para a extensão de visualização do agente SQL: | &nbsp; |
| &nbsp; &nbsp; &nbsp; Suporte aprimorado para arquivos. | &bull; &nbsp; Arquivos grandes.<br/>&bull; &nbsp; Arquivos protegidos, para salvar administrador protegida.<br/>&bull; &nbsp; Armazenando \>256m arquivos dentro do SQL Operations Studio. |
| &nbsp; &nbsp; &nbsp; Divisão de Terminal integrado. | Trabalhe com vários terminais abertos simultaneamente. |
| &nbsp; &nbsp; &nbsp; Instalações mais rápidas e tempos de inicialização. | Instalação reduzida de impressão pés de contagem do arquivo em disco. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>Corrigir problemas do GitHub, abril de 2018

- Corrigir [emitir 37](https://github.com/Microsoft/azuredatastudio/issues/37): Quando o Visualizador gráfico gera um erro, ocorre um comportamento inesperado.
- Corrigir [emitir 462](https://github.com/Microsoft/azuredatastudio/issues/462): Solicitação de recurso: Opção para grupos de servidores ser expandido por padrão.
- Corrigir [emitir 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense - sugestão incorreta para o comando 'Atualizar'.
- Corrigir [emitir 967](https://github.com/Microsoft/azuredatastudio/issues/967): Esperar que o plano de consulta quando seleciona o plano de execução XML na grade de resultado.
- Corrigir [emitir 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): Adicione os colchetes para chamada ms_foreachdb de flyfishingdba.
- Corrigir [emitir 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): Erro de handshake SSL/TLS de pré-logon.
- Corrigir [emitir 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): Modo de exibição de insights não criptografado antes de mostrar o erro.
- Corrigir [emitir 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): Novas ações de consulta no Gerenciador de widget e restauração foram interrompidas.
- Corrigir [emitir 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): Painel Saída windows pops-up com a mensagem de erro para o banco de dados SQL.
- Corrigir [emitir 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): Caixa de diálogo de Conexão mostra erro de servidor necessárias ao exibido inicialmente.
- Corrigir [emitir 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): Grupos de servidores agora precisam de um clique duplo para expandir.
- Corrigir [emitir 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): Plano de fundo do controle de seleção é semitransparente.
- Corrigir [emitir 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Corrigi problemas de acessibilidade de todos os alto contraste no SQL Operations Studio.
- Corrigir [emitir 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): Falha de extensão para atualização "baixar manualmente" link vai para o local errado.
- Corrigir [emitir 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): Rolagem de V não está funcionando na guia página inicial.
- Corrigir [emitir 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): Guias de extensão SQL parou de funcionar.

### <a name="visual-studio-code-121-platform"></a>Plataforma do Visual Studio código 1.21

Um realce para a visualização de abril pública é a atualização do código-fonte para a plataforma 1.21 de código do Visual Studio. Isso traz várias atualizações para o editor de núcleo e Bancada de trabalho do ponto de 1.19 sincronização anterior. Alguns exemplos incluem o seguinte:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| [Novas notificações de interface do usuário](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui). | Gerenciar facilmente e as notificações do SQL Operations Studio. |
| [Integrado a divisão de Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals). | Trabalhar com vários terminais abertos ao mesmo tempo. |
| [Salvar arquivos grandes e protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges). | Salvar administrador protegida e \>256m arquivos dentro do SQL Operations Studio. |
| [Melhor suporte de arquivo grande](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements). | Otimizações de buffer de texto para arquivos grandes. |
| [Uma pesquisa aperfeiçoada configurações](https://code.visualstudio.com/updates/v1_20#_settings-search). | Localize facilmente a configuração correta com a pesquisa em idioma natural. |
| [Trechos de código globais](https://code.visualstudio.com/updates/v1_20#_global-snippets). | Crie trechos de código que você pode usar em todos os tipos de arquivo. |
| [Seleção múltipla do Explorer](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer). | Execute ações em vários arquivos ao mesmo tempo. |
| [Erros e avisos no Explorer](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer). | Navegar rapidamente para erros em sua base de código. |
| [Arrastar e soltar, copiar e colar entre o windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support). | Mova arquivos entre as janelas abertas do SQL Operations Studio. |
| [Suporte de submódulo de Git](https://code.visualstudio.com/updates/v1_20#_git-submodules). | Execute operações de Git em repositórios de Git aninhados. |
| [Suporte de leitor de tela de terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support). | Terminal integrado agora tem **otimizado de leitor de tela** modo. |
| [Layout do editor centralizado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout). | Maximize seu código exibindo espaço na tela. |
| [Resultados da pesquisa horizontal (visualização)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | Você pode agora os resultados da pesquisa de exibição em um painel horizontal. |
| &nbsp; | &nbsp; |

Para obter mais detalhes, check-out a [notas de versão de fevereiro do Visual Studio código](https://code.visualstudio.com/updates/v1_21)e o [notas de versão de janeiro do Visual Studio código](https://code.visualstudio.com/updates/v1_20).

Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018"></a>Março de 2018

28 de março de 2018 &nbsp;  /  &nbsp; versão: 0.27.3 &nbsp;  /  &nbsp; visualização pública

O *Public Preview de março* continua abordar os principais problemas do GitHub e está focado em melhorar nossa história de extensibilidade. Especificamente, habilitar Extension Manager, melhorando o gerenciamento de painel e fornecendo SQL Agent e extensões de insights. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Aperfeiçoar o modelo de extensibilidade do painel para dar suporte a insights com guias e painéis de configuração. | Gerenciador de extensões permite que a aquisição simple das extensões.<br/><br/>Extensões de painel para sp\_whoisactive partir [whoisactive.com](http://www.whoisactive.com).<br/><br/>Para obter detalhes, consulte [estendem a funcionalidade do SQL Operations Studio](extensions.md). |
| Adicionar mais [APIs de extensibilidade para o Gerenciador de conexão e objeto](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) gerenciamento. | &nbsp; |
| Continuar a corrigir clientes importantes que afetam [problemas do GitHub](https://github.com/Microsoft/azuredatastudio/issues). | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>Fevereiro de 2018

15 de fevereiro de 2018 &nbsp;  /  &nbsp; versão: 0.26.7 &nbsp;  /  &nbsp; visualização pública

O *fevereiro Public Preview* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Apresentando a instalação da atualização automática, que fornece uma notificação quando uma nova versão está disponível para download. | &nbsp; |
| A caixa de diálogo de Conexão **banco de dados** campo agora é uma lista suspensa preenchida dinamicamente que contém uma lista de bancos de dados preenchida do servidor especificado. | &nbsp; |
| Introduza a API de extensibilidade de Conexão. | &nbsp; |
| Integração do VS 1.19 do Editor de código. | &nbsp; |
| Atualize o componente JustinPealing/html-planos de consulta para embarque várias melhorias de Visualizador de plano de consulta. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>Correção de problemas, fevereiro de 2018

- Corrigir [problema 6](https://github.com/Microsoft/azuredatastudio/issues/6): Mantenha a conexão e o banco de dados selecionado ao abrir novas guias de consulta.
- Corrigir [emitir 22](https://github.com/Microsoft/azuredatastudio/issues/22): 'Server Name' e 'Nome do banco de dados -' pode esses ser suspensos, em vez de caixas de texto?
- Corrigir [emitir 549](https://github.com/Microsoft/azuredatastudio/issues/549): A instalação silenciosa no modo silencioso/muito resulta no aplicativo que abre após a instalação.
- Corrigir [emitir 481](https://github.com/Microsoft/azuredatastudio/issues/481): Adicione a opção "Verificar atualizações".
- Colorização do Editor SQL e correções de preenchimento automático:
  - Corrigir [emitir 584](https://github.com/Microsoft/azuredatastudio/issues/584): Palavra-chave "Completo" não é realçado pelo IntelliSense.
  - Corrigir [emitir 345](https://github.com/Microsoft/azuredatastudio/issues/345): Colorir funções SQL dentro do editor.
  - Corrigir [emitir 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] mais recente "]" exibirá a cor verde.
  - Corrigir [emitir 225](https://github.com/Microsoft/azuredatastudio/issues/225): Incompatibilidade de cor da palavra-chave.
  - Corrigir [emitir 60](https://github.com/Microsoft/azuredatastudio/issues/60): Sql inválido cor realce de sintaxe ao usar a tabela temporária na cláusula from.

## <a name="january-2018"></a>Janeiro de 2018

17 de janeiro de 2018 &nbsp;  /  &nbsp; versão: 0.25.4 &nbsp;  /  &nbsp; visualização pública

O *Public Preview de janeiro* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Conexões do servidor salvas estão disponíveis na caixa de diálogo de Conexão. | &nbsp; |
| Habilite saída quente. Saída hot está desativado por padrão, para habilitar o consulte [configuração de saída Hot](settings.md#hot-exit). | &nbsp; |
| Coloração de guia com base no grupo de servidores. Coloração de guia está desativado por padrão, para habilitar o consulte [guia de configuração de cor](settings.md#tab-color). | &nbsp; |
| Alteração *nome do servidor* à *Server* na caixa de diálogo de Conexão. | &nbsp; |
| Correção de quebrado *executar consulta atual* comando. | &nbsp; |
| Correção de bug de script de separação de arrastar e soltar. | &nbsp; |
| Correção incorreto ícone fixado do Menu Iniciar. | &nbsp; |
| Corrigi a conta do Azure ausente, identidade visual de ícone. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>Dezembro de 2017

19 de dezembro de 2017 &nbsp;  /  &nbsp; versão: 0.24.1 &nbsp;  /  &nbsp; visualização pública

O *Public Preview de dezembro* inclui várias correções de bugs em todas as áreas de recurso, bem como os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Criar caixa de diálogo de regra de Firewall agora está disponível para ajudar a conectar-se ao banco de dados SQL e Azure SQL Data Warehouse. | &nbsp; |
| Adicionada a instalação Windows e Linux DEB e RPM pacotes de instalação. | &nbsp; |
| Gerencie o editor de layout visual do painel. | &nbsp; |
| *Como alterar script* e *Script como executar* comandos. | &nbsp; |
| *Executar consulta atual com o plano real* comando. | &nbsp; |
| Integre a plataforma de edição do VS Code 1.18.1. | &nbsp; |
| Habilite os arquivos de carregamento da extensão do VSIX. | &nbsp; |
| Dá suporte à sintaxe de iteração de lote de "N ir". | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>Novembro de 2017

15 de novembro de 2017 &nbsp;  /  &nbsp; versão: 0.23.6

- Versão inicial do [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:

- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
