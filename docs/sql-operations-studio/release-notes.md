---
title: Notas de versão do Microsoft SQL Operations Studio (versão prévia) | Microsoft Docs
description: Notas de versão do Microsoft SQL Operations Studio (versão prévia)
ms.custom: tools|sos
ms.date: 07/19/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5c331fc8b9e95940e0aaca29efbada78083340f
ms.sourcegitcommit: d80aaa52562d828f9bfb932662ad779432301860
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39188952"
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de versão do SQL Operations Studio (versão prévia)

**[Baixe a visualização pública de julho](download.md)**

## <a name="july-2018-july-public-preview"></a>Julho de 2018 (julho a visualização pública)

Data de lançamento: 19 de julho de 2018  
versão: 0.31.4

O *julho de visualização pública* se concentra na versão inicial do contínuas correções de bugs, aprimoramentos de modelo de sessão e modo de exibição do SQL Server Profiler e cenários de configuração do SQL Server Agent para GitHub problemas relatados pelo cliente. Esta versão contém os seguintes destaques:  

- [SQL Server Agent para a extensão do SQL Operations Studio](sql-server-agent-extension.md) melhorias
 - Exibição adicionada dos alertas, operadores e Proxies e ícones no painel esquerdo
 - Caixas de diálogo adicionadas para o novo trabalho, nova etapa de trabalho, novo alerta e operador New
 - Adicionado Delete Job, excluir alerta e operador excluir (botão direito do mouse)
 - Visualização de execuções anteriores adicionada
 - Filtros adicionados para cada nome de coluna
- [SQL Server Profiler para a extensão do SQL Operations Studio](sql-server-profiler-extension.md) melhorias
 - Teclas de atalho adicionadas rapidamente inicializar e iniciar/parar o Profiler
 - Adicionado 5 modelos padrão para exibir eventos estendidos
 - Nome de conexão de servidor/banco de dados adicionado
 - Adicionado suporte para instâncias de banco de dados SQL
 - Sugestão adicionado para sair do Profiler quando o guia é fechada quando o Profiler ainda está em execução
