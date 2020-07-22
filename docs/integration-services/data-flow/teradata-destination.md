---
title: Destino do Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2091999bce0fbacb99083239a7eb209fa8939505
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912347"
---
# <a name="teradata-destination"></a>Destino do Teradata

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

O destino do Teradata carrega dados em massa no Banco de Dados do Teradata.

O destino usa o gerenciador de conexões do Teradata para se conectar à fonte de dados. Confira mais informações em [Gerenciador de conexão do Teradata](teradata-connection-manager.md).

## <a name="load-options"></a>Opções de carregamento

O destino do Teradata dá suporte a dois modos de carregamento de dados:

- **Fluxo de TPT**: Esse modo usa o operador de Fluxo de API TPT (protocolo Teradata TPump).

- **Carregamento TPT** (carregamento em massa rápido): Esse modo usa o operador de Carregamento de API TPT (protocolo Teradata FastLoad) para carregamento em massa rápido.

O modo de carregamento rápido tem as seguintes restrições:

- O limite de sessões para o banco de dados do Teradata é determinado por qualquer fator abaixo que for encontrado primeiro:
    - Limites de sessão definidos usando o comando SESSIONS
    - O limite de uma sessão por AMP para o Banco de Dados do Teradata
    - O limite da plataforma para o número máximo de sessões por aplicativo: definido pela variável MaxSess no arquivo de software de interface do COP (Processador de Comunicações), CLISPB. DAT. Você pode usar o comando TDP SET MAXSESSIONS para especificar o limite de plataforma. O limite padrão é igual a MAXSESS do servidor.

- Não há suporte para a união de índices.
- Não há suporte para referências de chave estrangeira em tabelas de destino.
- Não há suporte para tabelas de destino definidas com um índice secundário.

Para saber mais sobre as restrições de carregamento rápido do Teradata, confira a referência do carregamento rápido do Teradata.

