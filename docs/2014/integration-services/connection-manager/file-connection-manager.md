---
title: Gerenciador de Conexões de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d9f02969042ec839a708045143b748890d25c1de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118186"
---
# <a name="file-connection-manager"></a>Gerenciador de conexões de arquivos
  Um gerenciador de conexões de Arquivo permite que um pacote faça referência a um arquivo ou pasta existente ou crie um arquivo ou pasta em tempo de execução. Por exemplo, você pode fazer referência a um arquivo do Excel. Alguns componentes em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usam as informações nos arquivos para executar seu trabalho. Por exemplo, uma tarefa Executar SQL pode fazer referência a um arquivo que contém as instruções SQL que a tarefa executa. Outros componentes executam operações em arquivos. Por exemplo, a tarefa Sistema de Arquivos pode fazer referência a um arquivo para copiá-lo para um novo local.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Tipos de uso do gerenciador de conexões de arquivos  
 O `FileUsageType` propriedade do Gerenciador de conexão de arquivo Especifica como a conexão de arquivo é usado. O gerenciador de conexões de arquivos pode criar tanto um arquivo quanto uma pasta e utilizar um arquivo ou uma pasta existente.  
  
 A tabela a seguir lista os valores de `FileUsageType`.  
  
|Valor|Description|  
|-----------|-----------------|  
|`0`|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|`1`|O gerenciador de conexões de arquivos cria um arquivo.|  
|`2`|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|`3`|O gerenciador de conexões de arquivos cria um arquivo.|  
  
## <a name="multiple-file-or-folder-connections"></a>Várias conexões de arquivo ou pasta  
 O gerenciador de conexões de arquivos pode fazer referência a apenas um arquivo ou a uma pasta. Para consultar vários arquivos ou pastas, utilize um gerenciador de conexões para vários arquivos em vez de um gerenciador de conexões de arquivos. Para obter mais informações, consulte [Multiple Files Connection Manager](multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Configuração do gerenciador de conexões de arquivo  
 Quando você adicionar um Gerenciador de conexão de arquivo a um pacote, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria uma conexão Gerenciador que resolverá uma conexão de arquivo em tempo de execução, define as propriedades de conexão de arquivo e adiciona a conexão de arquivo para o `Connections` coleção do pacote.  
  
 O `ConnectionManagerType` propriedade do Gerenciador de conexão está definida como `FILE`.  
  
 Você pode configurar um gerenciador de conexões de arquivos dos seguintes modos:  
  
-   Especificando o tipo de uso.  
  
-   Especificando um arquivo ou uma pasta.  
  
 Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No entanto, para evitar um erro de validação ao usar uma expressão para especificar o arquivo ou a pasta, no **Editor do Gerenciador de Conexões de Arquivos**, para **Arquivo/Pasta**, adicione um caminho de arquivo ou de pasta.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de Arquivos](../file-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um Gerenciador de conexão programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  