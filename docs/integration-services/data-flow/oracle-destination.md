---
title: Destino Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ee964e5c1c58ea54da3f3451c0ffdde29e71b23
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75246935"
---
# <a name="oracle-destination"></a>Destino Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

O destino Oracle carrega dados em massa no Oracle Database.

O destino usa o Gerenciador de Conexões do Oracle para se conectar à fonte de dados. Para saber mais, confira o [Gerenciador de Conexões do Oracle](oracle-connection-manager.md).

Um destino Oracle inclui mapeamentos entre as colunas de entrada e as colunas na fonte de dados de destino. Você não precisa mapear as colunas de entrada para todas as colunas de destino, mas, dependendo das propriedades das colunas de destino, podem ocorrer erros se nenhuma das colunas de entrada for mapeada para as colunas de destino. Por exemplo, se uma coluna de destino não permitir valores nulos, uma coluna de entrada deve ser mapeada para aquela coluna de destino. Além disso, se os dados de entrada não forem compatíveis com o tipo de coluna no destino, ocorrerá um erro no runtime. Dependendo da configuração de comportamento do erro, este será ignorado, causará uma falha ou a linha será redirecionada à saída de erro.

O destino Oracle tem uma entrada regular e uma saída de erro.

As colunas de tipos de dados sem suporte são excluídas das colunas, e é emitido um aviso antes do mapeamento.
Para saber mais, confira o [Suporte a tipo de dados](oracle-data-type-support.md).

## <a name="load-options"></a>Opções de carregamento

Há suporte para dois modos de carregamento de acesso. O modo pode ser definido no [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page). Os dois modos são:

