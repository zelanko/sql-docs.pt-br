---
title: "Notas de versão do Microsoft SQL operações Studio (visualização) | Microsoft Docs"
description: "Notas de versão do Microsoft SQL operações Studio (visualização)"
ms.custom: tools|sos
ms.date: 02/15/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b8c5e3cce8f84f0565c764a47d3f3b7c1709454
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de versão do SQL Studio de operações (visualização)

**[Baixe a visualização pública de fevereiro](download.md)**

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

Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).


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
