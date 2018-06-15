---
title: Notas de versão do Microsoft SQL operações Studio (visualização) | Microsoft Docs
description: Notas de versão do Microsoft SQL operações Studio (visualização)
ms.custom: tools|sos
ms.date: 05/08/2018
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
ms.openlocfilehash: 3f461b78c3d76f7e6b848b83d8a2333dffe5de3c
ms.sourcegitcommit: a9da0abd3e17fbcd6339980d7331d0418cdada53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34473820"
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de versão do SQL Studio de operações (visualização)

**[Baixe a visualização pública pode](download.md)**


## <a name="may-2018-may-public-preview"></a>De 2018 de maio (maio de visualização pública)

Data de lançamento: 7 de maio de 2018  
versão: 0.29.3

O *visualização pública pode* se concentra na estabilização e correções de bugs. Esta compilação contém destaca a seguinte:  

- Anunciando a extensão de pesquisa do SQL Redgate disponível no Gerenciador de extensões.
- Localização de comunidade disponível para 10 idiomas: alemão, espanhol, francês, italiano, japonês, coreano, português, russo, chinês simplificado e chinês tradicional.
- Coleção de telemetria reduzido, experiência aprimorada de recusa e links de dentro do produto a declaração de privacidade.
- Gerenciador de extensões tiver Marketplace melhor experiência para descobrir facilmente as extensões de comunidade.
- Trabalhos de extensão do SQL Agent e histórico do trabalho de exibição aperfeiçoamento.
- Atualizações para whoisactive e extensões de servidor de relatórios.
- Melhore a rolagem gerenciar propriedades do painel.
- Solucionar problemas do GitHub:
   - Corrigir [emitir 703](https://github.com/Microsoft/sqlopsstudio/issues/703): inserir texto em forma de HTML em dados de edição faz com que o valor a ser exibido incorretamente até que a atualização
   - Corrigir [emitir 821](https://github.com/Microsoft/sqlopsstudio/issues/821): sqlopsstudio.deb de dependência de pacote
   - Corrigir [emitir 1260](https://github.com/Microsoft/sqlopsstudio/issues/1260): palavra-chave 'distinct' não realçado
   - Corrigir [emitir 1332](https://github.com/Microsoft/sqlopsstudio/issues/1332): dados de edição reverter linha não funciona
   - Corrigir [emitir 1215](https://github.com/Microsoft/sqlopsstudio/issues/1215): extensão do SQL Agent e a barra de status
   - Corrigir [emitir 1316](https://github.com/Microsoft/sqlopsstudio/issues/1316): SQL Agent não redimensionar depois de alterar o tamanho do windows


Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/sqlopsstudio/releases).



## <a name="april-2018-april-public-preview"></a>De 2018 de abril (visualização pública de abril)

Data de lançamento: 25 de abril de 2018  
versão: 0.28.6

O *visualização pública abril* contém correções e aprimoramentos. 

- Melhorias para a extensão de visualização do agente SQL.
- Maior suporte a arquivos grandes e protegido para salvar Admin protegido e > 256 milhões de arquivos no Studio de operações do SQL.
- Integrado a divisão de Terminal para trabalhar com vários terminais abertos ao mesmo tempo.
- Imprimir pé de contagem de arquivos no disco reduzido de instalação para instalações mais rápidas e tempos de inicialização.
- Continue corrigir problemas do GitHub:
   - Corrigir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): quando o Visualizador gráfico gera um erro, ocorrerá um comportamento inesperado.
   - Corrigir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitação de recurso: opção para grupos de servidor a ser expandido por padrão.
   - Corrigir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - sugestão incorreta para o comando 'Atualizar'.
   - Corrigir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): espera que o plano de consulta quando seleciona showplan XML na grade de resultados.
   - Corrigir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): Adicionar colchetes para chamada ms_foreachdb de flyfishingdba.
   - Corrigir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): erro de handshake de PRÉ-LOGON SSL/TLS.
   - Corrigir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): Exibir insights criptografado antes de mostrar o erro.
   - Corrigir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): novas ações de consulta no Gerenciador de widget e restauração são interrompidas.
   - Corrigir [emitir 1068](https://github.com/Microsoft/sqlopsstudio/issues/1068): painel Saída windows pops-up com a mensagem de erro para o banco de dados do SQL Azure.
   - Corrigir [emitir 1069](https://github.com/Microsoft/sqlopsstudio/issues/1069): caixa de diálogo de Conexão mostra erro de servidor necessária quando inicialmente exibido.
   - Corrigir [emitir 1070](https://github.com/Microsoft/sqlopsstudio/issues/1070): grupos de servidores agora precisam de um clique duplo para expandir.
   - Corrigir [emitir 1072](https://github.com/Microsoft/sqlopsstudio/issues/1072): plano de fundo do controle de seleção é semitransparente.
   - Corrigir [emitir 1115](https://github.com/Microsoft/sqlopsstudio/issues/1115): corrigir problemas de acessibilidade de todos os alto contraste no Studio de operações do SQL.
   - Corrigir [emitir 1101](https://github.com/Microsoft/sqlopsstudio/issues/1101): falha de extensão para atualização "baixar manualmente" link vai para um local incorreto.
   - Corrigir [emitir 1103](https://github.com/Microsoft/sqlopsstudio/issues/1103): rolagem V não está funcionando na guia página inicial.
   - Corrigir [emitir 1104](https://github.com/Microsoft/sqlopsstudio/issues/1104): guias de extensão SQL parou de funcionar.


Um realce significativo para a visualização pública de abril é a atualização de código de origem de plataforma 1.21 de código do Visual Studio. Isso coloca em várias atualizações para o editor de núcleo e o workbench do ponto de 1.19 sincronização anterior. Alguns exemplos incluem o seguinte:

- [Nova interface do usuário de notificações](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) - facilmente gerenciar e revisar as notificações do SQL Studio de operações.
- [Integrado a divisão de Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals) -trabalhar com vários terminais abertos ao mesmo tempo.
- [Salvar arquivos grandes e protegidos](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) - salve Admin protegidos e > 256 milhões de arquivos no Studio de operações do SQL.
- [Maior suporte a grandes arquivos](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -otimizações de buffer de texto para arquivos grandes.
- [Pesquisa de configurações melhorada](https://code.visualstudio.com/updates/v1_20#_settings-search) - facilmente encontrar a configuração direita com a pesquisa de idioma natural.
- [Trechos de código global](https://code.visualstudio.com/updates/v1_20#_global-snippets) -criar trechos de código que você pode usar em todos os tipos de arquivo.
- [Seleção múltipla do Explorer](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -executar ações em vários arquivos ao mesmo tempo.
- [Erros e avisos no Explorer](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) - rapidamente navegar para erros em sua base de código.
- [Arrastar e soltar, copiar e cole em windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -mover arquivos entre janelas abertas do SQL Studio de operações.
- [Suporte de submódulo Git](https://code.visualstudio.com/updates/v1_20#_git-submodules) -Git executar operações em repositórios do Git aninhadas.
- [Suporte de leitor de tela de terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -Terminal integrado agora tem o modo de "Otimização de leitor de tela".
- [Layout de editor centralizado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -maximizar seu código exibindo o estado real da tela.
- [Resultados da pesquisa horizontal (visualização)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -você pode agora exibir resultados da pesquisa em um painel horizontal.

Para obter detalhes adicionais, check-out de [notas de versão de fevereiro do Visual Studio código](https://code.visualstudio.com/updates/v1_21)e o [notas de versão de janeiro do Visual Studio código](https://code.visualstudio.com/updates/v1_20).

Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>De 2018 de março (março visualização pública)

Data de lançamento: 28 de março de 2018  
versão: 0.27.3

O *Public Preview de março* continua a atender os principais problemas do GitHub e destina-se em melhorar nossa história de extensibilidade. Habilitando o Gerenciador de extensões, melhora o gerenciamento de painel e fornecendo o SQL Agent e extensões de insights especificamente. Esta versão inclui os seguintes aprimoramentos:

- Melhorar o modelo de extensibilidade do painel para oferecer suporte a insights com guias e painéis de configuração.
   - Gerenciador de extensões permite simple aquisição das extensões.
   - Extensões de painel para sp_whoisactive de [whoisactive.com](http://www.whoisactive.com).
   - Para obter detalhes, consulte [estender a funcionalidade do SQL operações Studio](extensions.md).
- Adicionar outras [APIs de extensibilidade para o Gerenciador de conexão e objeto](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) gerenciamento.
- Continuar corrigir o cliente importante [GitHub problemas](https://github.com/Microsoft/sqlopsstudio/issues).


## <a name="february-2018-february-public-preview"></a>De 2018 fevereiro (fevereiro visualização pública)

Data de lançamento: 15 de fevereiro de 2018  
versão: 0.26.7

O *visualização pública fevereiro* inclui algumas sugestões de recursos e correções de bug de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

- Introdução de instalação de atualização automática, fornecendo uma notificação quando uma nova versão está disponível para download 
- O campo de caixa de diálogo de Conexão 'Database' agora é uma lista suspensa preenchida dinamicamente que contém uma lista de bancos de dados preenchida com o servidor especificado.
- Corrigir [emitir 6](https://github.com/Microsoft/sqlopsstudio/issues/6): manter a conexão e o banco de dados selecionado ao abrir novas guias de consulta.
- Corrigir [emitir 22](https://github.com/Microsoft/sqlopsstudio/issues/22): 'Nome do servidor' e 'Nome do banco de dados' - esses podem ser suspensos em vez de caixas de texto?
- Corrigir [emitir 549](https://github.com/Microsoft/sqlopsstudio/issues/549): a instalação silenciosa do modo silencioso/muito resulta em abrir após a instalação do aplicativo.
- Corrigir [emitir 481](https://github.com/Microsoft/sqlopsstudio/issues/481): adicionar a opção "Verificar atualizações".
- Editor SQL colorização e correções de preenchimento automático:
   - Corrigir [emitir 584](https://github.com/Microsoft/sqlopsstudio/issues/584): palavra-chave "Completo" não realçado pelo IntelliSense.
   - Corrigir [emitir 345](https://github.com/Microsoft/sqlopsstudio/issues/345): funções de SQL colorir dentro do editor.
   - Corrigir [emitir 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] mais recente "]" exibirá a cor verde.
   - Corrigir [emitir 225](https://github.com/Microsoft/sqlopsstudio/issues/225): palavra-chave de cor não correspondem.
   - Corrigir [emitir 60](https://github.com/Microsoft/sqlopsstudio/issues/60): sql inválido cor realce de sintaxe ao usar a tabela temporária na cláusula from.
- Apresente a API de extensibilidade de Conexão.
- Integração do VS 1.19 do Editor de código.
- Atualize o componente JustinPealing/html-plano de consulta para coleta várias melhorias de Visualizador de plano de consulta.


## <a name="january-2018-january-public-preview"></a>De 2018 janeiro (janeiro visualização pública)

Data de lançamento: 17 de janeiro de 2018  
versão: 0.25.4

O *visualização pública janeiro* inclui algumas sugestões de recursos e correções de bug de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

- Conexões do servidor salvas estão disponíveis na caixa de diálogo de Conexão.
- Habilite saída ativa. Saída ativa é desativada por padrão, para habilitar consulte [configuração de saída Hot](settings.md#hot-exit).
- Guia-cores com base no grupo de servidores. Cores de guia está desativado por padrão, para habilitar consulte [guia Configuração de cor](settings.md#tab-color).
- Alterar *nome do servidor* para *Server* na caixa de diálogo de Conexão.
- Correção dividida *executar consulta atual* comando.
- Correção de bug de script de separação de arrastar e soltar.
- Correção incorretova fixado ícone do Menu Iniciar.
- Corrija a conta do Azure ausente ícone de marca.


## <a name="december-2017-december-public-preview"></a>Dezembro de 2017 (visualização pública de dezembro)

Data de lançamento: 19 de dezembro de 2017  
versão: 0.24.1

O *visualização pública dezembro* inclui várias correções de bugs em todas as áreas de recurso, bem como os seguintes aprimoramentos:

- Criar caixa de diálogo de regra de Firewall agora está disponível para ajudar a se conectar ao banco de dados do SQL Azure e o Azure SQL Data Warehouse.
- Adicionada a instalação do Windows e Linux DEB e RPM pacotes de instalação.
- Gerencie o editor de layout visual do painel.
- *Como alterar script* e *Script como executar* comandos.
- *Executar consulta atual com o plano real* comando.
- Integre o editor de código do VS 1.18.1 plataformas.
- Permitir que os arquivos de carregamento da extensão do VSIX.
- Suporte à sintaxe de iteração em lotes "VÁ N".


## <a name="november-2017"></a>Novembro de 2017

Data de lançamento: 15 de novembro de 2017  
versão: 0.23.6

- Versão de inicial [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes guias de início rápido para começar:
- [Conectar e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar e consultar o depósito de dados do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
