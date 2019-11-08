---
title: Notas de versão
titleSuffix: Azure Data Studio
description: Notas sobre a versão do Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 16e2a7568bb88dbf36576cf5a6d64a1b268621fa
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532525"
---
# <a name="release-notes-for-azure-data-studio"></a>Notas sobre a versão relacionadas ao Azure Data Studio

**[Baixe e instale a versão mais recente!](download.md)**

## <a name="november-2019"></a>Novembro de 2019

4 de novembro de 2019 &nbsp; / &nbsp; versão: 1.13.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Novo suporte do SQL Server 2019 | &bull; &nbsp; Implantar o cluster de Big Data do SQL Server 2019 com o assistente de Implantação do BDC <br/>&bull; &nbsp; Gerenciar a integridade do cluster com o painel do controlador <br/>&bull; &nbsp; Gerenciar listas de controle de acesso do HDFS usando a Caixa de Diálogo de ACLs de Segurança <br/> &bull; &nbsp; Adicionar montagens usando a Caixa de Diálogo de Camada do HDFS <br/> &bull; &nbsp; Solução de problemas usando o Jupyter Book interno, guia do SQL Server 2019 <br/> &bull; &nbsp; Renomeação da extensão do SQL vNext para extensão Virtualização de dados <br/> &bull; &nbsp; Adição de suporte ao Teradata e ao Mongo no Assistente de Tabela Externa|
| Novos recursos de notebook | &bull; &nbsp; Comunicado sobre notebooks do PowerShell &bull; &nbsp; Comunicado sobre células de código recolhíveis <br/>&bull; &nbsp; Melhorias de desempenho em notebooks <br/> &bull; &nbsp; Veja a lista completa de melhorias [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22November+2019+Release%22+is%3Aclosed+label%3A%22Area+-+Notebooks%22) |
| Comunicado sobre o Jupyter Books  | O Jupyter Books é uma coleção de notebooks e arquivos Markdown organizados em um sumário. |
| Novo assistente de Implantação do SQL Server  | Agora inclui suporte para implantação: <br/> &bull; &nbsp; SQL Server 2019 no Windows <br/> &bull; &nbsp; SQL Server 2017 no Windows <br/> &bull; &nbsp; SQL Server 2019 no Docker <br/> &bull; &nbsp; SQL Server 2017 no Docker |
| Comunicado sobre o GA da extensão Comparação de Esquemas| &bull; &nbsp; Modo SQLCMD <br/> &bull; &nbsp; Suporte à localização <br/> &bull; &nbsp; Correções de acessibilidade <br/> &bull; &nbsp; Bugs de segurança  |
| Comunicado sobre o GA da extensão DACPAC do SQL Server| <br/> &bull; &nbsp; Suporte à localização <br/> &bull; &nbsp; Correções de acessibilidade <br/> &bull; &nbsp; Bugs de segurança |
| Comunicado sobre a extensão Visual Studio IntelliCode | O Visual Studio IntelliCode agora dá suporte ao SQL, que permite sugestões mais inteligentes de palavras-chave reservadas. |
| Bugs e problemas resolvidos | Para obter uma lista completa das correções, confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22November+2019+Release%22+is%3Aclosed). |
| &nbsp; | &nbsp; |

## <a name="october-2019-hotfix-2"></a>Outubro de 2019 (hotfix 2)

11 de outubro de 2019 &nbsp; / &nbsp; versão: 1.12.2

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Desabilitar o início automático do EH no modo de inspeção |  |
| &nbsp; | &nbsp; |

## <a name="october-2019-hotfix"></a>Outubro de 2019 (hotfix)

08 de outubro de 2019 &nbsp; / &nbsp; versão: 1.12.1

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Correção do problema de aspas e barras invertidas em blocos de anotações para escape correto. |  |
| &nbsp; | &nbsp; |

## <a name="october-2019"></a>Outubro de 2019

