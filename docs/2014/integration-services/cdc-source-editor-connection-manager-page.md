---
title: Editor de origem CDC (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f60c9562a611ca3f396456abd80fb65c4fb5a99a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006160"
---
# <a name="cdc-source-editor-connection-manager-page"></a>Editor de Origem CDC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem CDC** para selecionar o gerenciador de conexões do ADO.NET para o banco de dados do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] do qual a origem CDC lê as linhas de alteração (o banco de dados CDC). Quando o banco de dados CDC é selecionado, você precisa selecionar uma tabela capturada no banco de dados.  
  
 Para obter mais informações sobre a origem CDC, consulte [Origem CDC](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página do Gerenciador de Conexões do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Gerenciador de Conexões**.  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões ADO.NET**  
 Selecione na lista um gerenciador de conexões existente ou clique em **Novo** para criar uma nova conexão. A conexão deve ser a um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que está habilitado para CDC e onde a tabela de alteração selecionada está localizada.  
  
 **Nova**  
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
 Selecione a variável de pacote de cadeia de caracteres SSIS que mantém o estado CDC para o contexto CDC atual. Para obter mais informações sobre a variável de estado CDC, consulte [Definir uma variável de estado](data-flow/define-a-state-variable.md).  
  
 **Incluir coluna de indicador de reprocessamento**  
 Marque esta caixa de seleção para criar uma coluna de saída especial chamada **__$reprocessing**.  
  
 Esta coluna apresenta um valor de **true** quando o intervalo de processamento CDC sobrepõe o intervalo de processamento inicial (o intervalo de LSNs que corresponde ao período de carga inicial) ou quando um intervalo de processamento CDC é reprocessado após um erro em uma execução anterior. Esta coluna de indicador permite que o desenvolvedor do SSIS trate erros diferentemente ao reprocessar alterações (por exemplo, ações como excluir de uma linha não existente e uma inserção com falha em uma chave duplicada podem ser ignoradas).  
  
 Para obter mais informações, consulte [Propriedades personalizadas da origem CDC](data-flow/cdc-source-custom-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Editor de origem CDC &#40;página colunas&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [Editor de origem CDC &#40;página de saída de erro&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  