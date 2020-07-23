---
title: Gerenciador de Conexões de Arquivos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 11c5a2404ec0c5dd8a51f09b1b96a4b5518231ae
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920780"
---
# <a name="file-connection-manager"></a>Gerenciador de conexões de arquivos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões de Arquivo permite que um pacote faça referência a um arquivo ou pasta existente ou crie um arquivo ou pasta em tempo de execução. Por exemplo, você pode fazer referência a um arquivo do Excel. Alguns componentes em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usam as informações nos arquivos para executar seu trabalho. Por exemplo, uma tarefa Executar SQL pode fazer referência a um arquivo que contém as instruções SQL que a tarefa executa. Outros componentes executam operações em arquivos. Por exemplo, a tarefa Sistema de Arquivos pode fazer referência a um arquivo para copiá-lo para um novo local.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Tipos de uso do gerenciador de conexões de arquivos  
 A propriedade **FileUsageType** do gerenciador de conexões de arquivos especifica como a conexão de arquivos é utilizada. O gerenciador de conexões de arquivos pode criar tanto um arquivo quanto uma pasta e utilizar um arquivo ou uma pasta existente.  
  
 A tabela a seguir lista os valores de **FileUsageType**.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**0**|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|**1**|O gerenciador de conexões de arquivos cria um arquivo.|  
|**2**|O gerenciador de conexões de arquivos utiliza um arquivo existente.|  
|**3**|O gerenciador de conexões de arquivos cria um arquivo.|  
  
## <a name="multiple-file-or-folder-connections"></a>Várias conexões de arquivo ou pasta  
 O gerenciador de conexões de arquivos pode fazer referência a apenas um arquivo ou a uma pasta. Para consultar vários arquivos ou pastas, utilize um gerenciador de conexões para vários arquivos em vez de um gerenciador de conexões de arquivos. Para obter mais informações, consulte [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Configuração do gerenciador de conexões de arquivo  
 Quando você adicionar um gerenciador de conexões de arquivos a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um gerenciador de conexões que será resolvido para uma conexão de arquivos em tempo de execução, definirá as propriedades da conexão de arquivos e adicionará a conexão de arquivos à coleção **Connections** do pacote.  
  
 A propriedade **ConnectionManagerType** do gerenciador de conexões é definida como **FILE**.  
  
 Você pode configurar um gerenciador de conexões de arquivos dos seguintes modos:  
  
-   Especificando o tipo de uso.  
  
-   Especificando um arquivo ou uma pasta.  
  
 Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No entanto, para evitar um erro de validação ao usar uma expressão para especificar o arquivo ou a pasta, no **Editor do Gerenciador de Conexões de Arquivos**, para **Arquivo/Pasta**, adicione um caminho de arquivo ou de pasta.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="file-connection-manager-editor"></a>Editor do Gerenciador de Conexões de Arquivos
  Use a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** para especificar as propriedades usadas para conectar a um arquivo ou pasta.  
  
> [!NOTE]  
>  Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No entanto, para evitar um erro de validação ao usar uma expressão para especificar o arquivo ou a pasta, no **Editor do Gerenciador de Conexões de Arquivos**, para **Arquivo/Pasta**, adicione um caminho de arquivo ou de pasta.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivos, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Tipo de Uso**  
 Especifique se o **Gerenciador de Conexões de Arquivos** conecta a um arquivo ou pasta existente ou crie um novo arquivo ou pasta.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|Criar arquivo|Crie um novo arquivo em tempo de execução.|  
|Arquivo existente|Use um arquivo existente.|  
|Criar pasta|Crie uma nova pasta em tempo de execução.|  
|Pasta existente|Use uma pasta existente.|  
  
 **Arquivo / Pasta**  
 Se **Arquivo**, especifique o arquivo a usar.  
  
 Se **Pasta**, especifique a pasta a usar.  
  
 **Procurar**  
 Selecione o arquivo ou pasta usando a caixa de diálogo **Selecionar Arquivo** ou **Procurar Pasta** .  
  
  
