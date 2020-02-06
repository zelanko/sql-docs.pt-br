---
title: Origem CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsource.f1
- sql13.ssis.designer.cdcsource.connection.f1
- sql13.ssis.designer.cdcsource.columns.f1
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 668b7343ae893d302a27c0a68aec58e536cffcc9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293275"
---
# <a name="cdc-source"></a>Origem CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A origem CDC lê um intervalo de dados de alteração de tabelas de alteração do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e entrega o downstream de alterações a outros SSIS componentes.  
  
 O intervalo de leitura de dados de alteração pela origem CDC é chamado Intervalo de Processamento CDC e é determinado pela tarefa Controle de CDC que é executada antes do início do fluxo de dados atual. O Intervalo de Processamento CDC é derivado do valor de uma variável de pacote que mantém o estado do processamento CDC para um grupo de tabelas.  
  
 A origem CDC extrai dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma tabela de banco de dados, uma exibição ou uma instrução SQL.  
  
 A origem CDC usa as configurações seguintes:  
  
-   Um gerenciador de conexões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET para acessar o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Para obter mais informações sobre como configurar a conexão de origem CDC, consulte [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).  
  
-   Uma tabela habilitada para CDC.  
  
-   O nome da instância de captura da tabela selecionada (se houver mais de uma).  
  
-   O modo de processamento de alteração.  
  
-   O nome da variável de pacote do estado CDC com base no qual o intervalo de Processamento CDC é determinado. A origem CDC não modifica essa variável.  
  
 Os dados retornados pela Origem CDC são iguais aos retornados pelas funções do CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**cdc.fn_cdc_get_all_changes_\<capture-instance-name>** ou **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** (quando disponível). A única adição opcional é a coluna, **__$initial_processing** , que indica se o intervalo de processamento atual pode se sobrepor a uma carga inicial da tabela. Para obter mais informações sobre o processamento inicial, consulte [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md).  
  
 A origem CDC tem uma saída regular e uma saída de erro.  
  
## <a name="error-handling"></a>Tratamento de erros  
 A origem CDC tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: o valor sempre é -1.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   **Colunas de Linha de Erro**: os dados de registro que causam o erro.  
  
 Dependendo da configuração de comportamento de erro, a origem CDC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro.  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 O componente origem CDC para Microsoft oferece suporte a todos os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão mapeados para os tipos de dados SSIS corretos.  
  
## <a name="troubleshooting-the-cdc-source"></a>Solucionando problemas da origem CDC  
 A seguir são apresentadas informações sobre como solucionar problemas de origem CDC.  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>Use este script para isolar problemas e reproduzi-los no SQL Server Management Studio  
 Uma operação de origem CDC é governada pela operação da tarefa Controle CDC executada antes da chamada à origem CDC. A tarefa Controle CDC prepara o valor da variável de pacote do estado CDC para conter LSNs de início e término. Ela executa uma função equivalente ao seguinte script:  
  
