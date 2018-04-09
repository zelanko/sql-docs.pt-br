---
title: Origem do Excel | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6a9795de30c7d4fbe2ede9a17043a916e5953cd5
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="excel-source"></a>Origem do Excel
  A origem do Excel extrai dados de planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Para obter informações detalhadas sobre como se conectar a arquivos do Excel, e sobre limitações e problemas conhecidos para carregar dados de ou para arquivos do Excel, consulte [Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md).

## <a name="access-mode"></a>Modo de acesso
 A origem do Excel fornece quatro modos de acesso a dados diferentes para extrair dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
-   Os resultados de uma instrução SQL armazenados em uma variável.  
  
 A origem do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo da planilha de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 A origem do Excel tem uma saída comum e uma saída de erro.  
  
## <a name="usage-considerations"></a>Considerações de uso  
 O Gerenciador de Conexões do Excel usa o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet 4.0 e driver ISAM do Excel com suporte para se conectar, além de ler e gravar dados nas fontes de dados do Excel.  
  
 Muitos artigos da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../includes/msconame-md.md)] documentam o comportamento desse provedor e driver e, embora esses artigos não sejam específicos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou de seus serviços de transformação de dados anteriores, talvez você queira obter mais informações sobre determinados comportamentos que podem levar a resultados inesperados. Para obter informações gerais sobre o uso e comportamento do driver do Excel, consulte [Como usar ADO com dados do Excel do Visual Basic ou do VBA](http://support.microsoft.com/kb/257819).  
  
 Os seguintes comportamentos do provedor Jet com o driver do Excel podem levar a resultados inesperados ao ler dados de uma fonte de dados do Excel.  
  
-   **Fontes de dados**. A fonte de dados em uma pasta de trabalho do Excel pode ser uma planilha de trabalho, à qual o sinal $ deve ser anexado (por exemplo, Planilha1$), ou um intervalo nomeado (por exemplo, MeuIntervalo). Em uma instrução SQL, o nome de uma planilha de trabalho deve ser delimitado (por exemplo, [Planilha1$]) para evitar um erro de sintaxe causado pelo sinal $. O Construtor de Consultas adiciona automaticamente esses delimitadores. Quando você especifica uma planilha de trabalho ou um intervalo, o driver lê o bloco contínuo de células começando com a primeira célula não vazia no canto superior esquerdo da planilha de trabalho ou do intervalo. Dessa forma, você não pode ter linhas vazias nos dados de origem ou uma linha vazia entre o título ou as linhas de cabeçalho e de dados.  
  
-   **Valores ausentes**. O driver do Excel lê um determinado número de linhas (por padrão, 8 linhas) na fonte especificada para determinar o tipo de dados de cada coluna. Quando uma coluna parece conter tipos de dados mistos, especialmente dados numéricos combinados com dados de texto, o driver decide em favor do tipo de dados majoritário e retorna valores nulos para as células que contêm dados de outro tipo. (Em uma ligação, o tipo numérico vence.) A maioria das opções de formatação de células na planilha de trabalho do Excel não parece afetar a determinação desse tipo de dados. Você pode modificar esse comportamento de driver do Excel especificando Modo de Importação. Para especificar Modo de Importação, adicione **IMEX=1** ao valor de Propriedades Estendidas na cadeia de conexão do gerenciador de conexões do Excel na janela **Propriedades** . Para obter mais informações, consulte [PRB: valores do Excel retornados como NULOS usando DAO OpenRecordset](http://support.microsoft.com/kb/194124).  
  
-   **Texto truncado**. Quando o driver determina que uma coluna do Excel contém dados de texto, ele seleciona o tipo de dados (cadeia ou memorando) com base no valor mais longo que ele obtém. Se o driver não descobre nenhum valor maior que 255 caracteres nas linhas que ele verifica, ele trata a coluna como uma coluna de cadeia de 255 caracteres, não como uma coluna de memorando. Assim, valores com mais de 255 caracteres podem estar truncados. Para importar dados de uma coluna de memorando sem que haja truncamento, você deve certificar-se de que essa coluna, em pelo menos uma das linhas de amostra, contenha um valor com mais 255 caracteres ou deve aumentar o número de linhas de amostra pelo driver para incluir esse tipo de linha. Você pode aumentar o número de linhas de amostra aumentando o valor de **TypeGuessRows** na chave do Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** . Para obter mais informações, consulte [PRB: a transferência de dados da fonte Jet 4.0 OLEDB falha com erro](http://support.microsoft.com/kb/281517).  
  
-   **Tipos de dados**. O driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Por exemplo, todas as colunas numéricas são interpretadas como duplas (DT_R8) e todas as colunas de cadeia de caracteres (que não sejam colunas de memorando) são interpretadas como cadeias Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mapeia os tipos de dados do Excel da seguinte maneira:  
  
    -   Numérico – flutuante de precisão dupla (DT_R8)  
  
    -   Moeda – moeda (DT_CY)  
  
    -   Booliano - booliano (DT_BOOL)  
  
    -   Data/hora – **datetime** (DT_DATE)  
  
    -   Cadeia – cadeia Unicode, 255 de comprimento (DT_WSTR)  
  
    -   Memorando – fluxo de texto Unicode (DT_NTEXT)  
  
-   **Conversões de tipo e comprimento de dados**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não converte tipos de dados implicitamente. Como resultado, você pode precisar usar as transformações Coluna Derivada ou Conversão de Dados para converter explicitamente dados do Excel antes de carregá-los em um destino que não seja Excel ou para converter dados que não sejam do Excel antes de carregá-los em um destino Excel. Nesse caso, pode ser útil criar o pacote inicial usando o Assistente de Importação e Exportação, que configura as conversões necessárias. Alguns exemplos de conversões que podem ser necessárias incluem:  
  
    -   Conversão entre colunas de cadeias Unicode e não Unicode do Excel com páginas de código específicas  
  
    -   Conversão entre colunas de cadeias de 255 caracteres e de comprimentos diferentes do Excel  
  
    -   Conversão entre colunas numéricas de precisão dupla e de outros tipos de colunas numéricas do Excel  
  
## <a name="excel-source-configuration"></a>Configuração da origem do Excel  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para obter informações sobre loop através de um grupo de arquivos do Excel, consulte [Loop por meio de arquivos do Excel e tabelas usando um contêiner de Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Mapear parâmetros de consulta para variáveis em um componente de fluxo de dados](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Loop através de arquivos e tabelas do Excel por meio de um contêiner do Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Editor de Origem do Excel (página Gerenciador de Conexões)
  Use o nó **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel** para selecionar a pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] para a origem que será usada. A origem do Excel lê os dados de uma planilha ou intervalo nomeado em uma pasta de trabalho existente.  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** da origem do Excel não está disponível no **Editor de Origem do Excel**, mas ela pode ser definida usando o **Editor Avançado**. Para obter mais informações sobre esta propriedade, consulte a seção Origem do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Valor|Description|  
|-----------|-----------------|  
|Tabela ou exibição|Recupere dados de uma planilha ou intervalo nomeado no arquivo do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas:** [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Recupere os dados do arquivo do Excel usando uma consulta SQL. |  
|Comando SQL a partir da variável|Especifique o texto da consulta SQL em uma variável.|  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Exibição de Dados** . A visualização pode exibir até 200 linhas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na pasta de trabalho do Excel.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Insira o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou procure o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Parâmetros**  
 Se você inseriu uma consulta parametrizada usando ? como um espaço reservado para o parâmetro no texto da consulta, use a caixa de diálogo **Definir Parâmetros da Consulta** para mapear os parâmetros de entrada da consulta para as variáveis do pacote.  
  
 **Build query**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar consulta**  
 Verifique a sintaxe do texto da consulta.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acesso aos dados = Comando SQL a partir da variável  
 **Nome da variável**  
 Selecione a variável que contém o texto da consulta SQL.  
  
## <a name="excel-source-editor-columns-page"></a>Editor de Origem do Excel (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem do Excel** para mapear uma coluna de saída para cada coluna externa (origem).  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas.  
  
 **Coluna Externa**  
 Exiba as colunas externas (fonte) na ordem em que serão lidas pela tarefa. Você pode alterar essa ordem desmarcando as colunas selecionadas na tabela discutida acima e selecionando colunas externas da lista em uma ordem diferente.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="excel-source-editor-error-output-page"></a>Editor de Origem do Excel (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem do Excel** para selecionar opções de tratamento de erro e definir propriedades em colunas de saída de erros.  
  
### <a name="options"></a>Opções  
 **Entrada ou Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Veja as colunas externas (origem) que você selecionou na página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="related-content"></a>Conteúdo relacionado  
[Carregar dados do ou para o Excel com o SSIS (SQL Server Integration Services)](../load-data-to-from-excel-with-ssis.md)
[Destino do Excel](excel-destination.md)  
[Gerenciador de Conexões do Excel](../connection-manager/excel-connection-manager.md)
