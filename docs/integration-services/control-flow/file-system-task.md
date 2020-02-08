---
title: Tarefa do Sistema de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.filesystemtask.f1
- sql13.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f170a279f591b496b4c69cbb80b4c719954c30ba
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71294134"
---
# <a name="file-system-task"></a>Tarefa Sistema de Arquivos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A tarefa Sistema de Arquivos executa operações em arquivos e diretórios no sistema de arquivos. Por exemplo, ao usar a tarefa Sistema de Arquivos, um pacote pode criar, mover ou excluir diretórios e arquivos. Você também pode usar a tarefa Sistema de Arquivos para definir atributos em arquivos e diretórios. Por exemplo, a tarefa Sistema de Arquivos pode tornar os arquivos em ocultos ou somente leitura.  
  
 Todas as operações da tarefa Sistema de Arquivos usam uma origem, que pode ser um arquivo ou diretório. Por exemplo, o arquivo que a tarefa copia ou o diretório que ela exclui é uma origem. A origem pode ser especificada usando um gerenciador de conexões de arquivos que aponta para o diretório ou arquivo, ou fornecendo o nome de uma variável que contém o caminho de origem. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
 As operações que copiam e movem arquivos e diretórios e renomeiam arquivos usam um destino e uma origem. O destino é especificado usando um gerenciador de conexões de arquivo ou uma variável. As operações de tarefa do sistema de arquivos podem ser configuradas para permitir substituição de arquivos de destino e os diretórios. A operação que cria um diretório novo pode ser configurada para usar um diretório existente que tenha o nome especificado, em vez de haver uma falha quando já existir o diretório.  
  
## <a name="predefined-file-system-operations"></a>Operações do sistema de arquivos predefinidas  
 A tarefa Sistema de Arquivos inclui um conjunto predefinido de operações. A tabela a seguir descreve essas operações.  
  
|Operação|Descrição|  
|---------------|-----------------|  
|Copiar diretório|Copia uma pasta de um local para outro.|  
|Copiar arquivo|Copia um arquivo de um local para outro.|  
|Criar diretório|Cria uma pasta em um local especificado.|  
|Excluir diretório|Exclui uma pasta de um local especificado.|  
|Excluir conteúdo do diretório|Exclui todos os arquivos e pastas de uma pasta.|  
|Excluir arquivo|Exclui um arquivo de um local especificado.|  
|Mover diretório|Move uma pasta de um local para outro.|  
|Mover arquivo|Move um arquivo de um local para outro.|  
|Renomear arquivo|Renomeia um arquivo em um local especificado.|  
|Definir atributos|Define os atributos de arquivos e pastas. Os atributos incluem: Arquivo morto, Oculto, Normal, Somente Leitura e Sistema. Normal é a falta de atributos e não pode ser combinado com outros atributos. Todos os outros atributos podem ser usados em combinação.|  
  
 A tarefa Sistema de Arquivos funciona em um único arquivo ou diretório. Por isso, essa tarefa não dá suporte a uso de caracteres curingas para executar a mesma operação em vários arquivos. Para fazer uma tarefa Sistema de Arquivos repetir uma operação em vários arquivos ou diretórios, coloque a tarefa Sistema de Arquivos em um contêiner Loop Foreach, conforme descrito nas seguintes etapas:  
  
-   **Configurar o contêiner Loop Foreach** Na página **Coleção** do Editor de Loop Foreach, defina o enumerador como **Enumerador de Arquivo Foreach** e digite a expressão de caractere curinga, conforme a configuração do enumerador para **Arquivos**. Na página **Mapeamento de Variáveis** do Editor de Loop Foreach, mapeie uma variável que você deseja usar para passar os nomes de arquivos, um de cada vez, para a tarefa Sistema de Arquivos.  
  
-   **Adicionar e configurar uma tarefa Sistema de Arquivos** Adicionar uma tarefa Sistema de Arquivos ao contêiner Loop Foreach. Na página **Geral** do Editor da Tarefa Sistema de Arquivos, defina o **SourceVariable** ou a propriedade **DestinationVariable** para a variável que você definiu no contêiner Loop Foreach.  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>Entradas de log personalizadas disponíveis na tarefa Sistema de Arquivos  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Sistema de Arquivos. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**FileSystemOperation**|Informa a operação executada pela tarefa. A entrada de log é gravada quando a operação de sistema de arquivos é iniciada e inclui informações sobre a origem e o destino.|  
  
## <a name="configuring-the-file-system-task"></a>Configurando a tarefa Arquivo de Sistemas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte os tópicos a seguir:  
  
