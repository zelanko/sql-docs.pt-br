---
title: Oracle Source | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4898a61b0f64f79b32a9efc81f0a41a025e6d2ad
ms.sourcegitcommit: c4258a644ac588fc222abee2854f89a81325814c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72545063"
---
# <a name="oracle-source"></a>Oracle Source

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

A origem do Oracle extrai dados do Oracle Database com os seguintes modos:

- Uma tabela ou exibição.

- Os resultados de uma instrução SQL.

A origem usa um Gerenciador de Conexões do Oracle para se conectar à origem do Oracle. Para saber mais, confira o [Gerenciador de Conexões do Oracle](oracle-connection-manager.md).

## <a name="error-output"></a>Saída de erro

A saída de erro inclui as seguintes colunas:  

- **Código do Erro**: um número que representa o tipo de erro do erro atual. O código de erro pode ser do:
    - Servidor Oracle. Confira a descrição detalhada de erros na documentação do banco de dados Oracle.
    - Tempo de execução SSIS. Para obter uma lista dos códigos de erro SSIS, consulte a Referência de código e mensagem de erro SSIS.
- **Coluna de Erro**: o número da coluna de origem que causa os erros de conversão.

- **Colunas de dados do erro**: os dados que causam o erro.

A origem do Oracle retorna erros ocorridos durante o processo de carregamento e extração da saída do erro. Para saber mais, confira [Editor do Oracle Source (Página Saída de Erro)](#oracle-source-editor-error-output-page).

## <a name="troubleshooting-the-oracle-source"></a>Solucionando problemas da origem do Oracle

Você pode registrar as chamadas ODBC que a origem do Oracle faz para as fontes de dados Oracle para solucionar problemas de exportação de dados. Para registrar as chamadas ODBC que a origem do Oracle faz a fontes de dados Oracle, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados.*

## <a name="oracle-source-custom-properties"></a>Propriedades personalizadas da origem do Oracle

As propriedades personalizadas da origem do Oracle estão abaixo. Todas as propriedades são de leitura/gravação.

|Nome da propriedade|Tipo de Dados|Descrição|
|:-|:-|:-|
|AccessMode|Inteiro (enumeração)|O modo usado para acessar o banco de dados. Os valores possíveis são **Nome da Tabela** e **Comando SQL**. O padrão é **Nome da Tabela**.|
|BatchSize|Integer|O tamanho do lote para carregamento em massa. Esse é o número de registros extraído como uma matriz. <br>Esta propriedade é definida somente pelo **Editor Avançado**|
|DefaultCodePage|Integer|A página de código a ser usada quando a fonte de dados não tiver informações da página de código. <br>Esta propriedade é definida somente pelo **Editor Avançado**.|
|PreFetchCount|Integer|O número de linhas de pré-busca. <br>Esta propriedade é definida somente pelo **Editor Avançado**.|
|SqlCommand|Cadeia de caracteres|O comando SQL a ser executado quando AccessMode é definido como Comando SQL.|
|TableName|Cadeia de caracteres|O nome da tabela com os dados a serem usados quando AccessMode for definido como Nome da Tabela.|

## <a name="configuring-the-oracle-source"></a>Como configurar o Oracle Source

Você pode configurar o Oracle Source programaticamente ou por meio do SSIS Designer.

O Editor do Oracle Source é mostrado na figura abaixo. Ele contém a Página do Gerenciador de Conexões, a Página de Colunas e a Página de Saída de Erro.

Saiba mais em uma das seções a seguir:

- [Editor do Oracle Source (página Connection Manager)](#oracle-source-editor-connection-manager-page)
- [Editor do Oracle Source (página Colunas)](#oracle-source-editor-columns-page)
- [Editor do Oracle Source (página Saída de Erro)](#oracle-source-editor-error-output-page)

![](media/oracle-source.png)

A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.

Para abrir a caixa de diálogo **Editor Avançado** :

- Na tela **Fluxo de Dados** do seu projeto do Integration Services, clique com o botão direito do mouse no Oracle Source e selecione **Mostrar Editor Avançado**.

Para saber mais sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado**, confira [Propriedades Personalizadas do Oracle Source](#oracle-source-custom-properties).

## <a name="oracle-source-editor-connection-manager-page"></a>Editor do Oracle Source (página Gerenciador de Conexões)

Na página do **Gerenciador de Conexões**, a caixa de diálogo do **Editor de Oracle Source** é para selecionar o Banco de dados do Oracle como fonte, tabela ou exibição do banco de dados.

**Para abrir a página do Gerenciador de Conexões do Editor do Oracle Source**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém a origem do Oracle.

- Na guia Fluxo de Dados, clique duas vezes na origem do Oracle.
### <a name="options"></a>Opções

**Connection manager**

Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões do Oracle.

**Nova**

Clique em **Nova**. A caixa de diálogo **Editor do Gerenciador de Conexões do Oracle** é aberta, e nela você pode criar um novo gerenciador de conexões.

**Modo de acesso a dados**

Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:

|Opção|Descrição|
|:-|:-|
|Tabela ou exibição|Recupere os dados de uma tabela ou exibição na fonte de dados Oracle. Quando esta opção é selecionada, selecione uma tabela ou exibição disponível no banco de dados da lista para **Nome da tabela ou da exibição**.|
|Comando SQL|Recupere os dados da fonte de dados Oracle usando uma consulta SQL. Quando esta opção for selecionada, insira uma consulta de uma das seguintes maneiras: <br>Insira o texto da consulta SQL no campo **Texto do comando do SQL** . <br>Clique em **Procurar** para carregar a consulta SQL de um arquivo de texto. <br>Clique em **Analisar consulta** para verificar a sintaxe do texto da consulta.|

**Visualização**

Clique em **Visualizar** para exibir até as primeiras 200 linhas dos dados extraídos da tabela ou exibição selecionada.

## <a name="oracle-source-editor-columns-page"></a>Editor do Oracle Source (página Colunas)

Na página **Colunas**, a caixa de diálogo do **Editor do Oracle Source** é usada para mapear uma coluna de saída em cada coluna externa (origem).

**Para abrir a página Colunas do Editor do Oracle Source**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém a origem do Oracle.

- Na guia Fluxo de Dados, clique duas vezes na origem do Oracle.

- No Editor do Oracle Source, clique em Colunas.

### <a name="options"></a>Opções

**Colunas Externas Disponíveis**

Uma lista de colunas externas disponíveis que podem ser selecionadas para adicionar à lista **Coluna Externa** na ordem em que são selecionadas. Esta tabela não pode ser usada para adicionar ou excluir colunas.

Marque a caixa de seleção **Selecionar Tudo** para selecionar todas as colunas.

**Colunas Externas**

As colunas externas (origem) que você selecionou estão listadas em ordem.
Para alterar a ordem, primeiro, limpe a lista **Coluna Externa Disponível" e selecione as colunas com uma ordem diferente.

**Coluna de Saída**

O nome da coluna externa (origem) selecionada é o nome de saída padrão. Contudo, você pode inserir qualquer nome exclusivo.
> [!NOTE]
>
>Caso haja colunas com tipos de dados não suportados, haverá um alerta mostrando que os tipos de dados não são suportados e as colunas relacionadas serão removidas das colunas de mapeamento.

## <a name="oracle-source-editor-error-output-page"></a>Editor do Oracle Source (página Saída de Erro)

Use a página **Saída de Erro** da caixa de diálogo **Editor do Oracle Source** para selecionar as opções para tratamento de erros.

**Para abrir a página Saída de Erro do Editor do Oracle Source**

- No SQL Server Data Tools, abra o pacote do SQL Server Integration Services (SSIS) que contém a origem do Oracle.

- Na guia Fluxo de Dados, clique duas vezes na origem do Oracle.

- No Editor do Oracle Source, clique em Saída de Erro.

### <a name="options"></a>Opções

**Comportamento do erro**

Selecione como a origem do Oracle deve tratar os erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.
**Seção relacionada**: [Tratamento de erro em dados](https://docs.microsoft.com/en-us/sql/integration-services/data-flow/error-handling-in-data?view=sql-server-2017)

**Truncation**

Selecione como a origem do Oracle deve tratar o truncamento em uma linha: ignorar a falha, redirecionar a linha ou causar falha no componente.

## <a name="next-steps"></a>Próximas etapas

- Configurar o [Destino Oracle](oracle-destination.md).
- Caso tenha dúvidas, visite a [TechCommunity](https://aka.ms/AA5u35j).