- Carregamento em lote: este modo serve para carregar dados na tabela do Oracle em lotes, sendo que todo o lote é inserido na mesma transação.
Para obter detalhes sobre como configurar este modo, confira o [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page) e as [Propriedades Personalizadas do Destino Oracle](#oracle-destination-custom-properties).

- Carregamento rápido usando Direct Path: este modo destina-se ao uso do modo de caminho direto do driver para carregamento da tabela do Oracle. Há restrições de uso deste modo; para obter detalhes, confira a documentação do Oracle.  
Para obter detalhes sobre como configurar este modo, confira o [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page) e as [Propriedades Personalizadas do Destino Oracle](#oracle-destination-custom-properties).

## <a name="error-handling"></a>Tratamento de erros

O destino Oracle tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:

- **Código do Erro**: um número que representa o tipo de erro do erro atual. O código de erro pode ser do:
    - Servidor Oracle. Confira a descrição detalhada de erros na documentação do banco de dados Oracle.
    - runtime SSIS. Para obter uma lista dos códigos de erro SSIS, consulte a Referência de código e mensagem de erro SSIS.
- **Coluna de Erro**: o número da coluna de origem que causa os erros de conversão.

- **Colunas de dados do erro**: os dados que causam o erro.

Os tipos de erros de saída, com suporte, durante o processo de carregamento são: conversão de dados, truncamento, violação de restrição, entre outros. Confira o [Editor de Destino do Oracle (Página de Saída de Erro)](#oracle-destination-editor-error-output-page).

A propriedade **número máximo de erros (MaxErrors)** define o número máximo de erros que pode ocorrer. Quando o número máximo é atingido, a execução cessa e retorna os erros. E somente os registros de execução antes de o número máximo de erros ser atingido são incluídos na tabela de destino. confira o [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page) para obter detalhes de configuração.

## <a name="parallelism"></a>Paralelismo

No modo de carregamento em lote, não há nenhuma restrição na configuração de execução paralela, mas o desempenho pode ser afetado pelo mecanismo padrão de bloqueio de registro. O volume de perda de desempenho dependerá da organização de dados e da tabela.

No protocolo do caminho direto (carregamento rápido), somente um destino Oracle pode ser configurado para ser executado na mesma tabela ao mesmo tempo, mas o modo Parallel pode ser usado.

O caminho direto paralelo permite vários carregamentos de caminho direto, com os quais vários destinos Oracle podem ser configurados para serem executados simultaneamente na mesma tabela e ao mesmo tempo. O Oracle não bloqueia a tabela de destino exclusivamente para uso na sessão de carregamento rápido; isso permite a execução de componentes adicionais de destino de carregamento rápido para carregar a mesma tabela de destino em paralelo.
O caminho direto paralelo é mais restritivo, qualquer uso de paralelismo deve ser planejado antecipadamente.

Não há motivo para usar uma única sessão paralela.

Confira a documentação do Oracle sobre as restrições do uso de carregamentos de caminho direto paralelo.

Para saber mais, confira as [Propriedades Personalizadas do Destino do Oracle](#oracle-destination-custom-properties).

## <a name="troubleshooting-the-oracle-destination"></a>Solução de problemas de destino Oracle

Você pode registrar as chamadas ODBC que a origem do Oracle faz para as fontes de dados Oracle para solucionar problemas de exportação de dados. Para registrar as chamadas ODBC que a origem do Oracle faz a fontes de dados Oracle, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados.*

## <a name="oracle-destination-custom-properties"></a>Propriedades personalizadas de destino Oracle

A tabela a seguir descreve as propriedades personalizadas do destino Oracle. Todas as propriedades são de leitura/gravação.

|Nome da propriedade|Tipo de Dados|Descrição|Modo de carregamento|
|:-|:-|:-|:-|
|BatchSize|Integer|O tamanho do lote para carregamento em massa. Esse é o número de linhas carregado como um lote.|Usado somente no modo de lote.|
|DefaultCodePage|Integer|A página de código a ser usada quando a fonte de dados não tiver informações da página de código. <br>**Observação**: esta propriedade é definida somente pelo **Editor Avançado**.|Uso em ambos os modos.|
|FastLoad|Boolean|Caso o carregamento rápido seja usado. O valor padrão é **false**. Esse também pode ser definido no [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page). |Uso em ambos os modos.|
|MaxErrors|Integer|O número de erros que pode ocorrer antes que o fluxo de dados cesse. O valor padrão é **0**, o que significa que não há limite para o número de erros.<br> Se o **Fluxo de redirecionamento** for selecionado na página de **Tratamento de erros**. Antes que o limite de número de erros seja atingido, todos os erros retornam na saída de erro. Para saber mais, confira o [Tratamento de erros](#error-handling).|Usado somente no modo de carregamento rápido.|
|NoLogging|Boolean|Caso o registro em log do banco de dados esteja desabilitado. O valor padrão é **False**, o que significa que o registro em log está habilitado.|Uso em ambos os modos.|
|Paralelo|Boolean|Se o carregamento paralelo for permitido. **True** indica que outras sessões de carregamento podem ser executadas na mesma tabela de destino.<br> Para saber mais, confira [Paralelismo](#parallelism).|Usado somente no modo de carregamento rápido.|
|TableName|String|O nome da tabela com os dados que estão sendo usados.|Usado em ambos os modos.|
|TableSubName|String|O subnome ou a subpartição. Esse valor é opcional.<br> **Observação**: Essa propriedade só pode ser definida no **Editor Avançado**.|Usado somente no modo de carregamento rápido.|
|TransactionSize|Integer|O número de inserções que pode ser feito em uma única transação. O padrão é o **BatchSize**.|Usado somente no modo de lote.|
|TransferBufferSize|Integer|O tamanho do buffer de transferência. O valor padrão é 64 KB.|Usado somente no modo de carregamento rápido.|

## <a name="configuring-the-oracle-destination"></a>Configurando o destino Oracle

O destino Oracle pode ser configurado programaticamente ou por meio do Designer SSIS.

O Editor de Destino do Oracle é mostrado na figura abaixo. Ele contém a Página do Gerenciador de Conexões, a Página de Mapeamentos e a Página de Saída de Erro.

Saiba mais em uma das seções a seguir:

- [Editor de Destino do Oracle (Página do Gerenciador de Conexões)](#oracle-destination-editor-connection-manager-page)
- [Editor de Destino do Oracle (Página de Mapeamentos)](#oracle-destination-editor-mappings-page)
- [Editor de Destino do Oracle (Página de Saída de Erro)](#oracle-destination-editor-error-output-page)

![Destino Oracle](media/oracle-destination.png)

A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.
Para abrir a caixa de diálogo **Editor Avançado** :

- Na tela **Fluxo de Dados** do seu projeto do Integration Services, clique com o botão direito do mouse no destino Oracle e selecione **Mostrar Editor Avançado**.

Para saber mais sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, confira as [Propriedades Personalizadas do Destino Oracle](#oracle-destination-custom-properties).

## <a name="oracle-destination-editor-connection-manager-page"></a>Editor de Destino do Oracle (Página do Gerenciador de Conexões)

Use a página do **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino do Oracle** para selecionar o gerenciador de conexões do Oracle para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.

**Para abrir a Página do Gerenciador de Conexões do Editor de Destino do Oracle**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém o destino Oracle.

- Na guia Fluxo de Dados, clique duas vezes no destino Oracle.

- No Editor de Destino do Oracle, clique em Gerenciador de Conexões.

### <a name="options"></a>Opções

**Connection manager**

Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões do Oracle.

**Novo**

Clique em **Nova**. A caixa de diálogo **Editor do Gerenciador de Conexões do Oracle** é aberta, e nela você pode criar um novo gerenciador de conexões.

**Modo de acesso aos dados**

Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:

|Opção|Descrição|
|:-|:-|
|Nome da tabela|Configurar o destino Oracle para funcionar no modo de lote. Opções:<br><br> **Nome da tabela ou da exibição**: selecione uma tabela ou exibição disponível no banco de dados na lista.<br><br> **Tamanho da transação**: insira o número de inserções que podem ser realizadas em uma única transação. O padrão é o **BatchSize**.<br><br> **Tamanho do lote**: digite o tamanho (número de linhas carregadas) do lote para o carregamento em massa.
|Nome da tabela – Carregamento Rápido|Configurar o destino Oracle para funcionar no modo de carregamento rápido (Direct Path). <br><br>As opções disponíveis são:<br><br> **Nome da tabela ou da exibição**: selecione uma tabela ou exibição disponível no banco de dados na lista.<br><br> **Carregamento paralelo**: Caso o carregamento paralelo esteja habilitado. Para saber mais, confira [Paralelismo](#parallelism).<br><br> **Sem registro em log**: esta caixa de seleção desabilita o registro em log do banco de dados. Esse registro em log é um banco de dados Oracle usado para fins de recuperação, não relacionado ao rastreamento.<br><br> **Número máximo de erros**: o número máximo de erros que pode ocorrer antes que o fluxo de dados cesse. O valor padrão é 0, o que significa que não há limite de número.<br><br> Todos os erros que podem ocorrer retornam na saída de erro.<br><br> **Tamanho do buffer de transferência (KB)** : insira o tamanho do buffer de transferência. O tamanho padrão é 64 KB.|

**Exibir dados existentes**

Clique em **Exibir dados existentes** para exibir até 200 linhas de dados da tabela selecionada.

## <a name="oracle-destination-editor-mappings-page"></a>Editor de Destino do Oracle (Página de Mapeamentos)

Use a página de **Mapeamentos** da caixa de diálogo **Editor de Destino do Oracle** para mapear as colunas de entrada para as colunas de destino.

**Para abrir a Página de Mapeamentos do Editor de Destino do Oracle**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém o destino Oracle.

- Na guia Fluxo de Dados, clique duas vezes no destino Oracle.

- No Editor de Destino do Oracle, clique em Mapeamentos.

### <a name="options"></a>Opções

**Colunas de Entrada Disponíveis**

A lista de colunas de entrada disponíveis. Arraste e solte uma coluna de entrada em uma coluna de destino disponível para mapear as colunas.

**Colunas de Destino Disponíveis**

A lista de colunas de destino disponíveis. Arraste e solte uma coluna de destino em uma coluna de entrada disponível para mapear as colunas.

**Coluna de Entrada**

Exiba as colunas de entrada que você selecionou. Você pode remover os mapeamentos selecionando **< ignorar >** para excluir as colunas da saída.

**Coluna de Destino**

Exiba todas as colunas de destino disponíveis, mapeadas e não mapeadas.

> [!NOTE]
>
>As colunas de tipos de dados sem suporte serão excluídas do mapeamento, e um aviso é emitido.

## <a name="oracle-destination-editor-error-output-page"></a>Editor de Destino do Oracle (Página de Saída de Erro)

Use a página de Saída de Erro da caixa de diálogo Editor de Destino do Oracle para selecionar as opções para tratamento de erros.

**Para abrir a Página de Saída de Erro do Editor de Destino do Oracle**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém o destino Oracle.

- Na guia Fluxo de Dados, clique duas vezes no destino Oracle.

- No Editor de Destino do Oracle, clique em Saída de Erro.

### <a name="options"></a>Opções

**Comportamento do erro**

Selecione como a origem do Oracle deve tratar os erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.
**Seção relacionada**: [Tratamento de erro em dados](https://docs.microsoft.com/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**Truncation**

Selecione como a origem do Oracle deve tratar o truncamento em uma linha: ignorar a falha, redirecionar a linha ou causar falha no componente.

## <a name="next-steps"></a>Próximas etapas

- Configurar o [Gerenciador de Conexões do Oracle](oracle-connection-manager.md).
- Configurar a [Origem do Oracle](oracle-source.md).
- Configurar o [Destino Oracle](oracle-destination.md).
- Caso tenha dúvidas, visite a [TechCommunity](https://aka.ms/AA5u35j).
