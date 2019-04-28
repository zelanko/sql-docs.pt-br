---
title: Gerenciador de Conexões de Vários Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 086790cbd654a101d4bced989848d9aaac80d7ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833609"
---
# <a name="multiple-files-connection-manager"></a>Gerenciador de conexões de vários arquivos
  Um gerenciador de conexões de Vários Arquivos permite que um pacote faça referência a arquivos e pastas existentes ou crie arquivos e pastas em tempo de execução.  
  
> [!NOTE]  
>  As tarefas internas e os componentes de fluxo de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não usam o gerenciador de conexões de vários arquivos. No entanto você pode usar o gerenciador de conexões na tarefa Script ou no componente Script. Para obter informações sobre como usar gerenciadores de conexões na tarefa Script, consulte [Conectando-se a fontes de dados na tarefa Script](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md). Para obter informações sobre como usar gerenciadores de conexão no componente Script, consulte [conexão a fontes de dados no componente Script] (... / extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md.  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>Tipos de uso do gerenciador de conexões de vários arquivos  
 A propriedade `FileUsageType` do gerenciador de conexões de vários arquivos especifica como a conexão é utilizada. O gerenciador de conexões de vários arquivos pode criar arquivos, pastas e usar arquivos e pastas existentes.  
  
 A tabela a seguir lista os valores de `FileUsageType`.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**0**|O gerenciador de conexões de vários arquivos utiliza um arquivo existente.|  
|**1**|O gerenciador de conexões de vários arquivos cria um arquivo.|  
|**2**|O gerenciador de conexões de vários arquivos utiliza uma pasta existente.|  
|**3**|O gerenciador de conexões de vários arquivos cria uma pasta.|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>Configuração do gerenciador de conexões de vários arquivos  
 Quando você adicionar um gerenciador de conexões de vários arquivos a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um gerenciador de conexões que será resolvido como um gerenciador de conexões de vários arquivos no tempo de execução, definirá as propriedades de conexão de vários arquivos e adicionará essa conexão à coleção `Connections` do pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `MULTIFILE`.  
  
 Você pode configurar um gerenciador de conexões de vários arquivos da seguinte maneira:  
  
-   Especifique o tipo de uso de arquivos e pastas.  
  
-   Especifique as pastas e os arquivos.  
  
-   Se estiver usando vários arquivos ou pastas, especifique a ordem na qual devem ser acessados os arquivos e as pastas.  
  
 Se o gerenciador de conexões de vários arquivos consultar vários arquivos e pastas, os caminhos dos arquivos e pastas serão separados pelo caractere pipe (|). A propriedade `ConnectionString` do gerenciador de conexões tem o seguinte formato:  
  
 \<*path*>|\<*path*>  
  
 Você também pode especificar vários arquivos ou pastas usando caracteres curingas. Por exemplo, a unidade de todos os arquivos de texto em C, o valor de referência a `ConnectionString` propriedade pode ser definida como c:\\*. txt.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](add-file-connection-manager-dialog-box-ui-reference.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