-   [Editor da Tarefa Sistema de Arquivos &#40;Página Geral&#41;](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte o tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte o tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui uma tarefa que faz downloads e uploads de arquivos de dados e gerencia diretórios em servidores. Para obter mais informações, consulte [FTP Task](../../integration-services/control-flow/ftp-task.md).  
  
## <a name="file-system-task-editor-general-page"></a>Editor da Tarefa Sistema de Arquivos (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa Sistema de Arquivos** para configurar a operação de sistema de arquivos que a tarefa executa.  
  
 Você deve especificar um gerenciador de conexões de origem e destino, definindo as propriedades SourceConnection e DestinationConnection. Você pode fornecer os nomes dos gerenciadores de conexões de Arquivo que apontam para os arquivos que a tarefa usa como origem ou destino ou, se os caminhos dos arquivos estiverem armazenados em variáveis, fornecer os nomes das variáveis. Antes de usar variáveis para armazenar os caminhos de arquivo, defina as opções IsSourcePathVariable, para a conexão de origem, e IsDestinationPatheVariable, para a conexão de destino, como **True**. Em seguida, opte por utilizar as variáveis do sistema ou definidas pelo usuário existentes, ou então, crie novas variáveis. Na caixa de diálogo **Adicionar Variável** , é possível configurar e especificar o escopo das variáveis. O escopo deve ser a tarefa Sistema de Arquivos ou um contêiner pai. Para obter mais informações, consulte [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Usar variáveis em pacotes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
> [!NOTE]  
>  Para anular as variáveis que você selecionou para as propriedades **SourceConnection** e **DestinationConnection** , insira uma expressão para as propriedades **Source** e **Destination** . Insira expressões na página **Expressões** do **Editor da Tarefa Sistema de Arquivos**. Por exemplo, para definir o caminho dos arquivos que a tarefa usa como um destino, você pode querer usar a variável A sob determinadas condições e usar a variável B sob outras condições.  
  
> [!NOTE]  
>  A tarefa Sistema de Arquivos funciona em um único arquivo ou diretório. Por isso, essa tarefa não dá suporte a uso de caracteres curingas para executar a mesma operação em vários arquivos ou diretórios. Para fazer com que uma tarefa Sistema de Arquivos repita uma operação em vários arquivos ou diretórios, coloque-a em um contêiner Loop Foreach. Para obter mais informações, consulte [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Você pode usar expressões para usar variáveis diferentes para o  
  
### <a name="options"></a>Opções  
 **IsDestinationPathVariable**  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **DestinationConnection**será exibida.|  
  
 **OverwriteDestination**  
 Especifique se a operação pode substituir arquivos no diretório de destino.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Sistema de Arquivos. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Sistema de Arquivos.  
  
 **Operação**  
 Selecione a operação de sistema de arquivos a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Copiar diretório**|Copiar um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Copiar arquivo**|Copia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Criar diretório**|Criar um diretório. A seleção deste valor exibe as opções dinâmicas para um diretório de origem e destino.|  
|**Excluir diretório**|Exclui um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir conteúdo do diretório**|Exclui o conteúdo de um diretório. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Excluir arquivo**|Exclui um arquivo. A seleção desse valor exibe as opções dinâmicas para a origem.|  
|**Mover diretório**|Move um diretório. A seleção desse valor exibe as opções dinâmicas para origem e destino.|  
|**Mover arquivo**|Move um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino. Ao mover um arquivo, não inclua um nome de arquivo no caminho de diretório que você fornecer como destino.|  
|**Renomear arquivo**|Renomeia um arquivo. A seleção desse valor exibe as opções dinâmicas para origem e destino. Ao renomear um arquivo, inclua o novo nome de arquivo no caminho de diretório que você fornecer para o destino.|  
|**Definir atributos**|Define os atributos de um arquivo ou diretório. A seleção desse valor exibe as opções dinâmicas para origem e operação.|  
  
 **IsSourcePathVariable**  
 Indique se o caminho de destino deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor||  
|-----------|-|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **DestinationVariable**será exibida.|  
  
### <a name="isdestinationpathvariable-dynamic-options"></a>Opções dinâmicas de IsDestinationPathVariable  
  
#### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Selecione o nome da variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 **DestinationConnection**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="issourcepathvariable-dynamic-options"></a>Opções dinâmicas de IsSourcePathVariable  
  
#### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Selecione o nome da variável na lista ou clique em \<**Nova variável...** > para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 **SourceConnection**  
 Selecione um gerenciador de conexões de arquivos na lista ou clique em \<**Nova conexão…** > para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexão de Arquivo](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="operation-dynamic-options"></a>Opções dinâmicas de operação  
  
#### <a name="operation--set-attributes"></a>Operação = Definir atributos  
 **Oculto**  
 Indique se o arquivo ou diretório deve ficar visível.  
  
 **ReadOnly (somente-leitura)**  
 Indique se o arquivo é somente leitura.  
  
 **Arquivar**  
 Indique se o arquivo ou diretório está pronto para ser arquivado.  
  
 **Sistema**  
 Indique se o arquivo é um arquivo do sistema operacional.  
  
#### <a name="operation--create-directory"></a>Operação = Criar diretório  
 **UseDirectoryIfExists**  
 Indica se a operação **Criar diretório** usa um diretório existente com o nome especificado, em vez de criar um novo diretório.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
  
