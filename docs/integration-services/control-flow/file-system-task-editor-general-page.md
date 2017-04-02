---
title: "Editor da Tarefa Sistema de Arquivos (p&#225;gina Geral) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.filesystemtask.general.f1"
helpviewer_keywords: 
  - "Editor da Tarefa Sistema de Arquivos"
ms.assetid: 51fe6614-3418-4eff-a28d-02ea31cc9aa9
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Editor da Tarefa Sistema de Arquivos (p&#225;gina Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Sistema de Arquivos** para configurar a operação de sistema de arquivos que a tarefa executa.  
  
 Para obter informações sobre essa tarefa, consulte [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Você deve especificar um gerenciador de conexões de origem e destino, definindo as propriedades SourceConnection e DestinationConnection. Você pode fornecer os nomes dos gerenciadores de conexões de Arquivo que apontam para os arquivos que a tarefa usa como origem ou destino ou, se os caminhos dos arquivos estiverem armazenados em variáveis, fornecer os nomes das variáveis. Antes de usar variáveis para armazenar os caminhos de arquivo, defina as opções IsSourcePathVariable, para a conexão de origem, e IsDestinationPatheVariable, para a conexão de destino, como **True**. Em seguida, opte por utilizar as variáveis do sistema ou definidas pelo usuário existentes, ou então, crie novas variáveis. Na caixa de diálogo **Adicionar Variável** , é possível configurar e especificar o escopo das variáveis. O escopo deve ser a tarefa Sistema de Arquivos ou um contêiner pai. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](../Topic/Use%20Variables%20in%20Packages.md).  
  
> [!NOTE]  
>  Para anular as variáveis que você selecionou para as propriedades **SourceConnection** e **DestinationConnection** , insira uma expressão para as propriedades **Source** e **Destination** . Insira expressões na página **Expressões** do **Editor da Tarefa Sistema de Arquivos**. Por exemplo, para definir o caminho dos arquivos que a tarefa usa como um destino, você pode querer usar a variável A sob determinadas condições e usar a variável B sob outras condições.  
  
> [!NOTE]  
>  A tarefa Sistema de Arquivos funciona em um único arquivo ou diretório. Por isso, essa tarefa não dá suporte a uso de caracteres curingas para executar a mesma operação em vários arquivos ou diretórios. Para fazer com que uma tarefa Sistema de Arquivos repita uma operação em vários arquivos ou diretórios, coloque-a em um contêiner Loop Foreach. Para obter mais informações, consulte [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Você pode usar expressões para usar variáveis diferentes para o  
  
## Opções  
 **IsDestinationPathVariable**  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **DestinationConnection**será exibida.|  
  
 **OverwriteDestination**  
 Especifique se a operação pode substituir arquivos no diretório de destino.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Sistema de Arquivos. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Description**  
 Digite uma descrição para a tarefa Sistema de Arquivos.  
  
 **Operação**  
 Selecione a operação de sistema de arquivos a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Copiar diretório**|Copiar um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Copiar arquivo**|Copia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Criar diretório**|Cria um diretório. A seleção deste valor exibe as opções dinâmicas para um diretório de origem e destino.|  
|**Excluir diretório**|Exclui um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir conteúdo do diretório**|Exclui o conteúdo de um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir arquivo**|Exclui um arquivo. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Mover diretório**|Move um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Mover arquivo**|Move um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino. Ao mover um arquivo, não inclua um nome de arquivo no caminho de diretório que você fornecer como destino.|  
|**Renomear arquivo**|Renomeia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino. Ao renomear um arquivo, inclua o novo nome de arquivo no caminho de diretório que você fornecer para o destino.|  
|**Definir atributos**|Define os atributos de um arquivo ou diretório. A seleção desse valor exibe as opções dinâmicas para origem e operação.|  
  
 **IsSourcePathVariable**  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value||  
|-----------|-|  
|**True**|O caminho de destino é armazenado em uma variável. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
  
## Opções dinâmicas de IsDestinationPathVariable  
  
### IsDestinationPathVariable = True  
 **DestinationVariable**  
 Selecione o nome da variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](../Topic/Add%20Variable.md)  
  
### IsDestinationPathVariable = False  
 **DestinationConnection**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Opções dinâmicas de IsSourcePathVariable  
  
### IsSourcePathVariable = True  
 **SourceVariable**  
 Selecione o nome da variável na lista ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](../Topic/Add%20Variable.md)  
  
### IsSourcePathVariable = False  
 **SourceConnection**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Opções dinâmicas de operação  
  
### Operação = Definir atributos  
 **Oculto**  
 Indique se o arquivo ou diretório deve ficar visível.  
  
 **ReadOnly (somente-leitura)**  
 Indique se o arquivo é somente leitura.  
  
 **Archive**  
 Indique se o arquivo ou diretório está pronto para ser arquivado.  
  
 **Sistema**  
 Indique se o arquivo é um arquivo do sistema operacional.  
  
### Operação = Criar diretório  
 **UseDirectoryIfExists**  
 Indica se a operação **Criar diretório** usa um diretório existente com o nome especificado, em vez de criar um novo diretório.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  