- Versão da extensão de Scripts de combinar
- Pontos de extensibilidade de caixa de diálogo e Assistente adicionados para autores de extensão
- Corrigi problemas do GitHub:
 - Corrigir [emitir 728](https://github.com/Microsoft/sqlopsstudio/issues/728): não há resposta para Adicionar Conexão no macOS
 - Corrigir [emitir 1612](https://github.com/Microsoft/sqlopsstudio/issues/1612): exibição de texto da grade de resultados é bagunçada por caracteres internacionais
 - Corrigir [emitir 1693](https://github.com/Microsoft/sqlopsstudio/issues/1693): caixa de diálogo de Backup: o navegador de arquivos da interface do usuário é interrompido
 - Corrigir [emitir 1713](https://github.com/Microsoft/sqlopsstudio/issues/1713): número de linhas afetadas
 - Corrigir [emitir 1718](https://github.com/Microsoft/sqlopsstudio/issues/1718): não é possível conectar a qualquer fonte de dados
 - Corrigir [emitir 1719](https://github.com/Microsoft/sqlopsstudio/issues/1719): TypeError ao se conectar ao servidor
 - Corrigir [emitir 1724](https://github.com/Microsoft/sqlopsstudio/issues/1724): caixas de diálogo de extensão tem parado de funcionar
 - Corrigir [emitir 1749](https://github.com/Microsoft/sqlopsstudio/issues/1749): BUG: interpretados dados HTML em uma coluna
 - Corrigir [emitir 1789](https://github.com/Microsoft/sqlopsstudio/issues/1789): extensibilidade: se você adicionar um provedor de conexão desinstalação nunca irá removê-lo da lista
 - Corrigir [emitir 1791](https://github.com/Microsoft/sqlopsstudio/issues/1791): extensões Sqlops: queryeditor.connect() se conecta ao banco de dados de destino, mas a interface do usuário não mostra o editor está conectado
 - Corrigir [emitir 1799](https://github.com/Microsoft/sqlopsstudio/issues/1799): gráfico de tamanho de BD Top 10 não funciona em instâncias diferencia maiusculas de minúsculas
 - Corrigir [emitir 1814](https://github.com/Microsoft/sqlopsstudio/issues/1814): definição de tipo de erro de digitação sqlops.d.ts causando 'any' implícito
 - Corrigir [emitir 1817](https://github.com/Microsoft/sqlopsstudio/issues/1817): erro de Ortografia
 - Corrigir [emitir 1830](https://github.com/Microsoft/sqlopsstudio/issues/1830): definindo iconPath no ButtonComponent depois component() é chamado não altera o ícone
 - Corrigir [emitir 1843](https://github.com/Microsoft/sqlopsstudio/issues/1843): organização da tabela melhor


Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/sqlopsstudio/releases).



## <a name="june-2018-june-public-preview"></a>Junho de 2018 (visualização pública de junho)

Data de lançamento: 20 de junho de 2018  
versão: 0.30.6

O *junho Public Preview* contém os seguintes destaques:  

- **SQL Server Profiler para SQL Operations Studio *versão prévia***  versão inicial da extensão.
- O novo **SQL Data Warehouse** extensão inclui widgets de painel personalizável avançado identificando insights ao seu data warehouse. Isso desbloqueia os principais cenários de gerenciamento e ajuste seu data warehouse para garantir que ele é otimizado para desempenho consistente.
- **Editar dados "Filtragem e classificação"** dão suporte.
- **SQL Server Agent para o SQL Operations Studio *versão prévia***  aprimoramentos de extensão para trabalhos e o histórico de trabalho de modos de exibição.
- Aprimorado **Assistente de & estrutura do construtor de interface do usuário de caixa de diálogo** APIs de extensibilidade.
- Atualizar a plataforma de código do VS fonte código integrando [(1.22) de março de 2018](https://code.visualstudio.com/updates/v1_22) e [abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) libera.
- Corrigi problemas do GitHub:
  - Solicitação de recurso ([emitir 1204](https://github.com/Microsoft/sqlopsstudio/issues/1204)):, fazer os resultados da largura da coluna de ajuste automático de grade de dados, e/ou se lembrar de alterações manuais se a mesma consulta for executada novamente.
  - Corrigir [emitir 1398](https://github.com/Microsoft/sqlopsstudio/issues/1398): Mostrar deve adicionar de mensagens e adicionar botão de conta da conta quando a conta vinculada está vazia.
  - Corrigir [emitir 1399](https://github.com/Microsoft/sqlopsstudio/issues/1399): guia Conta vinculada é interrompido quando o modo de exibição é recolhido.
  - Corrigir [emitir 1374](https://github.com/Microsoft/sqlopsstudio/issues/1374): serviço de ferramentas do SQL Falha ao abrir o arquivo. SQL no disco.
  - Corrigir [emitir 1372](https://github.com/Microsoft/sqlopsstudio/issues/1372): "BETWEEN" de palavra-chave SQL ausente.
  - Corrigir [emitir 1395](https://github.com/Microsoft/sqlopsstudio/issues/1395): palavra-chave de 'MATCH' falhas de serviço de ferramentas do SQL.
  - Corrigir [emitir 1496](https://github.com/Microsoft/sqlopsstudio/issues/1496): opção de menu de contexto "Nova Profiler" no Pesquisador de objetos não faz nada.
  - Corrigir [emitir 1495](https://github.com/Microsoft/sqlopsstudio/issues/1495): plano de consulta de "Explain" de editor de consulta é interrompido.


## <a name="may-2018-may-public-preview"></a>Maio de 2018 (maio de visualização pública)

Data de lançamento: 7 de maio de 2018  
versão: 0.29.3

O *visualização pública podem* se concentra na estabilização e correções de bugs. Esse build contém os seguintes destaques:  

- Anunciando a extensão do Redgate SQL Search disponível no Gerenciador de extensões.
- Localização da comunidade disponível para 10 idiomas: alemão, espanhol, francês, italiano, japonês, coreano, português, russo, chinês simplificado e chinês tradicional.
- Coleta de telemetria reduzida, experiência aprimorada de recusa e links no produto para declaração de privacidade.
- Gerenciador de extensões tem Marketplace aprimorado de experiência para descobrir facilmente extensões de comunidade.
- Trabalhos de extensão do SQL Agent e histórico de trabalho Exibir melhoria.
- Atualizações para whoisactive e extensões do relatórios do servidor.
- Melhore a rolagem de gerenciar propriedades do painel.
- Corrigi problemas do GitHub:
   - Corrigir [execute 703](https://github.com/Microsoft/sqlopsstudio/issues/703): inserindo o texto do tipo HTML na edição de dados faz com que o valor a ser exibido incorretamente após atualização
   - Corrigir [emitir 821](https://github.com/Microsoft/sqlopsstudio/issues/821): dependência de pacote sqlopsstudio.deb
   - Corrigir [emitir 1260](https://github.com/Microsoft/sqlopsstudio/issues/1260): palavra-chave 'distinct' não realçado
   - Corrigir [emitir 1332](https://github.com/Microsoft/sqlopsstudio/issues/1332): dados de edição reverter linha não funciona
   - Corrigir [emitir 1215](https://github.com/Microsoft/sqlopsstudio/issues/1215): extensão do agente SQL e a barra de status
   - Corrigir [emitir 1316](https://github.com/Microsoft/sqlopsstudio/issues/1316): SQL Agent não redimensionar após alterar o tamanho de windows




## <a name="april-2018-april-public-preview"></a>Abril de 2018 (visualização pública de abril)

Data de lançamento: 25 de abril de 2018  
versão: 0.28.6

O *abril de visualização pública* contém correções de bugs e melhorias. 

- Melhorias para a extensão de visualização do agente SQL.
- Arquivo protegido e grande suporte aprimorado para salvar administrador protegida e > 256m arquivos dentro do SQL Operations Studio.
- Terminal integrado divisão para trabalhar com vários terminais abertos ao mesmo tempo.
- Imprimir pés de contagem de arquivo em disco reduzido de instalação para instalações mais rápidas e tempos de inicialização.
- Continue a corrigir problemas do GitHub:
   - Corrigir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): quando o Visualizador gráfico gera um erro, ocorre um comportamento inesperado.
   - Corrigir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitação de recurso: opção de grupos de servidores ser expandido por padrão.
   - Corrigir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - sugestão incorreta para o comando 'Atualizar'.
   - Corrigir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): espera que o plano de consulta quando seleciona o plano de execução XML na grade de resultado.
   - Corrigir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): Adicionar colchetes para chamada ms_foreachdb da flyfishingdba.
   - Corrigir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): erro de handshake de PRÉ-LOGON SSL/TLS.
   - Corrigir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): insights claras exibir antes de mostrar o erro.
   - Corrigir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): novas ações de consulta no Gerenciador de widget e restauração são interrompidas.
   - Corrigir [emitir 1068](https://github.com/Microsoft/sqlopsstudio/issues/1068): painel Saída windows pops-up com a mensagem de erro para o banco de dados SQL.
   - Corrigir [emitir 1069](https://github.com/Microsoft/sqlopsstudio/issues/1069): caixa de diálogo de Conexão mostra erro de servidor necessárias ao exibido inicialmente.
   - Corrigir [emitir 1070](https://github.com/Microsoft/sqlopsstudio/issues/1070): grupos de servidores agora precisam de um clique duplo para expandir.
   - Corrigir [emitir 1072](https://github.com/Microsoft/sqlopsstudio/issues/1072): plano de fundo do controle de seleção é semitransparente.
   - Corrigir [emitir 1115](https://github.com/Microsoft/sqlopsstudio/issues/1115): corrigir problemas de acessibilidade de todos os alto contraste em SQL Operations Studio.
   - Corrigir [emitir 1101](https://github.com/Microsoft/sqlopsstudio/issues/1101): falha de extensão para atualização "baixar manualmente" link vai para o local errado.
   - Corrigir [emitir 1103](https://github.com/Microsoft/sqlopsstudio/issues/1103): rolagem V não está funcionando na guia página inicial.
   - Corrigir [emitir 1104](https://github.com/Microsoft/sqlopsstudio/issues/1104): guias de extensão SQL parou de funcionar.


Um realce significativo para a visualização de abril pública é a atualização de código de origem de plataforma 1.21 de código do Visual Studio. Isso traz várias atualizações para o editor de núcleo e Bancada de trabalho do ponto de 1.19 sincronização anterior. Alguns exemplos incluem o seguinte:

- [Nova interface do usuário de notificações](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) - facilmente gerenciar e as notificações do SQL Operations Studio.
- [Integrado a divisão de Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals) -trabalhar com vários terminais abertos ao mesmo tempo.
- [Salvar arquivos grandes e protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) - salve Admin protegidos e > 256m arquivos dentro do SQL Operations Studio.
- [Melhor suporte de arquivo grande](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -otimizações de buffer de texto para arquivos grandes.
- [Uma pesquisa aperfeiçoada configurações](https://code.visualstudio.com/updates/v1_20#_settings-search) – facilmente localizar a configuração correta com a pesquisa em idioma natural.
- [Trechos de código globais](https://code.visualstudio.com/updates/v1_20#_global-snippets) -criar trechos de código que você pode usar em todos os tipos de arquivo.
- [Seleção múltipla do Explorer](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -executar ações em vários arquivos ao mesmo tempo.
- [Erros e avisos no Explorer](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) - rapidamente navegar para erros em sua base de código.
- [Arrastar e soltar, copiar e colar entre o windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -mover arquivos entre as janelas abertas do SQL Operations Studio.
- [Suporte de submódulo de Git](https://code.visualstudio.com/updates/v1_20#_git-submodules) -Git executar operações em repositórios de Git aninhados.
- [Suporte de leitor de tela de terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -Terminal integrado agora tem o modo "Otimizado de leitor de tela".
- [Layout do editor centralizado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -maximizar seu código exibindo espaço na tela.
- [Resultados da pesquisa horizontal (visualização)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -você pode agora exibir resultados da pesquisa em um painel horizontal.

Para obter mais detalhes, check-out a [notas de versão de fevereiro do Visual Studio código](https://code.visualstudio.com/updates/v1_21)e o [notas de versão de janeiro do Visual Studio código](https://code.visualstudio.com/updates/v1_20).

Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>(Visualização pública de março) de março de 2018

Data de lançamento: 28 de março de 2018  
versão: 0.27.3

O *Public Preview de março* continua abordar os principais problemas do GitHub e está focado em melhorar nossa história de extensibilidade. Especificamente, habilitar Extension Manager, melhorando o gerenciamento de painel e fornecendo SQL Agent e extensões de insights. Esta versão inclui os seguintes aprimoramentos:

- Aperfeiçoar o modelo de extensibilidade do painel para dar suporte a insights com guias e painéis de configuração.
   - Gerenciador de extensões permite que a aquisição simple das extensões.
   - Extensões de painel para sp_whoisactive partir [whoisactive.com](http://www.whoisactive.com).
   - Para obter detalhes, consulte [estendem a funcionalidade do SQL Operations Studio](extensions.md).
- Adicionar mais [APIs de extensibilidade para o Gerenciador de conexão e objeto](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) gerenciamento.
- Continuar a corrigir clientes importantes que afetam [problemas do GitHub](https://github.com/Microsoft/sqlopsstudio/issues).


## <a name="february-2018-february-public-preview"></a>Fevereiro de 2018 (visualização pública de fevereiro)

Data de lançamento: 15 de fevereiro de 2018  
versão: 0.26.7

O *fevereiro Public Preview* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

- Apresentando a instalação da atualização automática, que a fornece uma notificação quando uma nova versão está disponível para download 
- O campo 'Banco de dados' de caixa de diálogo de Conexão agora é uma lista suspensa preenchida dinamicamente que contém uma lista de bancos de dados preenchida do servidor especificado.
- Corrigir [problema 6](https://github.com/Microsoft/sqlopsstudio/issues/6): manter a conexão e o banco de dados selecionado ao abrir novas guias de consulta.
- Corrigir [emitir 22](https://github.com/Microsoft/sqlopsstudio/issues/22): 'Server Name' e 'Nome do banco de dados' - estes podem ser suspensos, em vez de caixas de texto?
- Corrigir [emitir 549](https://github.com/Microsoft/sqlopsstudio/issues/549): a instalação silenciosa no modo silencioso/muito resulta em um aplicativo abrindo após a instalação.
- Corrigir [emitir 481](https://github.com/Microsoft/sqlopsstudio/issues/481): adicione a opção "Verificar atualizações".
- Colorização do Editor SQL e correções de preenchimento automático:
   - Corrigir [emitir 584](https://github.com/Microsoft/sqlopsstudio/issues/584): palavra-chave "FULL" não realçado pelo IntelliSense.
   - Corrigir [emitir 345](https://github.com/Microsoft/sqlopsstudio/issues/345): funções de SQL colorir dentro do editor.
   - Corrigir [emitir 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] mais recente "]" exibirá a cor verde.
   - Corrigir [emitir 225](https://github.com/Microsoft/sqlopsstudio/issues/225): incompatibilidade de cor da palavra-chave.
   - Corrigir [emitir 60](https://github.com/Microsoft/sqlopsstudio/issues/60): sql inválido cor realce de sintaxe ao usar a tabela temporária na cláusula from.
- Introduza a API de extensibilidade de Conexão.
- Integração do VS 1.19 do Editor de código.
- Atualize o componente JustinPealing/html-planos de consulta para embarque várias melhorias de Visualizador de plano de consulta.


## <a name="january-2018-january-public-preview"></a>Janeiro de 2018 (janeiro a visualização pública)

Data de lançamento: 17 de janeiro de 2018  
versão: 0.25.4

O *Public Preview de janeiro* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

- Conexões do servidor salvas estão disponíveis na caixa de diálogo de Conexão.
- Habilite saída quente. Saída hot está desativado por padrão, para habilitar o consulte [configuração de saída Hot](settings.md#hot-exit).
- Coloração de guia com base no grupo de servidores. Coloração de guia está desativado por padrão, para habilitar o consulte [guia de configuração de cor](settings.md#tab-color).
- Alteração *nome do servidor* à *Server* na caixa de diálogo de Conexão.
- Correção de quebrado *executar consulta atual* comando.
- Correção de bug de script de separação de arrastar e soltar.
- Correção incorreto ícone fixado do Menu Iniciar.
- Corrigi a conta do Azure ausente, identidade visual de ícone.


## <a name="december-2017-december-public-preview"></a>Dezembro de 2017 (visualização pública de dezembro)

Data de lançamento: 19 de dezembro de 2017  
versão: 0.24.1

O *Public Preview de dezembro* inclui várias correções de bugs em todas as áreas de recurso, bem como os seguintes aprimoramentos:

- Criar caixa de diálogo de regra de Firewall agora está disponível para ajudar a conectar-se ao banco de dados SQL e Azure SQL Data Warehouse.
- Adicionada a instalação Windows e Linux DEB e RPM pacotes de instalação.
- Gerencie o editor de layout visual do painel.
- *Como alterar script* e *Script como executar* comandos.
- *Executar consulta atual com o plano real* comando.
- Integre a plataforma de edição do VS Code 1.18.1.
- Habilite os arquivos de carregamento da extensão do VSIX.
- Dá suporte à sintaxe de iteração de lote de "N ir".


## <a name="november-2017"></a>Novembro de 2017

Data de lançamento: 15 de novembro de 2017  
versão: 0.23.6

- Versão inicial do [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:
- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