02 de outubro de 2019 &nbsp; / &nbsp; versão: 1.12.0

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Versão da extensão do histórico de consulta | A extensão do histórico do SQL salva todas as consultas passadas executadas em uma sessão de Azure Data Studio e as lista na ordem de execução. Os usuários podem ver e abrir a consulta, executá-la, excluí-la, pausar o histórico de consultas ou excluir todas as entradas desse histórico. |
| Novos Copiar/Colar Resultados | Adicionamos outras maneiras de copiar/colar resultados da grade de resultados. |
| Atualizar para extensão do PowerShell |  |
| Bugs e problemas resolvidos | Para obter uma lista completa das correções, confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/42?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos
- Notebooks
    - [7080](https://github.com/microsoft/azuredatastudio/issues/7080) Caso raros em que o notebook é serializado incorretamente

## <a name="september-2019"></a>Setembro de 2019

10 de setembro de 2019 versão &nbsp; / &nbsp;: 1.11.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Habilitar modo SQLCMD | Agora o editor de consultas dá suporte à alternância do modo SQLCMD para gravar e editar consultas como scripts SQLCMD |
| Extensão da Comunidade: Query Editor Boost | O Query Editor Boost é uma extensão de software livre com foco em aprimorar o editor de consultas do Azure Data Studio para usuários que estão frequentemente gravando consultas. &bull; &nbsp; Salvar a consulta atual como um snippet <br/>&bull; &nbsp; Alternar bancos de dados usando Ctrl+U <br/> &bull; &nbsp; Nova consulta com base em modelo <br/> &bull; &nbsp; Veja a lista completa de melhorias [aqui](https://github.com/dzsquared/query-editor-boost) |
| Melhorias ao Notebook | &bull; &nbsp; Melhorias de desempenho para dar suporte a arquivos de notebook maiores <br/> &bull; &nbsp; Veja a lista completa de melhorias [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22September+2019+Release%22+label%3A%22Area%3A+Notebooks%22+is%3Aclosed) |
| Mesclagem na versão de agosto do Visual Studio Code 1.38 | Os aprimoramentos mais recentes podem ser encontrados [aqui](https://code.visualstudio.com/updates/v1_38). |
| Bugs e problemas resolvidos | Para obter uma lista completa das correções, confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/39?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos
- Notebooks
    - [7080](https://github.com/microsoft/azuredatastudio/issues/7080) Caso raros em que o notebook é serializado incorretamente


## <a name="august-2019"></a>Agosto de 2019

15 de agosto de 2019 &nbsp; / &nbsp; versão: 1.10.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Lançamento da extensão SandDance 1.3.1 | &bull; &nbsp; Detecção de gráfico inteligente <br/>&bull; &nbsp; Visualizações 3D <br/> &bull; &nbsp; Filtragem de dados |
| Melhorias ao Notebook | &bull; &nbsp; Adicionar código ou célula de texto na linha <br/>&bull; &nbsp; Adicionada a possibilidade de clicar com o botão direito do mouse na grade de resultados SQL para salvar o resultado como CSV, JSON etc. <br/> &bull; &nbsp; Melhoria realizada no desempenho de carregamento de notebook, para um carregamento de JSON mais rápido <br/> &bull; &nbsp; Veja a lista completa de melhorias [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+label%3A%22Area%3A+Notebooks%22+milestone%3A%22August+2019+Release%22+is%3Aclosed) |
| Suporte ao SQL Server 2019 |  Esta versão inclui suporte para recursos adicionais de Cluster de Big Data do SQL Server 2019, incluindo: <br/> &bull; &nbsp; Redução do tempo necessário para carregar as informações da coluna e da tabela na página de mapeamento de objeto. <br/> &bull; &nbsp; Correção de um bug com o carregamento de credenciais de banco de dados com escopo na página de detalhes de conexão. <br/> &bull; &nbsp; Aumento no tamanho da amostra padrão usada para análise PROSE. | 
| A extensão Dacpac agora dá suporte a AAD | 
| Mesclagem na versão de julho do Visual Studio Code 1.37 | Os aprimoramentos mais recentes podem ser encontrados [aqui](https://code.visualstudio.com/updates/v1_37). |
| Bugs e problemas resolvidos | Para obter uma lista completa das correções, confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/39?closed=1). |
| &nbsp; | &nbsp; |

## <a name="july-2019"></a>Julho de 2019

11 de julho de 2019 &nbsp; / &nbsp; versão: 1.9.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Lançamento da extensão Plan Explorer do SentryOne | O valioso parceiro da Microsoft, SentryOne, disponibilizará a [extensão Plan Explorer do SentryOne para o Azure Data Studio](https://www.sentryone.com/products/sentryone-plan-explorer-extension-azure-data-studio). <br> Essa é uma extensão gratuita, que fornece diagramas de plano aprimorados para consultas executadas no Azure Data Studio, com algoritmos de layout otimizados e codificação de cores intuitiva para ajudar a identificar rapidamente os operadores mais pesados que afetam o desempenho da consulta. Para saber mais sobre a extensão, confira a postagem no blog do SentryOne [aqui](https://sqlperformance.com/2019/07/sentryone/plan-explorer-extension-azure-data-studio). |
| Novos recursos adicionados para a Comparação de Esquemas | &bull; &nbsp; Suporte a Arquivo de Comparação de Esquemas (.SCMP) <br/>&bull; &nbsp; Cancelamento de suporte à Comparação de Esquemas <br/>&bull; &nbsp; As alterações completas podem ser encontradas [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed+)|
| Melhorias ao Notebook | &bull; &nbsp; Suporte ao Plotly da Python <br/>&bull; &nbsp; Abrir Notebook usando o navegador <br/> &bull; &nbsp; Caixa de diálogo Gerenciamento de Pacotes do Python <br/> &bull; &nbsp; Aprimoramentos de desempenho e Markdown <br/> &bull; &nbsp; Atualização de atalhos do teclado <br/>  &bull; &nbsp; Correções de bugs e recursos secundários podem ser encontrados [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22+) |
| Suporte ao SQL Server 2019 |  Esta versão inclui suporte para recursos adicionais de Cluster de Big Data do SQL Server 2019, incluindo: <br/> &bull; &nbsp; Tabela de pontos de extremidade de serviço no painel de gerenciamento que lista todos os serviços principais do cluster. <br/> &bull; &nbsp; O Notebook de status do cluster mostra como você pode consultar e solucionar problemas de status do cluster em todos os serviços e pods.| 
| Pacotes de idiomas atualizados disponíveis| Agora há 10 pacotes de idiomas disponíveis no marketplace do Gerenciador de Extensões. Basta procurar o idioma específico usando o marketplace da extensão e instalar. Depois de instalar o idioma selecionado, o Azure Data Studio solicitará que você reinicie com o novo idioma. |
| Atualização do SQL Server Profiler | A extensão SQL Server Profiler foi atualizada para incluir novos recursos, incluindo: <br/> &bull; &nbsp; Filtragem por nome de banco de dados <br/> &bull; &nbsp; Suporte para copiar e colar <br/> &bull; &nbsp; Salvar/Carregar filtro <br/>Uma lista completa de melhorias na extensão SQL Server Profiler pode ser encontrada [aqui](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+SQL+Profiler%22+).  |
| Mesclagem na versão de maio do Visual Studio Code 1.35 | Os aprimoramentos mais recentes podem ser encontrados [aqui](https://code.visualstudio.com/updates/v1_35). |
| Bugs e problemas resolvidos | Nas versões anteriores do Azure Data Studio, se um banco de dados de usuário fosse selecionado ao se conectar usando a caixa de diálogo Conexão, a entrada resultante do Pesquisador de Objetos seria totalmente delimitada para esse banco de dados individual. Dessa versão em diante, esse comportamento está sendo alterado para que as propriedades de nível de servidor também sejam mostradas no pesquisador de objetos. <br/> Para obter uma lista completa das correções, confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/35?closed=1). |
| &nbsp; | &nbsp; |


## <a name="june-2019"></a>Junho de 2019

6 de junho, 2019 &nbsp; / &nbsp; versão: 1.8.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Lançamento da extensão CMS (Servidores de Gerenciamento Central) | Os servidores de gerenciamento central armazenam uma lista de instâncias do SQL Server que é organizada em um ou mais grupos de servidores de gerenciamento central. Os usuários podem se conectar aos seus próprios servidores de CMS existentes e gerenciá-los, como adicionar e remover servidores. Para saber mais, você pode ler [aqui](https://docs.microsoft.com/sql/relational-databases/administer-multiple-servers-using-central-management-servers) |
| Lançamento das extensões da Ferramenta de Administração de Banco de Dados para Windows | Essa extensão inicializa duas das experiências mais usadas no SQL Server Management Studio por meio do Azure Data Studio. Os usuários podem clicar com o botão direito do mouse em muitos objetos diferentes (como Bancos de Dados, Tabelas, Colunas, Exibições e muito mais) e selecionar Propriedades para exibir a caixa de diálogo de propriedades do SSMS para aquele objeto. Além disso, os usuários podem clicar com o botão direito do mouse em um banco de dados e selecionar Gerar Scripts para iniciar o famoso Assistente de Geração de Scripts do SSMS. 
| Melhorias na Comparação de Esquemas | &bull; &nbsp; Adição de opções Excluir/Incluir <br/>&bull; &nbsp; Geração de Script abre o script após ser gerado <br/>&bull; &nbsp; Barras de rolagem duplas removidas  <br/>&bull; &nbsp; Aprimoramentos de formatação e layout <br/>&bull; &nbsp; As alterações completas podem ser encontradas [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed)|
| Seção Mensagens movida para a própria guia | Quando os usuários executavam consultas SQL, os resultados e as mensagens ficavam em painéis empilhados. Agora eles estão em guias separadas em um painel como no SSMS. |
| Melhorias do Notebook do SQL | &bull; &nbsp; Agora os usuários podem decidir usar suas próprias instalações do Python 3 ou do Anaconda em notebooks <br/>&bull; &nbsp; Várias correções de estabilidade e de ajuste/término <br/> &bull; &nbsp; Veja a lista completa de melhorias [aqui](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22)|
| Mesclagem na versão de abril do Visual Studio Code 1.34 | Os aprimoramentos mais recentes podem ser encontrados [aqui](https://code.visualstudio.com/updates/v1_34) |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/32?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos
- Extensões da Ferramenta de Administração de Banco de Dados para Windows
    - Não é possível iniciar propriedades em nó de servidor desconectado
    - Não é possível iniciar propriedades de servidores do Azure
    - Nem todos os objetos têm caixas de diálogo de propriedades
    - As caixas de diálogo levam muito tempo para iniciar
    - Erros ao iniciar servidores com alguns tipos de conexões (como o AAD)
- Notebooks
    - [5838](https://github.com/microsoft/azuredatastudio/issues/5838) Permitir que usuários usem o Python do sistema para Notebooks
- Comparação de Esquemas
    - [5804](https://github.com/microsoft/azuredatastudio/issues/5804) Tarefas de Comparação de Esquemas mostram o menu de contexto padrão Cancelar que não faz nada

## <a name="may-2019"></a>Maio de 2019

8 de maio, 2019 &nbsp; / &nbsp; versão: 1.7.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Lançamento da extensão de Comparação de Esquemas | A Comparação de Esquemas é um recurso conhecido no SSDT (SQL Server Data Tools) e seu caso de uso principal é comparar e visualizar as diferenças entre bancos de dados e arquivos .dacpac, bem como para executar ações para torná-los iguais. |
| Mudança da exibição Tarefa para a Janela de Saída | Agora os usuários podem exibir o status de tarefas de execução prolongada, como Backup, Restauração e Comparação de Esquemas na exibição Tarefa na janela de Saída
| Página inicial adicionada | &bull; &nbsp; Links para ações comuns, como Nova Consulta, Novo Arquivo, Novo Notebook <br/>&bull; &nbsp; Links para documentação e GitHub |
| Melhorias do Notebook do SQL | &bull; &nbsp; Melhorias de renderização de Markdown, incluindo melhor suporte para anotações e tabelas <br/>&bull; &nbsp; Melhorias de usabilidade na barra de ferramentas <br/>&bull; &nbsp; Links de Markdown de notebooks confiáveis não exigem mais Cmd/Ctrl + clique e podem ser clicados diretamente <br/>&bull; &nbsp; Melhorias na limpeza de processos do Jupyter após o fechamento de notebooks e redução de erros ao iniciar vários notebooks simultaneamente <br/>&bull; &nbsp; Melhorias nas conexões de notebook do SQL para garantir que os erros não ocorram durante a execução de dois notebooks no mesmo banco de dados <br/>&bull; &nbsp; Melhorias na rolagem automática de notebooks para a célula em atualmente em execução ao clicar no botão Executar Células na barra de ferramentas <br/>&bull; &nbsp; Melhorias gerais de desempenho e estabilidade |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/microsoft/azuredatastudio/milestone/31?closed=1). |
| &nbsp; | &nbsp; |

## <a name="april-2019"></a>Abril de 2019

18 de abril, 2019 &nbsp; / &nbsp; versão: 1.6.0 

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Guia **Servidores** renomeada para **Conexões** | |
| Mudança do Azure Resource Explorer como um viewlet do Azure em Conexões | Agora os usuários podem exibir suas instâncias do SQL do Azure por meio de viewlet do Azure na exibição Conexões e expandir para exibir objetos em cada servidor ou banco de dados.|
| Melhorias do Notebook do SQL | &bull; &nbsp; Botão adicionado na barra de ferramentas para limpar a saída de todas as células <br/>&bull; &nbsp; Botão adicionado na barra de ferramentas para executar todas as células <br/>&bull; &nbsp; Correção no nome de conexão em vez do nome do servidor (se definido) na lista suspensa Anexar ao <br/>&bull; &nbsp; Correção da não renderização de imagens em Markdown ao usar caminhos de imagem relativos <br/>&bull; &nbsp; Funcionalidade aprimorada em grades de notebook por meio da adição de redimensionamento automático do tamanho de coluna ao clicar duas vezes e compatibilidade aprimorada com a roda do mouse <br/>&bull; &nbsp; Melhorias no tratamento de erro e na resiliência da instalação do Python ao instalar o Python por meio de notebooks <br/>&bull; &nbsp; Melhorias na funcionalidade "selecionar tudo" ao selecionar células de notebook <br/>&bull; &nbsp; Melhorias nas conexões de notebook para evitar o fechamento de um notebook e o impacto em uma conexão com o pesquisador de objetos <br/>&bull; &nbsp; Experiência de notebook aprimorada para exibir uma mensagem ao usuário quando o notebook estiver desconectado e precisar de uma conexão para executar células<br/>&bull; &nbsp; Suporte aprimorado para que notebooks não salvos sejam reidratados no ADS quando o ADS for iniciado novamente |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1). |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>Março de 2019 (hotfix)

22 de março, 2019 &nbsp; / &nbsp; versão: 1.5.2 &nbsp; / &nbsp; Versão de hotfix

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Correção de alguns problemas descobertos na versão 1.5.1. | Confira [Versão de hotfix de março, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/28).<br/> <br/>&bull; &nbsp; Correção do problema em que o usuário não conseguia fechar o notebook aberto na tarefa "Abrir Notebook" no painel <br/>&bull; &nbsp; Correção do problema em que o JSON Notebook tinha uma } adicional após salvar <br/>&bull; &nbsp; Correção do problema em que grades de notebook não respondiam às alterações do tema <br/>&bull; &nbsp; Corrigido o problema em que o caminho completo do notebook era mostrado no cabeçalho da guia. Agora, apenas o nome do arquivo é mostrado. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>Março de 2019

18 de março, 2019 &nbsp; / &nbsp; versão: 1.5.1

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Extensão [PostgreSQL adicionada ao Azure Data Studio](postgres-extension.md) | Recursos compatíveis: <br/>&bull; &nbsp; Caixa de diálogo Conexão <br/>&bull; &nbsp; Pesquisador de Objetos <br/>&bull; &nbsp; Editor de Consultas <br/>&bull; &nbsp; Gráficos <br/>&bull; &nbsp; Painéis <br/>&bull; &nbsp; Snippets <br/>&bull; &nbsp; Editar Dados <br/>&bull; &nbsp; Notebooks |
| Notebooks de SQL adicionados | Suporte ao kernel do SQL adicionado ao Visualizador de Notebook interno: <br/>&bull; &nbsp; Compatível com T-SQL <br/>&bull; &nbsp; Compatível com PGSQL |
| Extensão do PowerShell adicionada  | Traz a experiência da [extensão do PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) do VS Code.  |
| Extensão dacpac do SQL Server adicionada  | Remove o Assistente de aplicativo da camada de dados da extensão de importação do SQL Server colocando-o em uma nova extensão.  |
| Adicionada a extensão da Comunidade, a QueryPlan.show | Adiciona suporte à integração para visualizar planos de consulta  |
| Extensão do SQL Server 2019 Preview atualizada | &bull; &nbsp; Suporte ao Jupyter Notebook, especificamente kernels do Python3 e Spark, que foram movidos para a ferramenta principal do Azure Data Studio. <br/>&bull; &nbsp; Correções de bugs ao Assistente de Dados externos  |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conhecidos
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): Clicar em Executar na Célula antes que o kernel esteja pronto para o Spark resulta em um Erro fatal **Solução alternativa:** Aguarde até que os kernels sejam carregados para executar qualquer célula
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): o ADS iniciado no SSMS usando autenticação do SQL solicita senha ao usuário **Solução alternativa:** Use a autenticação do Windows por enquanto. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): Não é possível instalar o recurso de notebook do SQL <br/>
**Solução alternativa:** Siga as etapas de solução alternativa [aqui](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832). 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): O Azure Data Studio não pode ser aberto diretamente da pasta Downloads (Mac) <br />
**Solução alternativa:** Reinicie o computador após descompactar o aplicativo. Será investigada. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  Salvar como do Notebook causa perda de contexto de conexão <br />
**Solução alternativa:** Será corrigido na próxima versão. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): Extração de dacpac trava o SqlToolsService se uma versão inválida for usada <br/>
**Solução alternativa:** Reinicie o Azure Data Studio e use a versão correta.
- Os ícones Novo Notebook e Abrir Notebook ficam perdidos <br/>
**Solução alternativa:** O tipo de conexão herdada foi preterido. É recomendável conectar-se ao ponto de extremidade do SQL Server e você obterá todas as ações (Novo Notebook, Trabalho do Spark) conforme o esperado. 

## <a name="february-2019"></a>Fevereiro de 2019

13 de fevereiro de 2019 &nbsp;  /  &nbsp; versão: 1.4.5

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Extensão **Pacote de administração para SQL Server** adicionada. | Isso facilita instalar extensões relacionadas ao administrador do SQL Server. Isso inclui:<br/>&bull; &nbsp; [SQL Server Agent](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension)<br/>&bull; &nbsp; [SQL Server Import](sql-server-import-extension.md?view=sql-server-2017) |
| Adicionado suporte de filtragem de evento estendido na extensão Profiler. | &nbsp; |
| Adicionado o recurso Salvar como XML que pode salvar resultados de T-SQL como XML. | &nbsp; |
| Aprimoramentos adicionados ao Assistente de Aplicativo da Camada de Dados. | &bull; &nbsp; Botão Gerar script adicionado<br/>&bull; &nbsp; Adicionada uma exibição para fornecer avisos de possível perda de dados durante a implantação. |
| Atualizações à extensão do SQL Server 2019 Preview. | Confira [Extensão Virtualização de Dados](data-virtualization-extension.md?view=sql-server-ver15). |
| Streaming de resultados habilitado por padrão para consultas de execução prolongada. | &nbsp; |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1). |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>Janeiro de 2019 (hotfix)

