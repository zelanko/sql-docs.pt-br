---
title: Importar do Excel ou exportar para o Excel com o SSIS | Microsoft Docs
description: Saiba como importar ou exportar dados do Excel com o SQL Server Integration Services (SSIS), junto com os pré-requisitos, problemas conhecidos e limitações.
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d028e3aa679e91ca15f3a738f948b127517c112f
ms.sourcegitcommit: d463f543e8db4a768f8e9736ff28fedb3fb17b9f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36324740"
---
# <a name="import-data-from-excel-or-export-data-to-excel-with-sql-server-integration-services-ssis"></a>Importar dados do Excel ou exportar dados para o Excel com o SSIS (SQL Server Integration Services)

Este artigo descreve como importar dados do Excel ou exportá-los para o Excel com o SSIS (SQL Server Integration Services). O artigo também descreve os pré-requisitos, as limitações e os problemas conhecidos.

É possível importar dados do Excel ou exportá-los para o Excel criando um pacote do SSIS e usando o Gerenciador de Conexões do Excel e a Origem ou o Destino do Excel. Também é possível usar o Assistente de Importação e de Exportação do SQL Server, criado no SSIS.

Este artigo contém três conjuntos de informações de que você precisa para usar o Excel com êxito no SSIS ou para entender e solucionar problemas comuns:
1.  [Os arquivos necessários](#files-you-need).
2.  As informações que você precisa fornecer quando carrega dados bidirecionalmente no Excel.
    -   [Especifique o Excel](#specify-excel) como a fonte de dados.
    -   Forneça o [nome de arquivo e o caminho do Excel](#excel-file).
    -   Selecione a [versão do Excel](#excel-version).
    -   Especifique se a [primeira linha contém nomes de coluna](#first-row).
    -   Forneça a [planilha ou o intervalo que contém os dados](#sheets-ranges).
3.  Problemas conhecidos e limitações.
    -   Problemas com [tipos de dados](#issues-types).
    -   Problemas com a [importação](#issues-importing).
    -   Problemas com a [exportação](#issues-exporting).

## <a name="files-you-need"></a> Obter os arquivos necessários para se conectar ao Excel

Antes de poder importar dados do Excel ou exportá-los para o Excel, talvez seja necessário baixar os componentes de conectividade para o Excel, se você ainda não os tiver instalado. Os componentes de conectividade do Excel não são instalados por padrão.

Baixe a versão mais recente dos componentes de conectividade para Excel aqui: [Redistribuível de 2016 do Mecanismo de Banco de Dados do Microsoft Access](https://www.microsoft.com/download/details.aspx?id=54920).
  
A versão mais recente dos componentes podem abrir arquivos criados em versões anteriores do Excel.

Verifique se você baixou o *Redistribuível* de 2016 do Mecanismo de Banco de Dados do Access, e não o *Tempo de Execução* do Microsoft Access 2016.

Se o computador já tiver uma versão de 32 bits do Office, então será necessário instalar a versão de 32 bits dos componentes. Também é necessário executar o pacote do SSIS no modo de 32 bits ou executar a versão de 32 bits do Assistente de importação e de exportação.

Se você tiver uma assinatura do Office 365, talvez você veja uma mensagem de erro quando você executar o instalador. O erro indica que não é possível instalar o download lado a lado com os componentes do tipo clicar para executar do Office. Para ignorar essa mensagem de erro, execute a instalação no modo silencioso abrindo uma janela de Prompt de Comando e executando o arquivo .EXE baixado com a opção `/quiet`. Por exemplo:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

Se você tiver problemas para instalar o redistribuível de 2016, instale o redistribuível do 2010, em vez disto aqui: [Redistribuível do Mecanismo de Banco de Dados do Microsoft Access 2010](https://www.microsoft.com/download/details.aspx?id=13255). (Não há redistribuível para o Excel 2013.)

## <a name="specify-excel"></a> Especificar o Excel

A primeira etapa é indicar que você deseja se conectar ao Excel.

### <a name="in-ssis"></a>No SSIS
No SSIS, crie um Gerenciador de Conexões do Excel para se conectar ao arquivo de origem ou de destino do Excel. Há várias maneiras de criar o gerenciador de conexões:

-   Na área dos **Gerenciadores de Conexões**, clique com o botão direito do mouse e selecione **Nova conexão**. Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, selecione **EXCEL** e, em seguida, **Adicionar**.
 
-   No menu do **SSIS**, selecione **Nova conexão**. Na caixa de diálogo **Adicionar Gerenciador de Conexões do SSIS**, selecione **EXCEL** e, em seguida, **Adicionar**.

-   Crie o gerenciador de conexões ao mesmo tempo em que configura a **Origem do Excel** ou o **Destino do Excel** na página do **Gerenciador de conexões** do **Editor de Origem do Excel** ou do **Editor de Destino do Excel**.

### <a name="in-the-sql-server-import-and-export-wizard"></a>No Assistente de Importação e de Exportação do SQL Server
No Assistente de Importação e de Exportação, na página **Escolher uma fonte de dados** ou **Escolher um destino**, selecione **Microsoft Excel** na lista **Fonte de dados**.

Se você não vê o Excel na lista de fontes de dados, deve executar o assistente de 32 bits. Os componentes de conectividade do Excel são geralmente de 32 bits e não são visíveis no assistente de 64 bits.

## <a name="excel-file"></a> Arquivo e caminho do arquivo do Excel

A primeira parte das informações a ser fornecida é o caminho e o nome do arquivo do Excel. Forneça essas informações no **Editor do Gerenciador de Conexões do Excel** em um pacote do SSIS ou na página **Escolher uma fonte de dados** ou **Escolher um destino** do Assistente de Importação e de Exportação.

Insira o caminho e o nome do arquivo no seguinte formato:

-   Para um arquivo no computador local, **C:\\TestData.xlsx**.

-   Para um arquivo em um compartilhamento de rede, **\\\\Dados de\\Vendas\\TestData.xlsx**.

Ou clique em **Procurar** para localizar a planilha usando a caixa de diálogo **Abrir**.  
  
> [!IMPORTANT]
> Não é possível se conectar a um arquivo do Excel protegido por senha.

## <a name="excel-version"></a> Versão do Excel

A segunda parte dessas informações a ser fornecida é a versão do arquivo do Excel. Forneça essas informações no **Editor do Gerenciador de Conexões do Excel** em um pacote do SSIS ou na página **Escolher uma fonte de dados** ou **Escolher um destino** do Assistente de Importação e de Exportação.

Selecione a versão do Microsoft Excel que foi usado para criar o arquivo ou outra versão compatível. Por exemplo, se você teve dificuldades para instalar os componentes de conectividade de 2016, será possível instalar os componentes de 2010 e selecionar **Microsoft Excel 2007-2010** nesta lista.

Talvez você não consiga selecionar versões mais recentes do Excel na lista se você tiver apenas versões mais antigas dos componentes de conectividade instalados. A lista **versão do Excel** inclui todas as versões do Excel compatíveis com o SSIS. A presença de itens nesta lista não indica que os componentes de conectividade necessários estão instalados. Por exemplo, o **Microsoft Excel 2016** aparecerá na lista mesmo se você não tiver instalado os componentes de conectividade de 2016.

## <a name="first-row"></a> A primeira linha tem nomes de coluna

Se você estiver importando dados do Excel, a próxima etapa será indicar se a primeira linha dos dados contém nomes de coluna. Forneça essas informações no **Editor do Gerenciador de Conexões do Excel** em um pacote do SSIS ou na página **Escolher uma fonte de dados** do Assistente de Importação e de Exportação.

-   Se você desabilitar essa opção porque os dados de origem não contêm nomes de coluna, o assistente usará F1, F2 e assim por diante como títulos de coluna.
-   Se os dados contiverem nomes de coluna, mas você desabilitar essa opção, o assistente importará os nomes de coluna como a primeira linha de dados.
-   Se os dados de origem não contiverem nomes de coluna, mas você habilitar essa opção, o assistente usará a primeira linha dos dados de origem como os nomes de coluna. Nesse caso, a primeira linha dos dados de origem não está mais incluída nos dados em si.

Se você estiver exportando dados do Excel e habilitar essa opção, a primeira linha de dados exportados incluirá os nomes de coluna.

## <a name="sheets-ranges"></a> Planilhas e intervalos

Há três tipos de objetos do Excel que podem ser usados como a origem ou o destino dos seus dados: uma planilha, um intervalo nomeado ou um intervalo de células sem nome que você especifica com seu endereço.

-   **Planilha.** Para especificar uma planilha, acrescente o caractere `$` ao final do nome da planilha e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$]**. Ou procure um nome que termina com o caractere `$` na lista de tabelas e exibições existentes.

-   **Intervalo nomeado.** Para especificar um intervalo nomeado, forneça o nome do intervalo, por exemplo, **MyDataRange**. Ou procure um nome que não termine com o caractere `$` na lista de tabelas e exibições existentes.
    
-   **Intervalo sem nome.** Para especificar um intervalo de células ainda não nomeado, acrescente o caractere $ ao final do nome da planilha, adicione a especificação do intervalo e adicione delimitadores no começo e no final da cadeia de caracteres, por exemplo, **[Sheet1$A1:B4]**.

Para selecionar ou especificar o tipo de objeto do Excel que você deseja usar com a origem ou o destino dos seus dados, siga um destes procedimentos:

### <a name="in-ssis"></a>No SSIS

No SSIS, na página do **Gerenciador de conexões** do **Editor da Origem do Excel** ou do **Editor do Destino do Excel**, siga um destes procedimentos:

-   Para usar uma **planilha** ou um **intervalo nomeado**, selecione **Tabela ou exibição** como o **Modo de acesso a dados**. Em seguida, na lista **Nome da planilha do Excel**, selecione a planilha ou o intervalo nomeado.

-   Para usar um **intervalo sem nome** especificado com seu endereço, selecione o **Comando SQL** como o **Modo de acesso a dados**. Em seguida, no campo **texto do comando SQL**, insira uma consulta como o exemplo a seguir:

    ```sql
    SELECT * FROM [Sheet1$A1:B5]
    ```

### <a name="in-the-sql-server-import-and-export-wizard"></a>No Assistente de Importação e de Exportação do SQL Server
No Assistente de Importação e de Exportação, siga um destes procedimentos:

-   Quando você estiver **importando** do Excel, siga um destes procedimentos:

    -   Para usar uma **planilha** ou um **intervalo nomeado**, na página **Especificar Cópia ou Consulta de Tabela**, selecione **Copiar dados de uma ou mais tabelas ou exibições**. Em seguida, na página **Selecionar Tabelas de origem e exibições**, na coluna **Origem**, selecione as planilhas de origem e os intervalos nomeados.

    -   Para usar um **intervalo sem nome** especificado com seu endereço, na página **Especificar cópia ou consulta de tabela**, selecione **Escrever uma consulta para especificar os dados a serem transferidos**. Em seguida, na página **Fornecer uma Consulta de Origem**, forneça uma consulta semelhante ao exemplo a seguir:

        ```sql
        SELECT * FROM [Sheet1$A1:B5]
        ```

-   Quando você estiver **exportando** para o Excel, siga um destes procedimentos:

    -   Para usar uma **planilha** ou um **intervalo nomeado**, na página **Selecionar tabelas de origem e exibições**, na coluna **Destino**, selecione as planilhas de destino e os intervalos nomeados.

    -   Para usar um **intervalo sem nome** especificado com seu endereço, na página **Selecionar tabelas de origem e exibições**, na coluna **Destino**, insira o intervalo no seguinte formato sem delimitadores: `Sheet1$A1:B5`. O assistente adiciona os delimitadores.

Depois de selecionar ou de inserir os objetos do Excel a serem importados ou exportados, também será possível seguir estes procedimentos na página **Selecionar tabelas de origem e exibições** do assistente:

-   Revise os mapeamentos de coluna entre a origem e o destino selecionando **Editar mapeamentos**.

-   Visualize dados de exemplo para se certificar de que é o que você espera selecionando **Visualizar**.

## <a name="issues-types"></a>Problemas com tipos de dados

### <a name="data-types"></a>Tipos de dados

O driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Por exemplo, todas as colunas numéricas são interpretadas como duplas (DT_R8) e todas as colunas de cadeia de caracteres (que não sejam colunas de memorando) são interpretadas como cadeias Unicode de 255 caracteres (DT_WSTR). O SSIS mapeia os tipos de dados do Excel da seguinte maneira:

-   Numérico – flutuante de precisão dupla (DT_R8)

-   Moeda – moeda (DT_CY)

-   Booliano - booliano (DT_BOOL)

-   Data/hora – datetime (DT_DATE)

-   Cadeia – cadeia Unicode, 255 de comprimento (DT_WSTR)

-   Memorando – fluxo de texto Unicode (DT_NTEXT)

### <a name="data-type-and-length-conversions"></a>Tipo de dados e conversões de comprimento

O SSIS não converte implicitamente tipos de dados. Em decorrência disso, talvez você precise usar as transformações de Conversão de dados ou de Coluna derivada para converter dados do Excel explicitamente antes de carregá-los para um destino que não seja o Excel ou para converter dados de uma fonte diferente do Excel antes de carregá-los para um destino do Excel.

Veja alguns exemplos das conversões que podem ser necessárias:  
  
-   Conversão entre colunas de cadeias de caracteres Unicode e não Unicode do Excel com uma página de código específica.
  
-   Conversão entre colunas de cadeia de 255 caracteres e de comprimentos diferentes do Excel.
  
-   Conversão entre colunas numéricas de precisão dupla e outros tipos de colunas numéricas do Excel.

> [!TIP]
> Se você estiver usando o Assistente de Importação e de Exportação e seus dados precisarem de algumas dessas conversões, o assistente configurará as conversões necessárias para você. Em decorrência disso, mesmo quando você quiser usar um pacote do SSIS, talvez seja útil criar o pacote inicial usando o Assistente de Importação e de Exportação. Deixe o assistente criar e configurar gerenciadores de conexões, origens, transformações e destinos para você.

## <a name="issues-importing"></a> Problemas com a importação

### <a name="empty-rows"></a>Linhas vazias

Quando você especifica uma planilha ou um intervalo nomeado como a origem, o leitor lê o bloco de células *contíguo* que começa com a primeira célula não vazia no canto superior esquerdo da planilha ou do intervalo. Como resultado, seus dados não precisam começar na linha 1, mas você não pode ter linhas vazias nos dados de origem. Por exemplo, não é possível ter uma linha vazia entre os cabeçalhos da coluna e as linhas de dados nem um título seguido por linhas vazias na parte superior da planilha.

Se houver linhas vazias acima dos seus dados, não será possível consultá-los como uma planilha. No Excel, é necessário selecionar seu intervalo de dados, atribuir um nome ele e, em seguida, consultar o intervalo nomeado, em vez da planilha.

### <a name="missing-values"></a>Valores ausentes

O driver do Excel lê um determinado número de linhas (por padrão, oito linhas) na fonte especificada para determinar o tipo de dados de cada coluna. Quando uma coluna parece conter tipos de dados mistos, especialmente dados numéricos combinados com dados de texto, o driver decide em favor do tipo de dados majoritário e retorna valores nulos para as células que contêm dados de outro tipo. (Em uma ligação, o tipo numérico vence.) A maioria das opções de formatação de células na planilha de trabalho do Excel não parece afetar a determinação desse tipo de dados.

É possível modificar esse comportamento de driver do Excel especificando Modo de Importação para importar todos os valores como texto. Para especificar Modo de Importação, adicione `IMEX=1` ao valor de **Propriedades Estendidas** na cadeia de conexão do gerenciador de conexões do Excel na janela Propriedades. 

### <a name="truncated-text"></a>Texto truncado

Quando o driver determina que uma coluna do Excel contém dados de texto, ele seleciona o tipo de dados (cadeia ou memorando) com base no valor mais longo que ele obtém. Se o driver não descobre nenhum valor maior que 255 caracteres nas linhas que ele verifica, ele trata a coluna como uma coluna de cadeia de 255 caracteres, não como uma coluna de memorando. Assim, valores com mais de 255 caracteres podem estar truncados.

Para importar dados de uma coluna de memorando sem truncamento, você tem duas opções:

-   Certifique-se de que a coluna de memorando em pelo menos uma das linhas com amostras coletadas contém um valor maior que 255 caracteres

-   Aumente o número de linhas cujas amostras são coletadas pelo driver para incluir essa linha. É possível aumentar o número de linhas com amostras coletadas aumentando o valor de **TypeGuessRows** na seguinte chave do Registro:

| Versão de componentes redistribuíveis | Chave do Registro |
|---|---|
| Excel 2016 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel |
| Excel 2010 | HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel |
| | |

## <a name="issues-exporting"></a> Problemas com a exportação

### <a name="create-a-new-destination-file"></a>Criar um novo arquivo de destino

#### <a name="in-ssis"></a>No SSIS

Crie um Gerenciador de conexões do Excel com o caminho e o nome do arquivo do novo arquivo do Excel que você deseja criar. Em seguida, no **Editor de Destino do Excel**, para **Nome da planilha do Excel**, selecione **Novo** para criar a planilha de destino. Nesse ponto, o SSIS cria o novo arquivo do Excel com a planilha especificada.

#### <a name="in-the-sql-server-import-and-export-wizard"></a>No Assistente de Importação e de Exportação do SQL Server

Na página **Escolha um destino**, selecione **Procurar**. Na caixa de diálogo **Abrir**, navegue até a pasta em que você deseja que o novo arquivo do Excel seja criado, forneça um nome para o novo arquivo e, em seguida, selecione **Abrir**.

### <a name="export-to-a-large-enough-range"></a>Exportar para um intervalo grande o suficiente

Quando você especificar um intervalo como o destino, ocorrerá um erro se o intervalo tiver menos *colunas* do que os dados de origem. No entanto, se o intervalo especificado tiver menos *linhas* do que os dados de origem, o assistente continuará gravando linhas sem erro e estenderá a definição de intervalo para corresponder ao novo número de linhas.

### <a name="export-long-text-values"></a>Exportar valores de texto longos

Antes de salvar com sucesso cadeias de caracteres com mais de 255 caracteres em uma coluna do Excel, o driver deve reconhecer o tipo de dados da coluna de destino como **memorando** e não como **cadeia de caracteres**.

-   Se uma tabela de destino existente já contiver linhas de dados, então as primeiras linhas que serão amostradas pelo driver devem conter pelo menos uma instância com um valor maior que 255 caracteres na coluna de memorando.

-   Se uma nova tabela de destino for criada durante o desenvolvimento do pacote ou em tempo de execução ou pelo Assistente de Importação e de Exportação, então a instrução `CREATE TABLE` deverá usar LONGTEXT (ou um de seus sinônimos) como o tipo de dados da coluna de memorando de destino. No assistente, verifique a instrução `CREATE TABLE` e a revise, se necessário, clicando em **Editar SQL** ao lado da opção **Criar tabela de destino** na página **Mapeamentos de coluna**.

## <a name="related-content"></a>Conteúdo relacionado

Para obter mais informações sobre os componentes e os procedimentos descritos neste artigo, consulte os seguintes artigos:

### <a name="about-ssis"></a>Sobre o SSIS
[Gerenciador de Conexões do Excel](connection-manager/excel-connection-manager.md)  
[Origem do Excel](data-flow/excel-source.md)  
[Destino do Excel](data-flow/excel-destination.md)  
[Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
[Trabalhar com arquivos do Excel com a tarefa Script](extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)

### <a name="about-the-sql-server-import-and-export-wizard"></a>Sobre o Assistente de Importação e de Exportação do SQL Server
[Conectar-se a uma fonte de dados do Excel](/integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)  
[Começar com esse exemplo simples de Assistente de Importação e Exportação](/integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

### <a name="other-articles"></a>Outros artigos
[Importar dados do Excel para o SQL Server ou Banco de Dados SQL do Azure](/relational-databases/import-export/import-data-from-excel-to-sql.md)  

