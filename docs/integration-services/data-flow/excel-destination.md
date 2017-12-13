---
title: Destino do Excel | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
caps.latest.revision: "49"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3ee5bd643443aca136883e94a768fca60960c869
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="excel-destination"></a>Destino do Excel
  O destino do Excel carrega dados em planilhas ou intervalos em pastas de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
## <a name="access-modes"></a>Modos de acesso  
 O destino do Excel fornece três modos de acesso diferentes para carregar dados:  
  
-   Uma tabela ou exibição.  
  
-   Uma tabela ou exibição especificada em uma variável.  
  
-   Os resultados de uma instrução SQL. A consulta pode ser uma consulta parametrizada.  
  
> [!IMPORTANT]  
>  No Excel, uma planilha de trabalho ou intervalo é equivalente a uma tabela ou exibição. As listas de tabelas disponíveis nos Editores de Origem e Destino do Excel exibem somente planilhas existentes (identificadas pelo sinal $ anexado ao nome da planilha, por exemplo, Planilha1$) e os intervalos nomeados (identificados pela ausência desse sinal $, como MyRange).  
  
## <a name="usage-considerations"></a>Considerações de uso  
 O Gerenciador de Conexões do Excel usa o Provedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Jet 4.0 e driver ISAM do Excel com suporte para se conectar, além de ler e gravar dados nas fontes de dados do Excel.  
  
 Muitos artigos da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../includes/msconame-md.md)] documentam o comportamento desse provedor e driver e, embora esses artigos não sejam específicos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou de seus serviços de transformação de dados anteriores, talvez você queira obter mais informações sobre determinados comportamentos que podem levar a resultados inesperados. Para obter informações gerais sobre o uso e comportamento do driver do Excel, consulte [Como usar ADO com dados do Excel do Visual Basic ou do VBA](http://support.microsoft.com/kb/257819).  
  
 Os seguintes comportamentos do provedor Jet que está incluído no driver do Excel podem levar a resultados inesperados ao salvar dados em um destino do Excel.  
  
-   **Salvando dados de texto**. Quando o driver do Excel salva valores de dados de texto em um destino do Excel, o driver coloca aspas simples (') antes do texto de cada célula para garantir que os valores salvos serão interpretados como texto. Se você tem ou desenvolve outros aplicativos que leem ou processam os dados salvos, será necessário incluir um tratamento especial para as aspas simples que precedem cada texto.  
  
     Para obter informações sobre como evitar incluir aspas simples, consulte esta postagem no blog, [Aspas simples são acrescentadas a todas as cadeias de caracteres quando os dados são transformados para Excel ao usar o componente de fluxo de dados de destino do Excel no pacote SSIS](http://go.microsoft.com/fwlink/?LinkId=400876), no msdn.com.  
  
-   **Salvando dados de memorando (ntext)**. Antes de salvar com sucesso cadeias de caracteres com mais de 255 caracteres em uma coluna do Excel, o driver deve reconhecer o tipo de dados da coluna de destino como **memorando** e não como **cadeia de caracteres**. Se a tabela de destino já contém linhas de dados, então as primeiras linhas que serão amostradas pelo driver devem conter pelo menos uma instância com um valor maior que 255 caracteres na coluna de memorando. Se a tabela de destino for criada durante o desenvolvimento do pacote ou em tempo de execução, a instrução CREATE TABLE deve usar o tipo de dados LONGTEXT (ou um de seus sinônimos) para a coluna de memorando.  
  
-   **Tipos de dados**. O driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Por exemplo, todas as colunas numéricas são interpretadas como duplas (DT_R8) e todas as colunas de cadeia de caracteres (que não sejam colunas de memorando) são interpretadas como cadeias Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mapeia os tipos de dados do Excel da seguinte maneira:  
  
    -   Numérico    flutuante de precisão dupla (DT_R8)  
  
    -   Moeda     moeda (DT_CY)  
  
    -   Booliano     booliano (DT_BOOL)  
  
    -   Data/hora     **datetime** (DT_DATE)  
  
    -   Cadeia de caracteres     cadeia de caracteres Unicode com 255 caracteres (DT_WSTR)  
  
    -   Memorando     fluxo de texto Unicode (DT_NTEXT)  
  
-   **Conversões de tipo e comprimento de dados**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não converte tipos de dados implicitamente. Como resultado, talvez seja necessário usar as transformações Coluna Derivada ou Conversão de Dados para converter explicitamente os dados do Excel antes de carregá-los em um destino que não seja Excel ou para converter dados que não sejam do Excel antes de carregá-los em um destino do Excel. Nesse caso, pode ser útil criar o pacote inicial usando o Assistente de Importação e Exportação, que configura as conversões necessárias. Alguns exemplos de conversões que podem ser necessárias incluem:  
  
    -   Conversão entre colunas de cadeia de caracteres Unicode e não Unicode do Excel com páginas de código específicas.  
  
    -   Conversão entre colunas de cadeia de 255 caracteres e de comprimentos diferentes do Excel.  
  
    -   Conversão entre colunas numéricas de precisão dupla e outros tipos de colunas numéricas do Excel.  
  
## <a name="configuration-of-the-excel-destination"></a>Configuração do destino do Excel  
 O destino do Excel usa um gerenciador de conexões do Excel para se conectar a uma fonte de dados e o gerenciador de conexões especifica o arquivo de pasta de trabalho a ser usado. Para obter mais informações, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 O destino do Excel tem uma entrada regular e uma saída de erro.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete todas as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas do Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para obter mais informações sobre como definir as propriedades, consulte [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
-   [Conectar-se a uma pasta de trabalho do Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
-   [Loop através de arquivos e tabelas do Excel por meio de um contêiner Loop Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Excel no Integration Services, Parte 1 de 3: conexões e componentes](http://go.microsoft.com/fwlink/?LinkId=217674), em dougbert.com  
  
-   Entrada de blog, [Excel no Integration Services, Parte 2 de 3: tabelas e tipos de dados](http://go.microsoft.com/fwlink/?LinkId=217675), em dougbert.com.  
  
-   Entrada de blog, [O Excel no Integration Services, parte 3 de 3: problemas e alternativas](http://go.microsoft.com/fwlink/?LinkId=217676), no site dougbert.com.  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Editor de Destinos do Excel (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos do Excel** para especificar informações da fonte de dados e visualizar os resultados. O destino do Excel carrega dados em uma planilha ou um intervalo nomeado em uma pasta de trabalho do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  A propriedade **CommandTimeout** do destino do Excel não está disponível no **Editor de Destinos do Excel**, mas pode ser definida com o **Editor Avançado**. Além disso, determinadas opções de carregamento rápido só estarão disponíveis no **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Destino do Excel em [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Gerenciador de conexões do Excel**  
 Selecione um gerenciador de conexões do Excel existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões usando a caixa de diálogo **Gerenciador de Conexões do Excel** .  
  
 **Modo de acesso aos dados**  
 Especifique o método para selecionar os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|Tabela ou exibição|Carregue dados em uma planilha ou intervalo nomeado na fonte de dados do Excel.|  
|Nome da tabela ou variável do nome de exibição|Especifique a planilha ou o nome do intervalo em uma variável.<br /><br /> **Informações relacionadas**: [Usar variáveis em pacotes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Carregue dados no destino do Excel usando uma consulta SQL.|  
  
 **Nome da planilha do Excel**  
 Selecione o destino do Excel da listagem suspensa. Se a lista estiver vazia, clique em **Novo**.  
  
 **Nova**  
 Clique em **Novo** para iniciar a caixa de diálogo **Criar Tabela** . Quando você clicar em **OK**, a caixa de diálogo cria o arquivo Excel para o qual o **Gerenciador de Conexões do Excel** aponta.  
  
 **Exibir dados existentes**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
> [!WARNING]  
>  Se o **Gerenciador de conexões do Excel** que você selecionou apontar para um arquivo do Excel que não existe, você verá uma mensagem de erro ao clicar neste botão.  
  
### <a name="data-access-mode-dynamic-options"></a>Opções dinâmicas de modo de acesso aos dados  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acesso aos dados = Tabela ou exibição  
 **Nome da planilha do Excel**  
 Selecione o nome da planilha ou o intervalo nomeado na lista disponível na fonte de dados.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acesso aos dados = Variável do nome da tabela ou do nome de exibição  
 **Nome da variável**  
 Selecione a variável que contém o nome da planilha ou do intervalo nomeado.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acesso aos dados = Comando SQL  
 **Texto do comando SQL**  
 Digite o texto de uma consulta SQL, crie a consulta clicando em **Construir Consulta**ou localize o arquivo que contém o texto da consulta clicando em **Procurar**.  
  
 **Construir Consulta**  
 Use a caixa de diálogo **Construtor de Consultas** para construir a consulta SQL visualmente.  
  
 **Procurar**  
 Use a caixa de diálogo **Abrir** para localizar o arquivo com contém o texto da consulta SQL.  
  
 **Analisar Consulta**  
 Verifique a sintaxe do texto da consulta.  
  
## <a name="excel-destination-editor-mappings-page"></a>Editor de Destino do Excel (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo do **Editor de Destinos do Excel** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. Use uma operação de arrastar e soltar para mapear colunas de entrada disponíveis na tabela para as colunas de destino.  
  
 **Colunas de Destino Disponíveis**  
 Exiba a lista de colunas de destino disponíveis. Use uma operação de arrastar e soltar para mapear as colunas de destino disponíveis na tabela para as colunas de entrada.  
  
 **Coluna de Entrada**  
 Exibir colunas de entrada selecionadas na tabela acima. É possível alterar os mapeamentos usando a lista **Colunas de Entrada Disponíveis**.  
  
 **Coluna de Destino**  
 Exiba cada coluna de destino disponível, seja ela mapeada ou não.  
  
## <a name="excel-destination-editor-error-output-page"></a>Editor de Destino do Excel (página Saída de Erro)
  Use a página **Avançado** da caixa de diálogo **Editor de Destinos do Excel** para especificar opções de tratamento de erro.  
  
### <a name="options"></a>Opções  
 **Entrada ou Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Veja as colunas externas (origem) que você selecionou no nó **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem do Excel**.  
  
 **Erro**  
 Especifique o que deve acontecer quando ocorre um erro: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Tópicos Relacionados:** [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncation**  
 Especifique o que deve acontecer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou causar falha do componente.  
  
 **Description**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que deve acontecer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Origem do Excel](../../integration-services/data-flow/excel-source.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)   
 [Trabalhar com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
