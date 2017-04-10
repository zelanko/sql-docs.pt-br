---
title: "Extrair dados de altera&#231;&#227;o por meio da origem CDC | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Extrair dados de altera&#231;&#227;o por meio da origem CDC
  Para adicionar e configurar uma origem de CDC, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma tarefa Controle de CDC.  
  
 Para obter mais informações sobre a tarefa Controle de CDC, consulte [Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task.md).  
  
 Para obter mais informações sobre a origem CDC, consulte [Origem CDC](../../integration-services/data-flow/cdc-source.md).  
  
### Para extrair dados usando uma origem CDC  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a origem CDC para a superfície de design.  
  
4.  Clique duas vezes na origem CDC.  
  
5.  Na caixa de diálogo **Editor de Origem de CDC**, na página **Gerenciador de Conexões**, selecione um gerenciador de conexões ADO.NET na lista ou clique em **Novo** para criar uma nova conexão. A conexão deve ser estabelecida com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém as tabelas de alteração a serem lidas.  
  
6.  Selecione a **tabela CDC** em que você quer processar alterações.  
  
7.  Selecione ou digite o nome da **instância de captura CDC** com a tabela CDC que deve ser lida.  
  
     Uma tabela de origem capturada pode ter uma ou duas instâncias capturadas para tratar diretamente a transição da definição de tabela por meio de alterações de esquema. Se mais de uma instância de captura for definida para a tabela de origem que está sendo capturada, selecione a instância de captura que você deseja usar aqui. O nome padrão da instância de captura para uma tabela [schema].[table] é \<esquema>_\<tabela>, mas os nomes reais da instância de captura em uso podem ser diferentes. A tabela real da qual é lida é a tabela CDC **cdc .\<instância-de-captura>_CT**.  
  
8.  Selecione o modo de processamento que melhor trata suas necessidades de processamento. As opções possíveis são:  
  
    -   **Tudo**: retorna as alterações no intervalo CDC atual sem os valores **Antes da Atualização**.  
  
    -   **Todos com valores antigos**: retorna as alterações no intervalo de processamento CDC atual, incluindo os valores antigos (**Antes da Atualização**). Para cada operação de atualização, haverá duas linhas, uma com os valores antes da atualização e outra com o valor depois da atualização.  
  
    -   **Líquido**: retorna somente uma linha de alteração por linha de origem modificada no intervalo de processamento CDC atual. Se uma linha de origem tiver sido atualizada várias vezes, a alteração combinada será gerada (por exemplo, insert+update é gerado como uma única atualização e update+delete é gerado como uma única exclusão). Ao trabalhar em modo de processamento de alteração Líquido, é possível dividir as alterações para saídas Excluir, Inserir e Atualizar, e tratá-las em paralelo porque a única linha de origem aparece em mais de uma saída.  
  
    -   **Líquido com máscara atualizada**: este modo é semelhante ao modo Líquido normal, mas também adiciona colunas boolianas com o nome padrão **__$\<column-name>\__Changed**, que indica as colunas alteradas na linha de alteração atual.  
  
    -   **Líquido com mesclagem**: este modo é semelhante ao modo Líquido normal, mas com operações de inserção e atualização mescladas em uma única operação de mesclagem (UPSERT).  
  
9. Selecione a variável de pacote de cadeia de caracteres SSIS que mantém o estado CDC para o contexto CDC atual. Para obter mais informações sobre a variável de estado CDC, consulte [Definir uma variável de estado](../../integration-services/data-flow/define-a-state-variable.md).  
  
10. Marque esta caixa de seleção **Incluir coluna do indicador de reprocessamento** para criar uma coluna de saída especial chamada **__$reprocessing**. Esta coluna apresenta um valor de **true** quando o intervalo de processamento CDC sobrepõe o intervalo de processamento inicial (o intervalo de LSNs que corresponde ao período de carga inicial) ou quando um intervalo de processamento CDC é reprocessado após um erro em uma execução anterior. Esta coluna de indicador permite que o desenvolvedor do SSIS trate erros diferentemente ao reprocessar alterações (por exemplo, ações como excluir de uma linha não existente e uma inserção com falha em uma chave duplicada podem ser ignoradas).  
  
     Para obter mais informações, consulte [Propriedades personalizadas da origem CDC](../../integration-services/data-flow/cdc-source-custom-properties.md).  
  
11. Para atualizar o mapeamento entre colunas externas e de saída, clique em **Colunas** e selecione colunas diferentes na lista **Coluna Externa** .  
  
12. Opcionalmente, atualize os valores das colunas de saída excluindo os valores na lista **Coluna de Saída**.  
  
13. Para configurar a saída de erro, clique em **Saída de Erro**.  
  
14. É possível clicar em **Visualizar** para exibir até 200 linhas dos dados extraídos pela origem CDC.  
  
15. Clique em **OK**.  
  
## Consulte também  
 [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [Editor de Origem CDC &#40;página Colunas&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  