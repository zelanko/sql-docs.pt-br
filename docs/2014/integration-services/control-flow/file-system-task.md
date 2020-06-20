---
title: Tarefa do Sistema de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.filesystemtask.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bbe47dbba2def9a40caf506fe9d0b5cb914d1052
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84918896"
---
# <a name="file-system-task"></a>Tarefa Sistema de Arquivos
  A tarefa Sistema de Arquivos executa operações em arquivos e diretórios no sistema de arquivos. Por exemplo, ao usar a tarefa Sistema de Arquivos, um pacote pode criar, mover ou excluir diretórios e arquivos. Você também pode usar a tarefa Sistema de Arquivos para definir atributos em arquivos e diretórios. Por exemplo, a tarefa Sistema de Arquivos pode tornar os arquivos em ocultos ou somente leitura.  
  
 Todas as operações da tarefa Sistema de Arquivos usam uma origem, que pode ser um arquivo ou diretório. Por exemplo, o arquivo que a tarefa copia ou o diretório que ela exclui é uma origem. A origem pode ser especificada usando um gerenciador de conexões de arquivos que aponta para o diretório ou arquivo, ou fornecendo o nome de uma variável que contém o caminho de origem. Para obter mais informações, consulte [Gerenciador de Conexões de Arquivos](../connection-manager/file-connection-manager.md) e [Variáveis do Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).  
  
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
 A tabela a seguir descreve a entrada de log personalizada da tarefa Sistema de Arquivos. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../custom-messages-for-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|`FileSystemOperation`|Informa a operação executada pela tarefa. A entrada de log é gravada quando a operação de sistema de arquivos é iniciada e inclui informações sobre a origem e o destino.|  
  
## <a name="configuring-the-file-system-task"></a>Configurando a tarefa Arquivo de Sistemas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte os tópicos a seguir:  
  
-   [Editor da Tarefa Sistema de Arquivos &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, consulte o tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md)  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte o tópico a seguir:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui uma tarefa que faz downloads e uploads de arquivos de dados e gerencia diretórios em servidores. Para obter mais informações, consulte [FTP Task](ftp-task.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas de Integration Services](integration-services-tasks.md)   
 [Fluxo de controle](control-flow.md)  
  
  
