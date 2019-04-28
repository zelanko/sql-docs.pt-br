---
title: Gerenciador de Conexões de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cf820e3f5a3f4a2ca9db28510b867c5dbc8f3c4f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833800"
---
# <a name="file-connection-manager"></a>Gerenciador de conexões de arquivos
  Um gerenciador de conexões de Arquivo permite que um pacote faça referência a um arquivo ou pasta existente ou crie um arquivo ou pasta em tempo de execução. Por exemplo, você pode fazer referência a um arquivo do Excel. Alguns componentes em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usam as informações nos arquivos para executar seu trabalho. Por exemplo, uma tarefa Executar SQL pode fazer referência a um arquivo que contém as instruções SQL que a tarefa executa. Outros componentes executam operações em arquivos. Por exemplo, a tarefa Sistema de Arquivos pode fazer referência a um arquivo para copiá-lo para um novo local.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Tipos de uso do gerenciador de conexões de arquivos  
 A propriedade `FileUsageType` do gerenciador de conexões de arquivos especifica como a conexão de arquivos é utilizada. O gerenciador de conexões de arquivos pode criar tanto um arquivo quanto uma pasta e utilizar um arquivo ou uma pasta existente.  
  
 A tabela a seguir lista os valores de `FileUsageType`.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`0`|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|`1`|O gerenciador de conexões de arquivos cria um arquivo.|  
|`2`|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|`3`|O gerenciador de conexões de arquivos cria um arquivo.|  
  
## <a name="multiple-file-or-folder-connections"></a>Várias conexões de arquivo ou pasta  
 O gerenciador de conexões de arquivos pode fazer referência a apenas um arquivo ou a uma pasta. Para consultar vários arquivos ou pastas, utilize um gerenciador de conexões para vários arquivos em vez de um gerenciador de conexões de arquivos. Para obter mais informações, consulte [Multiple Files Connection Manager](multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Configuração do gerenciador de conexões de arquivo  
 Quando você adicionar um gerenciador de conexões de arquivos a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um gerenciador de conexões que determinará uma conexão de Arquivo no tempo de execução, definirá as propriedades da conexão de Arquivos e irá adicioná-la à coleção `Connections` do pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `FILE`.  
  
 Você pode configurar um gerenciador de conexões de arquivos dos seguintes modos:  
  
-   Especificando o tipo de uso.  
  
-   Especificando um arquivo ou uma pasta.  
  
 Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No entanto, para evitar um erro de validação ao usar uma expressão para especificar o arquivo ou a pasta, no **Editor do Gerenciador de Conexões de Arquivos**, para **Arquivo/Pasta**, adicione um caminho de arquivo ou de pasta.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de Arquivos](../file-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