É possível definir o modo no [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#teradata-destination-editor-connection-manager-page).

## <a name="error-handling"></a>Tratamento de erros

Os erros retornados durante o processo de carregamento são gravados em tabelas de erro temporárias que ficam bloqueadas durante o processo de carregamento.
A propriedade **Número máximo de erros (MaxErrors)** do Editor Avançado define o número máximo de erros que pode ocorrer.

Se o número máximo de erros for maior que zero, serão geradas tabelas de erros com nomes exclusivos, e a mensagem informativa será impressa no log do pacote. Os erros podem ser recuperados por saída de erro do componente SSIS padrão.

As tabelas temporárias são removidas quando o processo de carregamento é concluído. Se as tabelas temporais não puderem ser lidas pelo destino do Teradata, não serão removidas, a menos que a propriedade **Sempre remover tabela de erros** esteja marcada.  Se o processo de carregamento for interrompido antes da conclusão, você precisará remover manualmente essas tabelas, se necessário. Essas tabelas ficam no mesmo banco de dados com a tabela de destino.

Quando o **Número máximo de erros** é atingido, o estado da tabela de destino depende do modo em uso.

- No modo de carregamento rápido, a tabela de destino não pode ser usada. Para executar novamente, você deve truncar ou remover e recriar a tabela de destino. Não há suporte para reversão.
- No modo de operador do Fluxo de TPT, o destino do Teradata é executado por meio do mecanismo de linha em buffer. Se o trabalho falhar, todas as alterações concluídas (buffers que foram enviados) no momento da falha serão permanentes nas tabelas de destino. Não há nenhum conceito de reversão. As tabelas de erros serão removidas.

O destino do Teradata tem uma saída de erro. Confira mais informações em [Editor de Destino do Teradata (Página Saída de Erro)](#teradata-destination-editor-error-output-page).

## <a name="parallelism"></a>Paralelismo

O paralelismo é restrito no modo de carregamento rápido, vários trabalhos independentes de carregamento rápido não podem acessar a mesma tabela ao mesmo tempo. Além disso, o número de trabalhos simultâneos de carregamento rápido é limitado pela variável **MaxLoadTasks** do banco de dados.

Não há nenhuma restrição de paralelismo no modo de Fluxo de TPT. É possível executar simultaneamente vários destinos do Teradata na mesma tabela, embora isso possa reduzir o desempenho por Teradata. Confira a documentação do Teradata para obter mais informações.

## <a name="troubleshooting-the-teradata-destination"></a>Solução de problemas de destino do Teradata

Você pode registrar as chamadas que a origem do Teradata faz para a API TPT (Teradata Parallel Transporter). Você pode habilitar o registro em log do pacote e selecione o evento **Diagnóstico** no nível do pacote para registrar as chamadas.

Você pode registrar as chamadas ODBC que a origem do Teradada faz para o driver ODBC do Teradata ao habilitar o rastreamento do gerenciador do driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados*.

## <a name="teradata-destination-custom-properties"></a>Propriedades personalizadas de destino do Teradata

A tabela a seguir descreve as propriedades personalizadas do destino do Teradata. Todas as propriedades são de leitura/gravação.

|Nome da propriedade|Tipo de Dados|Descrição|
|:-|:-|:-|
|AlwaysDropErrorTable|Boolean|O padrão é **False**. Remova todas as tabelas de erro se for **True**, mesmo que o destino do Teradata falhe na leitura.|
|ArraySupport|Boolean|O padrão é **True**. Os grupos DML usam ArraySupport se for **True**. Aplicável somente ao Fluxo de TPT. Essa propriedade está no **Editor Avançado**.|
|Buffers|Integer|O número de buffers de solicitação a aumentar, o valor pode ser definido de 2 a 64. Aplicável somente ao Fluxo de TPT. Essa propriedade está no **Editor Avançado**.|
|BufferMode|Boolean|O padrão é **True**. Deve ser **True** se o recurso PutBuffer for usado. Essa propriedade está no **Editor Avançado**.|
|BufferSize|Integer|O tamanho do buffer de saída (em KB) usado para enviar os totais de carregamento. O valor padrão é 1.024. Aplicável somente para o Carregamento do TPT. Essa propriedade está no **Editor Avançado**.|
|DataEncryption|Boolean|O padrão é **False**. A criptografia de segurança completa será usada se for **True**.|
|DefaultCodePage|Integer|A página de código a ser usada quando a fonte de dados não tiver informações da página de código. <br>**Observação**: Essa propriedade está no **Editor Avançado**.|
|DetailedTracingLevel|Inteiro (Enumeração)|Selecione uma das seguintes opções para o rastreamento avançado: <br> **Off**: sem registro em log avançado. <br> **Geral**: o rastreamento geral de atividades específicas do driver é registrado. <br> **CLI**: o rastreamento de atividades relacionadas ao CLIv2 é registrado. <br> **Notificar Método**: o rastreamento de atividades relacionadas ao recurso de notificação é registrado. <br> **Biblioteca Comum**: o rastreamento de atividades da biblioteca opcommon é registrado. <br> **Tudo**: o rastreamento de todas as atividades acima é registrado. <br> O arquivo de log de rastreamento avançado é definido na propriedade **DetailedTracingFile**. <br> A propriedade **DetailedTracingFile** deve ser definida se a opção não estiver desativada. <br> Essa propriedade está no **Editor Avançado**.|
|DetailedTracingFile|String|O caminho do arquivo de log gerado automaticamente quando **DetailedTracingLevel** não está **desativado**. Essa propriedade está no **Editor Avançado**.|
|DiscardLargeRow|Boolean|O padrão é **False**. Remover linhas grandes (maiores que 64K) se for **True**|
|ErrorTableName|String|Nome da tabela de erros. O padrão é o nome da tabela de destino|
|ExtendedStringColumnsAllocation|Boolean|**Fator de Alocação Máxima de Caracteres de Transferência** será usado se for **True**. <br> Esse valor deve ser definido como **True** se a propriedade **Exportar ID da Tabela de Largura** do banco de dados do Teradata estiver definida como **Padrões Máximos**. <br> O padrão é **False**.|
|FastLoad|Boolean|O carregamento rápido é usado se for **True**. O valor padrão é **false**. Também pode ser definido no [Editor de Destino do Teradata (Página do Gerenciador de Conexões)](#teradata-destination-editor-connection-manager-page).|
|MaxErrors|Integer|O número de erros que pode ocorrer antes que o fluxo de dados cesse. O valor padrão é **0**, o que significa que não há limite para o número de erros.<br> Se o **Fluxo de redirecionamento** for selecionado na página de **Tratamento de erros**. Antes que o limite de número de erros seja atingido, todos os erros retornam na saída de erro. Confira mais informações em [Editor de Destino do Teradata (Página Saída de Erro)](#teradata-destination-editor-error-output-page).|
|MaxSessions|Integer|O número máximo de sessões que estão conectadas. Esse valor deve ser maior que um. O valor padrão é uma sessão para cada AMP disponível.|
|MinSessions|Integer|O número mínimo de sessões que estão conectadas. Esse valor deve ser maior que um. O valor padrão é uma sessão para cada AMP disponível.|
|Pack|Integer|O número de instruções a serem empacotadas em uma solicitação com várias instruções. O padrão é 20, o máximo permitido é 2400. Aplicável somente ao Fluxo de TPT. Essa propriedade está no **Editor Avançado**.|
|PackMaximum|Boolean|Determina dinamicamente o fator máximo do pacote para o trabalho de fluxo atual se for **True**. Aplicável somente ao Fluxo de TPT. Essa propriedade está no **Editor Avançado**.|
|QueryBandSessInfo|Varchar|Uma expressão de banda de consulta definida pelo usuário e com base em sessão para habilitar o monitoramento e a governança de estornos. Essa propriedade deve estar no formato de cadeia de conexão. Essa propriedade está no **Editor Avançado**.|
|ReplicationOveride|Inteiro (enumeração)|Opções: <br> **Padrão**: a instrução No SET SESSION OVERRIDE REPLICATION é enviada ao banco de dados. As configurações padrão do banco de dados são usadas. <br> **Em**: os controles de serviço de replicação normais são substituídos. <br> **Off**: os controles de serviço de replicação normais são usados. <br> Essa propriedade é aplicável somente ao Fluxo de TPT. <br> Essa propriedade está no **Editor Avançado**.|
|Robust|Boolean|A lógica de reinicialização robusta é usada em operações de recuperação e reinicialização se for **True**. Essa propriedade é aplicável somente ao **Fluxo de TPT**. Essa propriedade está no **Editor Avançado**.|
|TableName|String|O nome da tabela com os dados que estão sendo usados.|
|TenacityHours|Integer|O número de horas que o driver TPT tenta fazer logon quando o número máximo de operações de carregamento/exportação ainda estiver em execução. O padrão é de 4 horas. Essa propriedade está no **Editor Avançado**|
|TenacitySleep|Integer|Os minutos que o driver TPT pausa antes de tentar fazer logon quando o limite é atingido. O limite é definido pelas propriedades **MaxSessions** e **TenacityHours**. O padrão é seis minutos. Essa propriedade está no **Editor Avançado**|
|UnicodePassThrough|Boolean|Off (padrão): desabilita a Passagem Unicode. <br>On: habilita a Passagem Unicode.|

## <a name="configuring-the-teradata-destination"></a>Configurar o destino do Teradata

O destino do Teradata pode ser configurado programaticamente ou por meio do Designer SSIS.

O Editor de Destino do Teradata é mostrado na figura abaixo. Ele contém a Página do Gerenciador de Conexões, a Página de Mapeamentos e a Página de Saída de Erro.

Para obter mais informações, consulte um dos tópicos a seguir.

- [Editor de Destino do Teradata (Página do Gerenciador de Conexões)](#teradata-destination-editor-connection-manager-page)
- [Editor de Destino do Teradata (Página de Mapeamentos)](#teradata-destination-editor-mappings-page)
- [Editor de Destino do Teradata (Página de Saída de Erro)](#teradata-destination-editor-error-output-page)

![editor de destino](media/teradata-destination.png)

A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.
Para abrir a caixa de diálogo **Editor Avançado** :

- Na tela **Fluxo de Dados** do seu projeto do Integration Services, clique com o botão direito do mouse no destino do Teradata e selecione **Mostrar Editor Avançado**.

Para saber mais sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, confira as [Propriedades personalizadas do destino do Teradata](#teradata-destination-custom-properties).

## <a name="teradata-destination-editor-connection-manager-page"></a>Editor de Destino do Teradata (Página do Gerenciador de Conexões)

Use a página do **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino do Teradata** para selecionar o gerenciador de conexões do Teradata para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.

Para abrir a Página do Gerenciador de Conexões do Editor de Destino do Teradata

- No SQL Server Data Tools, abra o pacote do SSIS (SQL Server Integration Services) que contém o destino do Teradata.

- Na guia Fluxo de Dados, clique duas vezes no destino do Teradata.

- No Editor de Destino do Teradata, clique em Gerenciador de Conexões.

### <a name="options"></a>Opções

**Connection manager**

Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões do Teradata.

**Novo**

Clique em **Nova**. A caixa de diálogo **Editor do Gerenciador de Conexões do Teradata** é aberta, e nela você pode criar um novo gerenciador de conexões.

**Modo de acesso aos dados**

Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:

|Opção|Descrição|
|:-|:-|
|Nome da Tabela – Fluxo de TPT|Modo incremental usando o operador de Fluxo de TPT. <br>**Nome da tabela ou da exibição**: selecione uma tabela ou exibição existente na lista. Esta lista mostra apenas as primeiras 1.000 tabelas. Você pode digitar o prefixo do nome da tabela ou usar qualquer parte do nome com o curinga (*) para listar a tabela ou as tabelas que deseja usar.|
|Nome da Tabela – Carregamento de TPL|Modo de carregamento rápido (Caminho Direto) usando o operador de carregamento da API TPT (protocolo Teradata FastLoad), que requer que a tabela de destino esteja vazia. <br>**Nome da tabela ou da exibição**: selecione uma tabela ou exibição existente na lista. Esta lista mostra apenas as primeiras 1.000 tabelas. Você pode digitar o prefixo do nome da tabela ou usar qualquer parte do nome com o curinga (*) para listar a tabela ou as tabelas que deseja usar.|

**Criptografia de dados** Marque a caixa de seleção para habilitar a criptografia de dados. O padrão não está selecionado.

**Sempre remover tabela de erros** Marque a caixa de seleção para remover tabelas de erros em todas as instâncias.

**Tabela de erros** Nome da tabela na qual os erros são gravados.

**Número mínimo de sessões** O número mínimo de sessões que estão conectadas. O valor padrão é uma sessão para cada AMP disponível. O valor deve ser maior que um.

**Número máximo de sessões** O número máximo de sessões que estão conectadas. O valor padrão é uma sessão para cada AMP disponível. O valor deve ser maior que um.

**Número máximo de erros** O número máximo de erros que podem ser retornados antes que o fluxo de dados seja interrompido ou redirecionado. 

## <a name="teradata-destination-editor-mappings-page"></a>Editor de Destino do Teradata (Página de Mapeamentos)

Use a página **Mapeamentos** da caixa de diálogo **Editor de Destino do Teradata** para mapear as colunas de entrada para as colunas de destino.

Para abrir a Página de Mapeamentos do Editor de Destino do Teradata

- No SQL Server Data Tools, abra o pacote do SSIS (SQL Server Integration Services) que contém o destino do Teradata.

- Na guia Fluxo de Dados, clique duas vezes no destino do Teradata.

- No Editor de Destino do Teradata, clique em Mapeamentos.

### <a name="options"></a>Opções

**Colunas de Entrada Disponíveis**

A lista de colunas de entrada disponíveis. Arraste e solte uma coluna de entrada em uma coluna de destino disponível para mapear as colunas.

**Colunas de Destino Disponíveis**

A lista de colunas de destino disponíveis. Arraste e solte uma coluna de destino em uma coluna de entrada disponível para mapear as colunas.

**Coluna de Entrada**

Exiba as colunas de entrada que você selecionou. Você pode remover os mapeamentos selecionando **< ignorar >** para excluir as colunas da saída.

**Coluna de Destino**

Exiba todas as colunas de destino disponíveis, mapeadas e não mapeadas.

>[!NOTE]
>
>As colunas de tipos de dados sem suporte serão excluídas do mapeamento, e um aviso é emitido.

## <a name="teradata-destination-editor-error-output-page"></a>Editor de Destino do Teradata (Página de Saída de Erro)
Use a página de Saída de Erro da caixa de diálogo Editor de Destino do Teradata para selecionar as opções para tratamento de erros.

**Para abrir a Página de Saída de Erro do Editor de Destino do Teradata**

- No SQL Server Data Tools, abra o pacote do SSIS (SQL Server Integration Services) que contém o destino do Teradata.

- Na guia Fluxo de Dados, clique duas vezes no destino do Teradata.

- No Editor de Destino do Teradata, clique em Saída de Erro.

### <a name="options"></a>Opções

**Comportamento do erro**

Selecione como o destino do Teradata deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.

**Tópicos relacionados**: [Tratamento de Erro em Dados](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**Truncation**

Selecione como o destino do Teradata deve tratar truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.

## <a name="next-steps"></a>Próximas etapas

- Configurar o [gerenciador de conexões do Teradata](teradata-connection-manager.md)
- Configurar a [origem do Teradata](teradata-source.md)
- Configurar o [destino do Teradata](teradata-destination.md)
- Em caso de dúvidas, acesse a [Tech Community](https://aka.ms/AA6iwdw).