```sql
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 onde:  
  
-   \<cdc-enabled-database-name> é o nome do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém as tabelas de alterações.  
  
-   \<value-from-state-cs> é o valor que aparece na variável de estado CDC como CS/\<value-from-state-cs>/ (CS significa Current-processing-range-Start, início atual do intervalo de processamento).  
  
-   \<value-from-state-ce> é o valor que aparece na variável de estado CDC, como em CE/\<value-from-state-cs>/ (CE significa Current-processing-range-End).  
  
-   \<mode> corresponde aos modos de processamento CDC. Os modos de processamento têm um dos seguintes valores: **Tudo**, **Tudo com Valores Antigos**, **Rede**, **Rede com Máscara de Atualização**, **Rede com Mesclagem**.  
  
 Este script ajuda a isolar problemas reproduzindo-os no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], onde é fácil reproduzir e identificar erros.  
  
#### <a name="sql-server-error-message"></a>Mensagem de erro do SQL Server  
 A mensagem seguinte poderá ser retornada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 **Um número insuficiente de argumentos foram fornecidos ao procedimento ou função cdc.fn_cdc_get_net_changes_\<..>.**  
  
 Esse erro não indica que um argumento está faltando. Significa que os valores de LSN de início ou fim na variável de estado CDC são inválidos.  
  
## <a name="configuring-the-cdc-source"></a>Configurando a origem CDC  
 Você pode configurar a origem CDC programaticamente ou por meio do SSIS Designer.  
  
 Para obter mais informações, consulte um dos tópicos a seguir.  
  
-   [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [Editor de Origem CDC &#40;página Colunas&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse na origem CDC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** , consulte [CDC Source Custom Properties](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Propriedades personalizadas da origem CDC](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [Extrair dados de alteração por meio da origem CDC](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="cdc-source-editor-connection-manager-page"></a>Editor de Origem CDC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem CDC** para selecionar o gerenciador de conexões do ADO.NET para o banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do qual a origem CDC lê as linhas de alteração (o banco de dados CDC). Quando o banco de dados CDC é selecionado, você precisa selecionar uma tabela capturada no banco de dados.  
  
 Para obter mais informações sobre a origem CDC, consulte [Origem CDC](../../integration-services/data-flow/cdc-source.md).  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página do Gerenciador de Conexões do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Gerenciador de Conexões**.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões ADO.NET**  
 Selecione na lista um gerenciador de conexões existente ou clique em **Novo** para criar uma nova conexão. A conexão deve ser a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está habilitado para CDC e onde a tabela de alteração selecionada está localizada.  
  
 **Novo**  
 Clique em **Nova**. A caixa de diálogo **Configurar Editor do Gerenciador de Conexões ADO.NET** é aberta, na qual você pode criar um novo gerenciador de conexões  
  
 **Tabela CDC**  
 Selecione a tabela de origem CDC que contém as alterações capturadas que você deseja ler e alimente os componentes SSIS downstream para serem processados.  
  
 **Instância de captura**  
 Selecione ou digite o nome da instância de captura CDC com a tabela CDC que deve ser lida.  
  
 Uma tabela de origem capturada pode ter uma ou duas instâncias capturadas para tratar diretamente a transição da definição de tabela por meio de alterações de esquema. Se mais de uma instância de captura for definida para a tabela de origem que está sendo capturada, selecione a instância de captura que você deseja usar aqui. O nome padrão da instância de captura para uma tabela [esquema].[tabela] é \<esquema>_\<tabela>, mas os nomes reais da instância de captura em uso podem ser diferentes. A tabela da qual a leitura é realmente realizada é a tabela CDC **cdc.\<instância-de-captura>_CT**.  
  
 **Modo de processamento CDC**  
 Selecione o modo de processamento que melhor trata suas necessidades de processamento. As opções possíveis são:  
  
-   **Tudo**: retorna as alterações no intervalo CDC atual sem os valores **Antes da Atualização** .  
  
-   **Todos com valores antigos**: retorna as alterações no intervalo de processamento CDC atual, incluindo os valores antigos (**Antes da Atualização**). Para cada operação de atualização, haverá duas linhas, uma com os valores antes da atualização e outra com o valor depois da atualização.  
  
-   **Líquido**: retorna somente uma linha de alteração por linha de origem modificada no intervalo de processamento CDC atual. Se uma linha de origem tiver sido atualizada várias vezes, a alteração combinada será gerada (por exemplo, insert+update é gerado como uma única atualização e update+delete é gerado como uma única exclusão). Ao trabalhar em modo de processamento de alteração Líquido, é possível dividir as alterações para saídas Excluir, Inserir e Atualizar, e tratá-las em paralelo porque a única linha de origem aparece em mais de uma saída.  
  
-   **Líquido com máscara atualizada**: este modo é semelhante ao modo Líquido normal, mas também adiciona colunas boolianas com o nome padrão **__$\<nome-da-coluna>\__Changed**, que indica as colunas alteradas na linha de alteração atual.  
  
-   **Líquido com mesclagem**: este modo é semelhante ao modo Líquido normal, mas com operações de inserção e atualização mescladas em uma única operação de mesclagem (UPSERT).  
  
> [!NOTE]  
>  Para todas as opções de alteração Net, a tabela de origem deve ter uma chave primária ou índice exclusivo. Para tabelas sem uma chave primária ou um índice exclusivo, você deve use a opção **Tudo** .  
  
 **Variável contendo o estado de CDC**  
 Selecione a variável de pacote de cadeia de caracteres SSIS que mantém o estado CDC para o contexto CDC atual. Para obter mais informações sobre a variável de estado CDC, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
 **Incluir coluna de indicador de reprocessamento**  
 Marque esta caixa de seleção para criar uma coluna de saída especial chamada **__$reprocessing**.  
  
 Esta coluna apresenta um valor de **true** quando o intervalo de processamento CDC sobrepõe o intervalo de processamento inicial (o intervalo de LSNs que corresponde ao período de carga inicial) ou quando um intervalo de processamento CDC é reprocessado após um erro em uma execução anterior. Esta coluna de indicador permite que o desenvolvedor do SSIS trate erros diferentemente ao reprocessar alterações (por exemplo, ações como excluir de uma linha não existente e uma inserção com falha em uma chave duplicada podem ser ignoradas).  
  
 Para obter mais informações, consulte [Propriedades personalizadas da origem CDC](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
## <a name="cdc-source-editor-columns-page"></a>Editor de Origem CDC (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem CDC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Colunas**.  
  
### <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecione as colunas a serem usadas na origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna Externa**  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem CDC. Para alterar essa ordem, primeiro limpe as colunas selecionadas na lista **Colunas Externas Disponíveis** e depois selecione colunas externas na lista em uma ordem diferente. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna de Saída**  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## <a name="cdc-source-editor-error-output-page"></a>Editor de Origem CDC (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem CDC** para selecionar as opções para tratamento de erros.  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Saída de Erro do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Saída de Erro**.  
  
### <a name="options"></a>Opções  
 **Entrada/Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) selecionadas na página **Gerenciador de Conexões** da caixa de diálogo **CDC Source Editor (Editor de Origem CDC)** .  
  
 **Erro**  
 Selecione como a origem CDC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Truncation**  
 Selecione como a origem CDC deve tratar o truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
 **Descrição**  
 Não usado.  
  
 **Definir este valor para células selecionadas**  
 Selecione como a origem CDC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
### <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como a origem CDC trata erros e truncamentos.  
  
 **Falha no Componente**  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
 **Ignorar Falha**  
 O erro ou truncamento é ignorado e a linha de dados é direcionada para a saída da origem CDC.  
  
 **Redirecionar fluxo**  
 O erro ou a linha de dados de truncamento é direcionada para a saída do erro da origem CDC. Neste caso, o tratamento de erro da origem CDC é usado. Para obter mais informações, consulte [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Modos de processamento para a origem de CDC](https://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/), em mattmasson.com.  
  
  
