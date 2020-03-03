---
title: Conectar-se à origem do Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f8eba07362ac5780d1d7790d5553aaa397b7847e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75245094"
---
# <a name="connect-to-the-teradata-source"></a>Conectar-se à origem do Teradata

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

A origem do Teradata extrai dados de bancos de dados do Teradata usando:
- Uma tabela ou exibição.
- Os resultados de uma instrução SQL.

A origem usa o gerenciador de conexões do Teradata para se conectar à origem do Teradata. Confira mais informações em [Usar o gerenciador de conexões do Teradata](teradata-connection-manager.md).

## <a name="troubleshoot-the-teradata-source"></a>Solucionar problemas da origem do Teradata

Você pode registrar as chamadas que a origem do Teradata faz para a API TPT (Teradata Parallel Transporter). Para isso, habilite o registro em log do pacote e selecione o evento **Diagnóstico** no nível do pacote.

Você pode registrar em log as chamadas ODBC (Conectividade Aberta de Banco de Dados) que a origem do Teradata faz ao driver ODBC do Teradata habilitando o rastreamento do gerenciador de driver ODBC. Confira mais informações em [Como gerar um rastreamento ODBC com o Administrador de Fonte de Dados ODBC](https://docs.microsoft.com/sql/odbc/admin/setting-tracing-options).

## <a name="parallelism"></a>Paralelismo

A origem do Teradata dá suporte ao paralelismo, no qual os trabalhos de exportação podem acessar a mesma tabela ou tabelas diferentes ao mesmo tempo. A variável de banco de dados `MaxLoadTasks` define o limite do número de trabalhos de exportação que podem ser executados ao mesmo tempo. Você pode definir esse número máximo usando a variável `MaxLoadTasks`.

## <a name="teradata-source-custom-properties"></a>Propriedades personalizadas da origem do Teradata

As propriedades personalizadas da origem do Teradata são listadas na tabela a seguir. Todas as propriedades são de leitura/gravação.

|Nome da propriedade|Tipo de dados|Descrição|
|:-|:-|:-|
|AccessMode|Inteiro (enumeração)|O modo usado para acessar o banco de dados. Os valores possíveis são *Nome da Tabela* e *Comando SQL*. O valor padrão é *Nome da Tabela*.|
|BlockSize|Integer|O tamanho do bloco, em bytes, usado ao retornar dados para o cliente. O valor padrão é 1.048.576 (1 MB). O valor mínimo é 256 bytes. O valor máximo é 16.775.168 bytes.<br> Essa propriedade está no painel **Editor Avançado**.|
|BufferMaxSize|Integer|O tamanho máximo total do buffer de dados retornado pela função GetBuffer. Esse tamanho deve ser grande o suficiente para manter pelo menos uma linha de dados, incluindo o cabeçalho da linha, a linha de dados real e o trailer do buffer. O tamanho padrão máximo total do buffer de dados é de 16.775.552 bytes. <br>Confira mais informações em [Exportar dados de um banco de dados do Teradata usando GetBuffer](https://docs.teradata.com/reader/TvVKKmxaBAoyETJZD8zz_g/oaxiwNJmnCa6UctY4k498w).|
|BufferMode|Boolean|O valor padrão é *True*. O valor deverá ser *True* se o recurso PutBuffer for usado. Essa propriedade está no painel **Editor Avançado**.|
|DataEncryption|Boolean|O valor padrão é *False*. A criptografia de segurança completa será usada se o valor for *True*.|
|DefaultCodePage|Integer|A página de código a ser usada quando a fonte de dados não tiver informações sobre a página de código. Essa propriedade está no painel **Editor Avançado**.|
|DetailedTracingLevel|Inteiro (enumeração)|Selecione uma das seguintes opções para o rastreamento avançado: <br> *Off*: sem registro em log avançado. <br> *Geral*: o rastreamento geral de atividades específicas do driver é registrado. <br> *CLI*: o rastreamento de atividades relacionadas ao CLIv2 é registrado. <br> *Notificar Método*: o rastreamento de atividades relacionadas ao recurso de notificação é registrado. <br> *Biblioteca Comum*: o rastreamento de atividades da biblioteca opcommon é registrado. <br> *Tudo*: todo o rastreamento de atividades anteriores é registrado. <br> O arquivo de log de rastreamento avançado é definido na propriedade `DetailedTracingFile`. <br> A propriedade `DetailedTracingFile` deverá ser definida se a opção não estiver *desativada*. Essa propriedade está no painel **Editor Avançado**.|
|DetailedTracingFile|String|O caminho do arquivo de log gerado automaticamente quando *DetailedTracingLevel* não está *desativado*. Essa propriedade está no painel **Editor Avançado**.|
|DiscardLargeRow|Boolean|O valor padrão é *False*. Removerá as linhas grandes (maiores que 64 KB) se o valor for *True*.|
|ExtendedStringColumnsAllocation|Boolean|*Fator de Alocação Máxima de Caracteres de Transferência* será usado se o valor for *True*. <br> Esse valor deverá ser definido como *True* se a propriedade `Export Width Table ID` do banco de dados do Teradata estiver definida como *Padrões Máximos*. <br> O valor padrão é *False*.|
|JobMaxRowSize|Integer|Pode haver suporte ao tamanho máximo da linha. Esse valor será necessário se o valor `DiscardLargeRow` for *True*.<br>Valores válidos:  <br>*64* (valor padrão): pode haver suporte para comprimentos de linha de 2 bytes. <br>*1024*: pode haver suporte para comprimentos de linha de 4 bytes.|
|MaxSessions|Integer|O número máximo de sessões que estão conectadas. Esse valor deve ser maior que um. O valor padrão é uma sessão para cada AMP (Processador de Módulo de Acesso) disponível.|
|MinSessions|Integer|O número mínimo de sessões que estão conectadas. Esse valor deve ser maior que um. O valor padrão é uma sessão para cada AMP disponível.|
|QueryBandSessInfo|Varchar|Uma expressão de banda de consulta baseada em sessão e definida pelo usuário em um formato de cadeia de conexão. Use essa propriedade para monitoramento e governança de estornos. Essa propriedade está no painel **Editor Avançado**.|
|SpoolMode|Varchar|Os valores válidos são: <br>*Spool*: use o valor padrão *Spool*. <br> *NoSpool*: Não use *Spool*. Esse valor só será válido se o DBS (servidor de banco de dados) der suporte a *NoSpool*. <br>  *NoSpoolOnly*: não use *Spool* de forma alguma. O trabalho finalizará com um erro se DBS não der suporte a *NoSpool*.|
|SqlCommand|String|O comando SQL a ser executado quando `AccessMode` estiver definido como *Comando SQL*.|
|TableName|String|O nome da tabela que contém  os dados a serem usados quando `AccessMode` estiver definido como *Nome da Tabela*.|
|TenacityHours|Integer|O número de horas que o driver TPT tenta fazer logon quando o número máximo de operações de carregamento/exportação ainda estiver em execução. O valor padrão é *4 horas*. Essa propriedade está no painel **Editor Avançado**.|
|TenacitySleep|Integer|O número de minutos que o driver TPT pausa antes de tentar fazer logon quando o limite é atingido. O limite é definido pelas propriedades `MaxSessions` e `TenacityHours`. O valor padrão é 6 minutos. Essa propriedade está no painel **Editor Avançado**.|
|UnicodePassThrough|Boolean|*Desativado* (valor padrão): desabilita a passagem Unicode. <br>*Em*: habilita a passagem Unicode.|

## <a name="configure-the-teradata-source"></a>Configurar a origem do Teradata

É possível configurar a origem do Teradata programaticamente ou usando o Designer do SSIS (SQL Server Integration Services).

O painel **Editor da Origem do Teradata** é mostrado na imagem a seguir. Para saber mais, acesse cada uma das seguintes seções do Editor de Origem do Teradata:

- [O painel Gerenciador de Conexões](#the-connection-manager-pane)
- [O painel Colunas](#the-columns-pane)
- [O painel Saída de Erro](#the-error-output-pane)

![Editor de Origem do Teradata](media/teradata-source.png)

O painel **Editor Avançado** contém propriedades que podem ser definidas programaticamente. Para abrir o painel:
- Na página **Fluxo de Dados** do seu projeto do Integration Services, clique com o botão direito do mouse na Origem do Oracle e selecione **Mostrar Editor Avançado**.

Para saber mais sobre as propriedades que podem ser definidas no painel **Editor Avançado**, confira [Propriedades personalizadas da origem do Teradata](#teradata-source-custom-properties).

## <a name="the-connection-manager-pane"></a>O painel Gerenciador de Conexões

Use o painel **Gerenciador de Conexões** para selecionar a instância do Gerenciador de Conexões do Teradata para a origem. Nesse painel, também é possível selecionar uma tabela ou uma exibição do banco de dados. Para abrir o painel:

1. No SQL Server Data Tools, abra o pacote SSIS que contém a origem do Teradata.

1. Na guia **Fluxo de Dados**, clique duas vezes na origem do Teradata.

1. No Editor de Origem do Teradata, selecione a guia **Gerenciador de Conexões**.

### <a name="options"></a>Opções

**Connection manager**

* Selecione na lista um gerenciador de conexões existente ou clique em **Novo** para criar uma nova instância de gerenciador de conexões para o Teradata.

**Novo**

* Selecione **Novo**. O painel **Editor do Gerenciador de Conexões do Teradata** é aberto. Nesse painel, você pode criar um novo gerenciador de conexões.

**Modo de acesso a dados**

* Escolha o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:

    |Opção|Descrição|
    |:-|:-|
    |Nome da tabela – Exportação de TPT|Recupere os dados de uma tabela ou exibição na fonte de dados do Teradata. Quando esta opção é selecionada, selecione uma tabela ou exibição disponível no banco de dados da lista para **Nome da tabela ou da exibição**.|
    |Comando SQL – Exportação de TPT|Recupere os dados da fonte de dados do Teradata usando uma consulta SQL. Quando esta opção for selecionada, insira uma consulta de uma das seguintes maneiras: <ul><li>Insira o texto da consulta SQL no campo **Texto do comando do SQL** .</li><li>Selecione **Procurar** para carregar a consulta SQL de um arquivo de texto.</li><li>Selecione **Analisar consulta** para verificar a sintaxe do texto da consulta.</li></ul>|

**Visualização**

* Selecione **Visualizar** para exibir até 200 das primeiras linhas dos dados extraídos da tabela ou exibição selecionada.

## <a name="the-columns-pane"></a>O painel Colunas

Use o painel **Colunas** para mapear uma coluna de saída em cada coluna externa (origem). Para abrir o painel:

1. No SQL Server Data Tools, abra o pacote SSIS que contém a origem do Teradata.

1. Na guia **Fluxo de Dados**, clique duas vezes na origem do Teradata.

1. No Editor de Origem do Teradata, selecione a guia **Colunas**.

### <a name="options"></a>Opções

**Colunas Externas Disponíveis**

Esta tabela lista as colunas externas disponíveis que você pode selecionar para adicionar à lista **Coluna externa**. Você pode listar as colunas na ordem que quiser. Você não pode usar esta tabela para adicionar ou excluir colunas.

* Para escolher todas as colunas, marque a caixa de seleção **Selecionar Tudo**.

**Colunas Externas**

As colunas externas (origem) que você selecionou aparecem em ordem. Para alterar a ordem, primeiro limpe a lista **Coluna Externa Disponível**, depois selecione as colunas em uma ordem diferente.

**Coluna de Saída**

Embora o nome da coluna externa (origem) selecionada seja o nome de saída padrão, você pode inserir qualquer nome exclusivo.

>[!NOTE]
>>Se houver colunas que contenham tipos de dados sem suporte, você receberá um aviso que exibe os tipos de dados sem suporte, e as colunas relevantes serão removidas das colunas de mapeamento.

## <a name="the-error-output-pane"></a>O painel Saída de Erro

Use o painel **Saída de Erro** para selecionar opções de tratamento de erros. Para abrir o painel:

1. No SQL Server Data Tools, abra o pacote SSIS que contém a origem do Teradata.

1. Na guia **Fluxo de Dados**, clique duas vezes na origem do Teradata.

1. No Editor de Origem do Teradata, selecione a guia **Saída de Erro**.

### <a name="options"></a>Opções

**Comportamento do erro**

* Selecione como a origem do Teradata deve tratar erros em um fluxo: 
  * Ignorar a falha
  * Redirecionar a linha
  * Falha no componente

**Tópicos relacionados:** Confira [Tratamento de erro em dados](error-handling-in-data.md).

**Truncation**

* Selecione como a origem do Teradata deve tratar truncamento em um fluxo: 
  * Ignorar a falha
  * Redirecionar a linha
  * Falha no componente

## <a name="next-steps"></a>Próximas etapas

- Configure o [Destino do Teradata](teradata-destination.md).
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA6iwdw).