16 de janeiro, 2019 &nbsp; / &nbsp; versão: 1.3.9 &nbsp; / &nbsp; Versão de hotfix

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Correção de alguns problemas descobertos na versão 1.3.8. | Confira [Versão de hotfix de janeiro, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).<br/><br/>Para obter informações detalhadas, veja:<br/>&bull; &nbsp; [Log de alterações, no GitHub](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).<br/>&bull; &nbsp; [Versões, no GitHub](https://github.com/Microsoft/azuredatastudio/releases). |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>Janeiro de 2019

9 de janeiro, 2019 &nbsp; / &nbsp; versão: 1.3.8

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Foi adicionado um novo instalador de usuário para o Windows. | Ao contrário do instalador do sistema existente, o novo instalador de usuário não requer privilégios de administrador. Isso também proporciona uma experiência de atualização mais fácil para não administradores. |
| Suporte adicionado para Autenticação do Azure Active Directory. | &nbsp; |
| Anunciando Idera SQL DM Performance Insights (Versão prévia). | &nbsp; |
| Suporte do Assistente de Aplicativo da Camada de Dados na extensão de Importação do SQL Server. | &nbsp; |
| Atualização à extensão do SQL Server 2019 Preview. | Confira [Extensão Virtualização de Dados](data-virtualization-extension.md?view=sql-server-ver15). |
| Aprimoramentos ao SQL Server Profiler. | &nbsp; |
| Streaming de resultados para consultas grandes (versão prévia). | &nbsp; |
| Extensões da comunidade: sp_executesql para sql e Novo Banco de Dados. | &nbsp; |
| Bugs e problemas resolvidos. | Confira [Bugs e problemas, no GitHub](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1). |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>Novembro de 2018

6 de novembro, 2018 &nbsp; / &nbsp; versão: 1.2.4

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Atualização à extensão do SQL Server 2019 Preview. | Confira [Extensão Virtualização de Dados](data-virtualization-extension.md?view=sql-server-ver15). |
| Apresentando a extensão Colar o Plano. | &nbsp; |
| Introdução à extensão de consultas High Color, incluindo o tema do editor do SSMS. | &nbsp; |
| Correções no SQL Server Agent, no Profiler e nas extensões de Importação. | &nbsp; |
| Correção no problema KeepAlive do soquete do .Net Core que causava quedas de conexões inativas no macOS. | &nbsp; |
| Atualização do serviço de Ferramentas do SQL para .Net Core 2.2 Preview 3 (para suporte eventual ao AAD). | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Correções de bugs, novembro de 2018

- Correção do [problema 2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexão perdida com o BD de SQL do Azure
- Correção do [problema 2914](https://github.com/Microsoft/azuredatastudio/issues/2914): Exceção "Argumento inválido" ao expandir o nó do banco de dados OE
- Correção do [problema 2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Exibição de mensagens de várias linhas corretamente nos resultados da consulta
- Correção do [problema 2906](https://github.com/Microsoft/azuredatastudio/pull/2906): Correção da Edição do nome do documento de dados quando o nome da tabela contém caracteres especiais
- Correção do [problema 2929](https://github.com/Microsoft/azuredatastudio/issues/2929): O log de mudanças da extensão interna diz para verificar as Notas sobre a versão do VSCode quanto às alterações
- Correção do [problema 2719](https://github.com/Microsoft/azuredatastudio/issues/2719): Ícones duplos/triplos do tema Alto Contraste
- Correção do [problema 3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Adição de uma interface de linha de comando para conexão com um SQL Server
- Correção do [problema 3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Adição de suporte ao tema do plano de consulta

## <a name="october-2018"></a>Outubro de 2018

29 de outubro, 2018 &nbsp; / &nbsp; versão: 1.1.4

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Apresentando o Azure Resource Explorer para navegar em Bancos de Dados SQL do Azure. | &nbsp; |
| Melhoria na robustez da conectividade do Pesquisador de Objetos e do Editor de Consultas. | &nbsp; |
| Melhorias nas extensões do SQL Agent. | &nbsp; |
| Atualização à extensão do SQL Server 2019 Preview. | Confira [Extensão Virtualização de Dados](data-virtualization-extension.md?view=sql-server-ver15). |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Correções de bugs, outubro de 2018

- Correção do [problema 2717](https://github.com/Microsoft/azuredatastudio/issues/2717): Formatação após clique no resultado da coluna XML
- Correção do [problema 2993](https://github.com/Microsoft/azuredatastudio/issues/2993): A largura das janelas Resultados fica incompleta
- Correção do [problema 2999](https://github.com/Microsoft/azuredatastudio/issues/2999): Não é possível carregar o arquivo System.Diagnostics.Tracing no Mac ao se conectar ao BD
- Correção do [problema 2851](https://github.com/Microsoft/azuredatastudio/issues/2851): O gráfico TimeSeries não é renderizado corretamente
- Correção do [problema 2996](https://github.com/Microsoft/azuredatastudio/issues/2996): Perda de tabela temporária devido à alteração de sessão repentina

Para obter informações detalhadas, confira o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md) e as [Versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-ga-release"></a>Setembro de 2018 (versão GA)

24 de setembro, 2018 &nbsp; / &nbsp; versão: 1.0 &nbsp; / &nbsp; versão GA

Versão de Disponibilidade Geral do Azure Data Studio (anteriormente SQL Operations Studio).

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Desempenho da Grade de Resultados da Consulta e melhorias de UX para grande número de conjuntos de resultados. | &nbsp; |
| Atualização do código-fonte do Visual Studio Code de 1.23 para 1.26.1 com o Layout de Grade e Editor de Configurações aprimorado (versão prévia). | &nbsp; |
| Aprimoramentos de acessibilidade para leitor de tela, navegação de teclado e alto contraste. | &nbsp; |
| Opção `Connection name` adicionada para fornecer um nome de exibição alternativo no viewlet de Servidores. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>Anúncio da extensão do SQL Server 2019 Preview

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Suporte para versão prévia do recurso do SQL Server 2019, incluindo suporte a [cluster de Big Data](../big-data-cluster/big-data-cluster-overview.md). | Conecte-se com o gateway do HDFS/Spark fornecido com a versão prévia do SQL Server 2019.<br/><br/>Navegue no HDFS, faça upload de arquivos, salve arquivos e inicie ações úteis, como Analisar no Notebook para arquivos CSV.<br/><br/>Envie trabalhos do Spark por meio do painel ou clique com o botão direito do mouse em uma conexão do HDFS/Spark no Pesquisador de Objetos. |
| Notebooks do Azure Data Studio. | Crie ou abra Notebooks usando um visualizador de Notebook integrado. Nesta versão, o Visualizador de Notebook é compatível com a conexão somente com kernels locais e com o cluster de Big Data do SQL Server 2019.<br/><br/>Use as bibliotecas PROSE Code Accelerator em seu Notebook para saber formatos de arquivo e tipos de dados que proporcionam uma rápida preparação de dados. |
| Azure Resource Explorer. | A exibição Azure Resource Explorer permite procurar pontos de extremidade relacionados a dados para suas contas do Azure e criar conexões com eles no Pesquisador de Objetos. Nesta versão, os servidores e os Bancos de Dados SQL do Azure são compatíveis. |
| Assistente de criação de tabela externa do PolyBase no SQL Server. | Crie uma tabela externa e suas estruturas de metadados de suporte com um assistente fácil de usar. Nesta versão, há suporte para os servidores remotos SQL Server e Oracle. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Correções de bugs, setembro de 2018

- Correção do [problema 2647](https://github.com/Microsoft/azuredatastudio/issues/143): Os gráficos regrediram muito.
- Correção do [problema 2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que retorna um JSON faz hiperlink de toda a coluna.

Para obter informações detalhadas, confira o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md) e as [Versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="august-2018"></a>Agosto de 2018

30 agosto, 2018 &nbsp; / &nbsp; versão: 0.32.8 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de agosto* se concentra em correções de bugs, estabilização do produto e preenchimento de lacunas em cenários existentes.

_A 0.32.8 contém correções para algumas regressões encontradas na 0.32.7 ([1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [2372](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Anúncio da extensão de Importação do SQL Server. | &nbsp; |
| Gerenciamento de sessão do SQL Server Profiler. | &nbsp; |
| Suporte ao modelo de sessão do SQL Server Profiler. | &nbsp; |
| Aprimoramentos no SQL Server Agent. | &nbsp; |
| Nova extensão da comunidade: Kit do primeiro respondente. | &nbsp; |
| Melhorias na Qualidade de Vida: Cadeias de conexão | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Correções de bugs, agosto de 2018

- Analise o SQL em uma janela do Editor de Consultas usando o comando `Parse Syntax`.
- Correção do [problema 143](https://github.com/Microsoft/azuredatastudio/issues/143): Clicar duas vezes não seleciona @ no nome da variável.
- Correção do [problema 387](https://github.com/Microsoft/azuredatastudio/issues/387): O ícone do BD da guia do SQL é vermelho.
- Correção do [problema 825](https://github.com/Microsoft/azuredatastudio/issues/825): Solicitação: Conectar automaticamente ao servidor atual após o Gerar Script como... 
- Correção do [problema 1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [entrada de área de trabalho] – valor redundante para o Nome e Comentário.
- Correção do [problema 1285](https://github.com/Microsoft/azuredatastudio/issues/1285): A atualização faz com que o ícone do aplicativo seja removido/substituído no Windows.
- Correção do [problema 1317](https://github.com/Microsoft/azuredatastudio/issues/1317): Correção do separador de decimal.
- Correção do [problema 1474](https://github.com/Microsoft/azuredatastudio/issues/1474): Cancelar alteração de conexão desconecta a conexão atual.
- Correção do [problema 1497](https://github.com/Microsoft/azuredatastudio/issues/1497): As opções de Exibir como Gráfico ficam cortadas na parte inferior.
- Correção do [problema 1524](https://github.com/Microsoft/azuredatastudio/issues/1524): Shell/painel: Os ícones principais do viewlet podem ser arrastados e podem causar falhas no aplicativo.
- Correção do [problema 1578](https://github.com/Microsoft/azuredatastudio/issues/1578): Não é possível expandir/recolher a pasta do navegador de arquivos remotos clicando no nome.
- Correção do [problema 1620](https://github.com/Microsoft/azuredatastudio/issues/1620): Sugestão de recurso: Obter cadeia de conexão para conexão existente.
- Correção do [problema 1624](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox não altera a cor quando desabilitada.
- Correção do [problema 1728](https://github.com/Microsoft/azuredatastudio/issues/1728): Salvar como JSON/EXCEL/CSV não funciona.
- Correção do [problema 1744](https://github.com/Microsoft/azuredatastudio/issues/1744): O painel resultados perde asa posições de rolagem ao alternar entre guias.
- Correção do [problema 1748](https://github.com/Microsoft/azuredatastudio/issues/1748): Mensagem de erro ao salvar arquivo do Excel uma segunda (e subsequente) vez.
- Correção do [problema 1782](https://github.com/Microsoft/azuredatastudio/issues/1782): Edição de dados: a célula não reverte para o valor original ao pressionar a tecla Esc.
- Correção do [problema 1836](https://github.com/Microsoft/azuredatastudio/issues/1836): arquivos .sql não associados ao SQL Operations Studio.
- Correção do [problema 1850](https://github.com/Microsoft/azuredatastudio/issues/1850): Ao digitar N'' ocorre o preenchimento automático de N'''.
- Correção do [problema 1985](https://github.com/Microsoft/azuredatastudio/issues/1985): A cópia da grade de resultados da consulta é deslocada em 1 coluna.
- Correção do [problema 1998](htpts://github.com/Microsoft/azuredatastudio/pull/1998): Adicionar a versão do VS Code à caixa de diálogo Sobre.
- Correção do [problema 2042](https://github.com/Microsoft/azuredatastudio/pull/2042): Agente: Botão habilitado para importar consultas de arquivos sql.
- Correção do [problema 2091](https://github.com/Microsoft/azuredatastudio/issues/2091): Não é possível usar o atalho CTRL + C para copiar no painel de resultados.
- Correção do [problema 2099](https://github.com/Microsoft/azuredatastudio/pull/2099): Adição de mais opções de saveAsCsv.
- Correção do [problema 2107](https://github.com/Microsoft/azuredatastudio/issues/2107): Ícone Atualizar documento para documentos do Painel e do Profiler.
- Correção do [problema 2129](https://github.com/Microsoft/azuredatastudio/pull/2129): Salvar a posição de rolagem dos dados de edição ao alternar guias.
- Correção do [problema 2152](https://github.com/Microsoft/azuredatastudio/issues/2152): Indicador de linha da grade de resultados com base em zero.

### <a name="known-issues-august-2018"></a>Problemas conhecidos, agosto de 2018

- [Problema 2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Salvar como Excel salva apenas a primeira linha dos dados
- [Problema 2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Não é possível conectar no Ubuntu 16.04 ao SQL em um contêiner

## <a name="july-2018"></a>Julho de 2018

19 de julho de 2018 &nbsp;  /  &nbsp; versão: 0.31.4 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de julho* se concentra nos seguintes itens:

- A versão inicial dos cenários de configuração do SQL Server Agent.
- Nos aprimoramentos de modelo de sessão e exibição do SQL Server Profiler.
- Correções de bugs continuadas para problemas relatados pelo cliente no GitHub.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Melhorias na [extensão SQL Server Agent para SQL Operations Studio](sql-server-agent-extension.md). | Adição de exibição de Alertas, Operadores e Proxies e ícones no painel esquerdo.<br/><br/>Adicionadas caixas de diálogo para Novo Trabalho, Nova Etapa do Trabalho, Novo Alerta e Novo Operador.<br/><br/>Adição de Excluir Trabalho, Excluir Alerta e Excluir Operador (ao clicar com o botão direito do mouse).<br/><br/>Adicionada a visualização Execuções Anteriores.<br/><br/>Adição de Filtros para cada nome de coluna. |
| Melhorias no [SQL Server Profiler para extensão do SQL Operations Studio](sql-server-profiler-extension.md). | Adição de cinco modelos padrão para exibir Eventos Estendidos.<br/><br/>Adição de nome de Servidor/Conexão de banco de dados.<br/><br/>Adição de suporte para instâncias do Banco de Dados SQL do Azure.<br/><br/>Adição de sugestão para sair do Profiler quando a guia é fechada e o Profiler ainda está em execução. |
| Lançamento da extensão Combinação de Scripts. | &nbsp; |
| Pontos de extensibilidade de Assistente e Caixa de diálogo adicionados para Autores de extensão. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Correções de bugs, julho de 2018

- Correção do [problema 728](https://github.com/Microsoft/azuredatastudio/issues/728): Sem resposta para Adicionar Conexão no macOS
- Correção do [problema 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): A exibição do texto da grade de resultados fica bagunçada por caracteres internacionais
- Correção do [problema 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): Caixa de diálogo de backup: A interface do usuário do navegador de arquivos está desfeita
- Correção do [problema 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): Número de linhas afetadas
- Correção do [problema 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): Não é possível conectar a nenhuma fonte de dados
- Correção do [problema 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError durante Conectando-se ao Servidor
- Correção do [problema 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): As caixas de diálogo de extensão pararam de funcionar
- Correção do [problema 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): BUG: Dados HTML em uma coluna são interpretados
- Correção do [problema 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): Extensibilidade: se você adicionar um provedor de conexão, a desinstalação nunca o removerá da lista
- Correção do [problema 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Extensões Sqlops: o queryeditor.connect() conecta-se ao banco de dados de destino, mas a interface do usuário não mostra que o editor está conectado
- Correção do [problema 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): O gráfico 10 maiores do BD não funciona em instâncias que diferenciam maiúsculas de minúsculas
- Correção do [problema 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): erro de digitação em sqlops.d.ts causando uma definição de tipo “any” implícita
- Correção do [problema 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Erro de ortografia
- Correção do [problema 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): A definição de iconPath no ButtonComponent após component() ser chamado não altera o ícone
- Correção do [problema 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): Melhor organização da tabela

## <a name="june-2018"></a>Junho de 2018

20 de junho, 2018 &nbsp; / &nbsp; versão: 0.30.6 &nbsp; / &nbsp; Versão Prévia Pública

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Liberação inicial da extensão **SQL Server Profiler para SQL Operations Studio _Versão Prévia_** . | &nbsp; |
| A nova extensão **SQL Data Warehouse** inclui widgets de painel personalizáveis avançados que identificam insights para seu data warehouse. | Isso libera os principais cenários de gerenciamento e ajuste do data warehouse para garantir que ele seja otimizado para um desempenho consistente. |
| Suporte à **Edição de dados por "Filtragem e Classificação"** . | &nbsp; |
| Melhorias na extensão **SQL Server Agent para SQL Operations Studio _Versão Prévia_** para as exibições Trabalhos e Histórico de Trabalhos. | &nbsp; |
| Aprimoramentos nas APIs de extensibilidade do **Assistente e Caixa de diálogo da Estrutura de Construtor de interface do usuário**. | &nbsp; |
| Atualização no código-fonte da plataforma do VS Code. | Integração das seguintes versões:<br/>&bull; &nbsp; [Março de 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [Abril de 2018 (1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>Correções de problemas do GitHub, junho de 2018

- Solicitação de recurso[(problema 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Faça com que a grade de resultados ajuste automaticamente a largura da coluna aos dados e lembre-se das alterações manuais se a mesma consulta for executada novamente.
- Correção do [problema 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Deveria mostrar o botão Adicionar mensagem e Adicionar conta quando a conta vinculada estivesse vazia.
- Correção do [problema 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): A guia da conta vinculada é desfeita quando a exibição é recolhida.
- Correção do [problema 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): O serviço SQL Tools falha ao abrir o arquivo .sql do disco.
- Correção do [problema 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Palavra-chave SQL "BETWEEN" ausente.
- Correção do [problema 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Palavra-chave "MATCH" causa falha no serviço SQL Tools.
- Correção do [problema 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): A opção de menu de contexto "Novo Profiler" no Pesquisador de Objetos não faz nada.
- Correção do [problema 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): O plano de consulta "Explicar" do Editor de Consultas está corrompido.

## <a name="may-2018"></a>Maio de 2018

7 de maio, 2018 &nbsp; / &nbsp; versão: 0.29.3 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de maio* se concentra na estabilização e correções de bugs.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Anunciando a extensão SQL Search da Redgate disponível no Gerenciador de Extensões. | &nbsp; |
| Localização da comunidade disponível para 10 idiomas. | Alemão, espanhol, francês, italiano, japonês, coreano, português, russo, chinês simplificado e chinês tradicional. |
| Alterações na coleção de telemetria. | &bull; &nbsp; Coleção de telemetria reduzida.<br/>&bull; &nbsp; Experiência de recusa aprimorada.<br/>&bull; &nbsp; Links no produto para a Política de Privacidade. |
| O Gerenciador de Extensões aprimorou a experiência do Marketplace. | Descubra mais facilmente as extensões da comunidade. |
| Extensão SQL Agent. | &bull; &nbsp; Trabalhos.<br/>&bull; &nbsp; Aprimoramento da exibição do histórico de trabalhos. |
| Atualizações para extensões de relatórios de servidor e whoisactive. | &nbsp; |
| Rolagem aprimorada em Gerenciar Propriedades do Painel. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>Correção de problemas do GitHub

- Correção do [problema 703](https://github.com/Microsoft/azuredatastudio/issues/703): A inserção de texto semelhante a HTML na edição de dados faz com que o valor seja exibido incorretamente até a atualização
- Correção [do problema 821](https://github.com/Microsoft/azuredatastudio/issues/821): dependência de pacote azuredatastudio.deb
- Correção do [problema 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palavra-chave "distinct" não realçada
- Correção do [problema 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Editar linha de reversão de dados não funciona
- Correção do [problema 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensão SQL Agent e a barra de status
- Correção do [problema 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): O SQL Agent não redimensiona após alterar o tamanho da janela

## <a name="april-2018"></a>Abril de 2018

25 de abril, 2018 &nbsp; / &nbsp; versão: 0.28.6 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de abril* contém correções de bugs e melhorias.

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Melhorias na extensão de SQL Agent Preview: | &nbsp; |
| &nbsp; &nbsp; &nbsp; Suporte aprimorado para arquivos. | &bull; &nbsp; Arquivos grandes.<br/>&bull; &nbsp; Arquivos protegidos, para salvar protegido pelo administrador.<br/>&bull; &nbsp; Armazenamento de \>arquivos de 256M no SQL Operations Studio. |
| &nbsp; &nbsp; &nbsp; Divisão do Terminal Integrado. | Trabalhe com vários terminais abertos simultaneamente. |
| &nbsp; &nbsp; &nbsp; Tempos de inicialização e instalação mais rápidos. | Instalação reduzida de arquivos em disco conta como volume. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>Correção de problemas do GitHub, abril de 2018

- Correção do [problema 37](https://github.com/Microsoft/azuredatastudio/issues/37): Quando o visualizador de gráfico gera um erro, ocorre um comportamento inesperado.
- Correção do [problema 462](https://github.com/Microsoft/azuredatastudio/issues/462): Solicitação de recurso: Opção para que os grupos de servidores sejam expandidos por padrão.
- Correção do [problema 606](https://github.com/Microsoft/azuredatastudio/issues/606): IntelliSense – sugestão inadequada para o comando "Update".
- Correção do [problema 967](https://github.com/Microsoft/azuredatastudio/issues/967): Espera-se o plano de consulta ao selecionar plano de execução de XML na grade de resultados.
- Correção do [problema 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): Adicionar colchetes para a chamada ms_foreachdb de flyfishingdba.
- Correção do [problema 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): Erro de handshake de SSL/TLS no pré-logon.
- Correção do [problema 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): Limpar a exibição de insights antes de mostrar o erro.
- Correção do [problema 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): As ações restaurar e nova consulta no explorer-widget estão corrompidas.
- Correção do [problema 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): A janela Saída do Painel é exibida com mensagem de erro para o Banco de Dados SQL do Azure.
- Correção do [problema 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): A caixa de diálogo de conexão mostra o erro de Servidor Necessário quando exibida inicialmente.
- Correção do [problema 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): Agora os grupos de servidores exigem clicar duas vezes para expandir.
- Correção do [problema 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): Tela de fundo da seleção de controle está semitransparente.
- Correção do [problema 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Corrigir todos os problemas de acessibilidade de alto contraste no SQL Operations Studio.
- Correção do [problema 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): A extensão falha ao atualizar "Baixar Manualmente". O link vai para a localização errada.
- Correção do [problema 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): Rolagem vertical não funciona na guia Página Inicial.
- Correção do [problema 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): As guias de extensão do SQL pararam de funcionar.

### <a name="visual-studio-code-121-platform"></a>Plataforma do Visual Studio Code 1.21

Um destaque da Versão Prévia Pública de abril é a atualização do código-fonte da plataforma do Visual Studio Code 1,21. Isso traz várias atualizações ao editor principal e ao workbench em relação ao ponto de sincronização anterior 1.19. Alguns exemplos incluem o seguinte:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| [Nova interface do usuário de notificações](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui). | Gerencie e examine facilmente as notificações do SQL Operations Studio. |
| [Divisão do Terminal Integrado](https://code.visualstudio.com/updates/v1_21#_split-terminals). | Trabalhe com vários terminais abertos ao mesmo tempo. |
| [Salve arquivos grandes e protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges). | Salve arquivos protegidos pelo administrador e \>256 M de arquivos no SQL Operations Studio. |
| [Suporte aprimorado a arquivos grandes](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements). | Otimizações de buffer de texto para arquivos grandes. |
| [Pesquisa de Configurações aprimorada](https://code.visualstudio.com/updates/v1_20#_settings-search). | Encontre facilmente a configuração correta com a pesquisa em idioma natural. |
| [Snippets globais](https://code.visualstudio.com/updates/v1_20#_global-snippets). | Crie snippets que podem ser usados em todos os tipos de arquivo. |
| [Multisseleção no Explorer](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer). | Execute ações em vários arquivos ao mesmo tempo. |
| [Erros e avisos no Explorer](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer). | Navegue rapidamente até os erros na sua base de código. |
| [Arrastar e soltar, copiar e colar entre janelas](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support). | Mova arquivos entre as janelas abertas do SQL Operations Studio. |
| [Suporte ao submódulo Git](https://code.visualstudio.com/updates/v1_20#_git-submodules). | Execute operações Git em repositórios Git aninhados. |
| [Suporte ao leitor de tela do terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support). | O Terminal Integrado agora tem o modo **Otimizado Para Leitor de Tela**. |
| [Layout do editor centralizado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout). | Maximize seu código exibindo o espaço da tela. |
| [Resultados da pesquisa na horizontal (versão prévia)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | Agora você pode exibir os resultados da pesquisa em um painel horizontal. |
| &nbsp; | &nbsp; |

Para obter detalhes adicionais, confira as [Notas sobre a versão de fevereiro do Visual Studio Code](https://code.visualstudio.com/updates/v1_21) e as [Notas sobre a versão de janeiro do Visual Studio Code](https://code.visualstudio.com/updates/v1_20).

Para obter mais informações, confira o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018"></a>Março de 2018

28 de março, 2018 &nbsp; / &nbsp; versão: 0.27.3 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de março* continua a abordar os principais problemas do GitHub e concentra-se em melhorar nosso histórico de extensibilidade. Especificamente habilitando o Gerenciador de Extensões, melhorando o gerenciamento de painel e fornecendo extensões do SQL Agent e de insights. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Aprimorar o modelo de extensibilidade do painel para dar suporte a insights em guias e painéis de configuração. | O Gerenciador de Extensões permite a aquisição simplificada de extensões.<br/><br/>Extensões do painel para o sp\_whoisactive da [whoisactive.com](http://www.whoisactive.com).<br/><br/>Para obter detalhes, confira [Estender a funcionalidade do SQL Operations Studio](extensions.md). |
| Adicione outras [APIs de extensibilidade para o gerenciamento de conexão e do pesquisador de objetos](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API). | &nbsp; |
| Continuar a corrigir [problemas importantes do GitHub](https://github.com/Microsoft/azuredatastudio/issues) que afetam o cliente. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>Fevereiro de 2018

15 de fevereiro de 2018 &nbsp; / &nbsp; versão: 0.26.7 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de fevereiro* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Introdução à instalação de atualização automática, que fornece uma notificação quando uma nova versão está disponível para baixar. | &nbsp; |
| O campo Caixa de Diálogo de Conexão do **Banco de dados** agora é uma lista suspensa preenchida dinamicamente que conterá uma lista de bancos de dados populados por meio do servidor especificado. | &nbsp; |
| Apresentar a API de extensibilidade de conexão. | &nbsp; |
| Integração do VS Code Editor 1.19. | &nbsp; |
| Atualizar o componente JustinPealing/html-query-plan para obter vários aprimoramentos do visualizador do Plano de Consulta. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>Problemas corrigidos, fevereiro de 2018

- Correção do [problema 6](https://github.com/Microsoft/azuredatastudio/issues/6): Manter a conexão e o banco de dados selecionado ao abrir novas guias de consulta.
- Correção do [problema 22](https://github.com/Microsoft/azuredatastudio/issues/22): "Nome do Servidor" e "Nome do Banco de Dados"– podem ser listas suspensas em vez de caixas de texto?
- Correção do [problema 549](https://github.com/Microsoft/azuredatastudio/issues/549): A Instalação Silenciosa/Muito Silenciosa resulta na abertura do aplicativo após a instalação.
- Correção do [problema 481](https://github.com/Microsoft/azuredatastudio/issues/481): Adicionar a opção "Verificar Atualizações".
- Colorização do Editor SQL e correções de preenchimento automático:
  - Correção do [problema 584](https://github.com/Microsoft/azuredatastudio/issues/584): Palavra-chave "FULL" não realçada pelo IntelliSense.
  - Correção do [problema 345](https://github.com/Microsoft/azuredatastudio/issues/345): Colorir funções SQL dentro do editor.
  - Correção do [problema 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] latest "]" exibirá a cor verde.
  - Correção do [problema 225](https://github.com/Microsoft/azuredatastudio/issues/225): Incompatibilidade de cor de palavra-chave.
  - Correção do [problema 60](https://github.com/Microsoft/azuredatastudio/issues/60): Realce de cor de sintaxe SQL inválido ao usar tabela temporária na cláusula FROM.

## <a name="january-2018"></a>Janeiro de 2018

17 de janeiro, 2018 &nbsp; / &nbsp; versão: 0.25.4 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de janeiro* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Conexões de servidor salvas estão disponíveis na Caixa de Diálogo de Conexão. | &nbsp; |
| Habilitar Hot Exit. Hot Exit está desativado por padrão; para habilitar, confira a [Configuração do Hot Exit](settings.md#hot-exit). | &nbsp; |
| Cor da guia com base no Grupo de Servidores. A coloração de guias está desativada por padrão, para habilitar, confira [Configuração de cor da guia](settings.md#tab-color). | &nbsp; |
| Alterar *Nome do servidor* para *Servidor* na Caixa de Diálogo de Conexão. | &nbsp; |
| Corrigir o comando *Executar Consulta Atual* corrompido. | &nbsp; |
| Corrigir o bug de interrupção de script do tipo "arrastar e soltar". | &nbsp; |
| Corrigir o ícone do Menu Iniciar fixado incorretamente. | &nbsp; |
| Corrigir o ícone de identidade visual ausente da Conta do Azure. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>Dezembro de 2017

19 de dezembro, 2017 &nbsp; / &nbsp; versão: 0.24.1 &nbsp; / &nbsp; Versão Prévia Pública

A *Versão Prévia Pública de dezembro* inclui várias correções de bugs em todas as áreas de recursos, bem como os seguintes aprimoramentos:

&nbsp;

| Alterar | Detalhes |
| :----- | :------ |
| Caixa de diálogo Criar Regra de Firewall agora está disponível para auxiliar na conexão com o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure. | &nbsp; |
| Adicionados os pacotes de Instalação do Windows e os pacotes de instalação DEB e RPM do Linux. | &nbsp; |
| Gerenciar o editor de layout visual do Painel. | &nbsp; |
| Comandos *Script As Alter* e *Script As Execute*. | &nbsp; |
| Comando *Run Current Query with Actual Plan*. | &nbsp; |
| Integração da plataforma do editor do VS Code 1.18.1. | &nbsp; |
| Habilitar o sideload de arquivos de extensão VSIX. | &nbsp; |
| Suporte à sintaxe de iteração em lote "GO N". | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>Novembro de 2017

15 de novembro, 2017 &nbsp; / &nbsp; versão: 0.23.6

- Versão inicial do [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="next-steps"></a>Next Steps

Confira um dos seguintes inícios rápidos para começar:

- [Conectar-se ao SQL Server e consultá-lo](quickstart-sql-server.md)
- [Conectar-se a um Banco de Dados SQL do Azure e consultá-lo](quickstart-sql-database.md)
- [Conectar-se ao Data Warehouse do Azure e consultá-lo](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
