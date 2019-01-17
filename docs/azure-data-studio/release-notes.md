---
title: Notas de versão e o log de alterações
titleSuffix: Azure Data Studio
description: Notas de versão Data Studio do Azure
ms.custom: seodec18
ms.date: 01/17/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 163f5740626b0f4cb927272d46acddc79495e4c1
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361676"
---
# <a name="azure-data-studio-latest-release-notes-and-changelog"></a>Notas de versão mais recente do Studio de dados e log de alterações do Azure

**[Baixe e instale a versão mais recente!](download.md)**


## <a name="january-hotfix-2019-january-hotfix-release"></a>Hotfix de janeiro de 2019 (versão do Hotfix de janeiro)

Data de lançamento: 16 de janeiro de 2019  
Versão: 1.3.9

Versão 1.3.9 corrige alguns problemas descobertos em 1.3.8. Para obter detalhes, consulte [versão do Hotfix de janeiro](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).

Para obter informações detalhadas, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="january-2019-january-release"></a>Janeiro de 2019 (versão de janeiro)

Data de lançamento: 09 de janeiro de 2019  
Versão: 1.3.8

- Adicionado um novo instalador do usuário para Windows. Ao contrário do instalador do sistema existente, o novo instalador do usuário não requer privilégios de administrador. Isso também permite uma experiência de atualização mais fácil para não administradores.
- Suporte de autenticação do Active Directory do Azure.
- Anunciando a análise de desempenho de DM Idera SQL (versão prévia).
- Suporte de data-Tier Application Wizard na extensão do SQL Server Import.
- Atualizar para o [extensão de visualização do SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- Aprimoramentos do SQL Server Profiler.
- Resultados de Streaming para grandes consultas (visualização).
- Extensões de comunidade: sp_executesql to sql e o novo banco de dados.
- Resolvido [bugs e problemas](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1).

## <a name="november-2018-november-release"></a>Novembro de 2018 (versão de novembro)

Data de lançamento: 6 de novembro de 2018  
Versão: 1.2.4

- Atualizar para o [extensão de visualização do SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- Introdução ao colar a extensão de plano
- Apresentando a extensão de consultas de High Color, incluindo o tema do editor SSMS
- Correções no SQL Server Agent, Profiler e importação de extensões
- Corrigir o.Net Core fazendo com que o soquete KeepAlive problema quedas de conexões inativas no macOS
- Serviço de ferramentas de atualização do SQL para.Net Core 2.2 Preview 3 (para eventual suporte do AAD)

### <a name="bug-fixes"></a>Correções de bugs

- Corrigir [emitir #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexão perdida para BD SQL do Azure
- Corrigir [emitir #2914](https://github.com/Microsoft/azuredatastudio/issues/2914): Nó "Argumento inválido" exceção expansão OE banco de dados
- Corrigir [emitir #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Exibir mensagens de várias linhas corretamente nos resultados da consulta
- Corrigir [emitir #2906](https://github.com/Microsoft/azuredatastudio/pull/2906): Corrija o nome do documento de editar dados quando o nome da tabela contém caracteres especiais
- Corrigir [emitir #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): Compilado na extensão de log de alterações diz para verificar as notas de versão do VSCode para alterações
- Corrigir [emitir #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): Tema de alto contraste duplos/triplos de ícones
- Corrigir [emitir #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Adicionar uma interface de linha de comando para se conectar a um SQL Server
- Corrigir [emitir #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Adicionar suporte de tema do plano de consulta
- ...

## <a name="october-2018-october-release"></a>Outubro de 2018 (versão de outubro)

Data de lançamento: 29 de outubro de 2018  
Versão: 1.1.4

- Apresentando o Azure Resource Explorer para procurar bancos de dados SQL do Azure
- Aumentar a robustez de conectividade do Pesquisador de objetos e o Editor de consultas
- Aprimoramentos de extensões do SQL Agent
- Atualizar para o [extensão de visualização do SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>Correções de bugs
- Corrigir [emitir #2717](https://github.com/Microsoft/azuredatastudio/issues/2717): O resultado de coluna XML, clico em formatação
- Corrigir [emitir #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Windows de resultado da largura está incompleta
- Corrigir [emitir #2999](https://github.com/Microsoft/azuredatastudio/issues/2999): Não foi possível carregar o arquivo Tracing no Mac ao se conectar ao banco de dados
- Corrigir [emitir #2851](https://github.com/Microsoft/azuredatastudio/issues/2851): Gráfico de série temporal não sejam renderizadas corretamente
- Corrigir [emitir #2996](https://github.com/Microsoft/azuredatastudio/issues/2996): Tabela temporária perda devido a alteração repentina de sessão
- ...

Para obter informações detalhadas, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-september-ga-release"></a>Setembro de 2018 (versão de setembro GA)

Data de lançamento: 24 de setembro de 2018  
Versão: 1.0

Versão de disponibilidade geral do estúdio de dados do Azure (anteriormente conhecido como o SQL Operations Studio).

- Anunciando a extensão de visualização do SQL Server de 2019.
  - Suporte para recursos de visualização do SQL Server 2019 incluindo [cluster de big data](../big-data-cluster/big-data-cluster-overview.md) dão suporte.
    - Conecte-se ao Gateway de HDFS/Spark que acompanha a versão prévia do SQL Server 2019.
    - Procurar HDFS, carregar arquivos, salvar arquivos e iniciar ações úteis, como analisar no bloco de anotações para arquivos CSV.
    - Enviar trabalhos do Spark no painel ou clique duas vezes em uma conexão de HDFS/Spark no Pesquisador de objetos.
  - Blocos de anotações do Studio dados do Azure
    - Criar ou abrir Notebooks usando um visualizador de bloco de anotações integrado. Nesta versão, o bloco de anotações visualizador dá suporte à conexão para kernels locais e o cluster de big data 2019 do SQL Server somente.
    - Use as bibliotecas de PROSA acelerador de código no bloco de anotações para saber os tipos de dados e formato de arquivo para a preparação de dados rápido.
  - Gerenciador de recursos do Azure
    - O modo de exibição do Gerenciador de recursos do Azure permite procurar pontos de extremidade relacionados a dados para suas contas do Azure e criar conexões para eles no Pesquisador de objetos. Nesta versão, servidores e bancos de dados SQL do Azure têm suporte.
  - Assistente de tabela externa de criação de PolyBase do SQL Server
    - Crie uma tabela externa e suas estruturas de metadados de suporte com um assistente fácil de usar. Nesta versão, há suporte para servidores remotos do SQL Server e Oracle.
- Grade de resultados melhorias no desempenho e experiência do usuário para um grande número de conjuntos de resultados de consulta.
- Código de origem do Visual Studio Code é atualizada de 1.23 para 1.26.1 com Layout de grade e o melhor Editor de configurações (visualização).
- Melhorias de acessibilidade para o leitor de tela, navegação por teclado e alto contraste.
- Adicionado `Connection name` permite que você forneça um nome de exibição alternativa que o modo de exibição de servidores-let.

### <a name="bug-fixes"></a>Correções de bugs

- Corrigir [emitir #2647](https://github.com/Microsoft/azuredatastudio/issues/143): Os gráficos fez um grande avanço com versões anteriores.
- Corrigir [emitir #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que retorna a coluna inteira de hyperlinks JSON.
- ...

Para obter informações detalhadas, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), e [versões](https://github.com/Microsoft/azuredatastudio/releases).


## <a name="august-2018-august-public-preview"></a>Agosto de 2018 (visualização pública de agosto)

Data de lançamento: 30 de agosto de 2018  
Versão: 0.32.8

*0.32.8 contém correções para algumas regressões, encontradas no 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

O *agosto Public Preview* se concentra em correções de bugs, estabilização do produto e preenchendo as lacunas nos cenários existentes.  

- Anunciando a extensão de importação do SQL Server
- Gerenciamento de sessão do SQL Server Profiler
- Suporte de modelo de sessão do SQL Server Profiler
- Aprimoramentos do SQL Server Agent
- Nova extensão de comunidade: Kit de Respondente primeiro
- Aprimoramentos de qualidade de vida: Cadeias de conexão

### <a name="bug-fixes"></a>Correções de bugs

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

### <a name="known-issues"></a>Problemas conhecidos

- [Emitir #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Salvar como apenas salva primeira linha de dados do Excel
- [Emitir #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Não é possível conectar-se no Ubuntu 16.04 to SQL em um contêiner


## <a name="july-2018-july-public-preview"></a>Julho de 2018 (julho a visualização pública)

Data de lançamento: 19 de julho de 2018  
Versão: 0.31.4

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


## <a name="june-2018-june-public-preview"></a>Junho de 2018 (visualização pública de junho)

Data de lançamento: 20 de junho de 2018  
Versão: 0.30.6

O *junho Public Preview* contém os seguintes destaques:  

- **SQL Server Profiler para SQL Operations Studio *versão prévia***  versão inicial da extensão.
- O novo **SQL Data Warehouse** extensão inclui widgets de painel personalizável avançado identificando insights ao seu data warehouse. Isso desbloqueia os principais cenários de gerenciamento e ajuste seu data warehouse para garantir que ele é otimizado para desempenho consistente.
- **Editar dados "Filtragem e classificação"** dão suporte.
- **SQL Server Agent para o SQL Operations Studio *versão prévia***  aprimoramentos de extensão para trabalhos e o histórico de trabalho de modos de exibição.
- Aprimorado **Assistente de & estrutura do construtor de interface do usuário de caixa de diálogo** APIs de extensibilidade.
- Atualizar a plataforma de código do VS fonte código integrando [(1.22) de março de 2018](https://code.visualstudio.com/updates/v1_22) e [abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) libera.
- Corrigi problemas do GitHub:
  - Solicitação de recurso ([emitir 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Fazer os resultados da largura da coluna de ajuste automático de grade de dados, e/ou se lembrar de alterações manuais se a mesma consulta for executada novamente.
  - Corrigir [emitir 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Deve mostrar Adicionar mensagem e adicionar botão de conta da conta quando a conta vinculada está vazia.
  - Corrigir [emitir 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): Guia Conta vinculada é interrompido quando o modo de exibição é recolhido.
  - Corrigir [emitir 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): Serviço de ferramentas do SQL Falha ao abrir o arquivo. SQL no disco.
  - Corrigir [emitir 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Faltando "BETWEEN" palavra-chave SQL.
  - Corrigir [emitir 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Palavra-chave de 'MATCH' falhas de serviço de ferramentas do SQL.
  - Corrigir [emitir 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): "Novo Profiler" opção de menu de contexto no Pesquisador de objetos não faz nada.
  - Corrigir [emitir 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): Plano de consulta de "Explain" de editor de consulta é interrompido.


## <a name="may-2018-may-public-preview"></a>Maio de 2018 (maio de visualização pública)

Data de lançamento: 7 de maio de 2018  
Versão: 0.29.3

O *visualização pública podem* se concentra na estabilização e correções de bugs. Esse build contém os seguintes destaques:  

- Anunciando a extensão do Redgate SQL Search disponível no Gerenciador de extensões.
- Localização da comunidade disponível para 10 idiomas: Chinês alemão, espanhol, francês, italiano, japonês, coreano, português, russo, simplificado e chinês tradicional.
- Coleta de telemetria reduzida, experiência aprimorada de recusa e links no produto para declaração de privacidade.
- Gerenciador de extensões tem Marketplace aprimorado de experiência para descobrir facilmente extensões de comunidade.
- Trabalhos de extensão do SQL Agent e histórico de trabalho Exibir melhoria.
- Atualizações para whoisactive e extensões do relatórios do servidor.
- Melhore a rolagem de gerenciar propriedades do painel.
- Corrigi problemas do GitHub:
   - Corrigir [execute 703](https://github.com/Microsoft/azuredatastudio/issues/703): Inserir texto do tipo HTML em dados de edição faz com que o valor a ser exibido incorretamente após atualização
   - Corrigir [emitir 821](https://github.com/Microsoft/azuredatastudio/issues/821): dependência de pacote azuredatastudio.deb
   - Corrigir [emitir 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palavra-chave 'distinct' não realçado
   - Corrigir [emitir 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Editar dados reverter linha não funciona
   - Corrigir [emitir 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensão do agente SQL e a barra de status
   - Corrigir [emitir 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Redimensionamento do SQL Agent não depois altere o tamanho do windows




## <a name="april-2018-april-public-preview"></a>Abril de 2018 (visualização pública de abril)

Data de lançamento: 25 de abril de 2018  
Versão: 0.28.6

O *abril de visualização pública* contém correções de bugs e melhorias. 

- Melhorias para a extensão de visualização do agente SQL.
- Arquivo protegido e grande suporte aprimorado para salvar administrador protegida e > 256m arquivos dentro do SQL Operations Studio.
- Terminal integrado divisão para trabalhar com vários terminais abertos ao mesmo tempo.
- Imprimir pés de contagem de arquivo em disco reduzido de instalação para instalações mais rápidas e tempos de inicialização.
- Continue a corrigir problemas do GitHub:
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

Para obter mais informações, consulte o [Log de alterações](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>(Visualização pública de março) de março de 2018

Data de lançamento: 28 de março de 2018  
Versão: 0.27.3

O *Public Preview de março* continua abordar os principais problemas do GitHub e está focado em melhorar nossa história de extensibilidade. Especificamente, habilitar Extension Manager, melhorando o gerenciamento de painel e fornecendo SQL Agent e extensões de insights. Esta versão inclui os seguintes aprimoramentos:

- Aperfeiçoar o modelo de extensibilidade do painel para dar suporte a insights com guias e painéis de configuração.
   - Gerenciador de extensões permite que a aquisição simple das extensões.
   - Extensões de painel para sp_whoisactive partir [whoisactive.com](http://www.whoisactive.com).
   - Para obter detalhes, consulte [estendem a funcionalidade do SQL Operations Studio](extensions.md).
- Adicionar mais [APIs de extensibilidade para o Gerenciador de conexão e objeto](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) gerenciamento.
- Continuar a corrigir clientes importantes que afetam [problemas do GitHub](https://github.com/Microsoft/azuredatastudio/issues).


## <a name="february-2018-february-public-preview"></a>Fevereiro de 2018 (visualização pública de fevereiro)

Data de lançamento: 15 de fevereiro de 2018  
Versão: 0.26.7

O *fevereiro Public Preview* inclui algumas sugestões de recursos e correções de bugs de alta prioridade. Esta versão inclui os seguintes aprimoramentos:

- Apresentando a instalação da atualização automática, que a fornece uma notificação quando uma nova versão está disponível para download 
- O campo 'Banco de dados' de caixa de diálogo de Conexão agora é uma lista suspensa preenchida dinamicamente que contém uma lista de bancos de dados preenchida do servidor especificado.
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
- Introduza a API de extensibilidade de Conexão.
- Integração do VS 1.19 do Editor de código.
- Atualize o componente JustinPealing/html-planos de consulta para embarque várias melhorias de Visualizador de plano de consulta.


## <a name="january-2018-january-public-preview"></a>Janeiro de 2018 (janeiro a visualização pública)

Data de lançamento: 17 de janeiro de 2018  
Versão: 0.25.4

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
Versão: 0.24.1

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
Versão: 0.23.6

- Versão inicial do [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:
- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
