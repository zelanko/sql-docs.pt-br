---
title: Gerenciar pacotes e pastas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5c45f6a5b59a65046a0e48fd930fd27d689c0a0a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913299"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gerenciando pacotes e pastas programaticamente

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


<a name="top"></a> Ao trabalhar de forma programática com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], convém determinar se um pacote ou pasta individual existe ou então gerenciar as pastas em que os pacotes estão armazenados. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.    
    
##  <a name="determining-whether-a-package-or-folder-exists"></a><a name="exists"></a> Determinando se existe um pacote ou pasta    
 Para determinar programaticamente se existe um pacote salvo, chame um dos métodos a seguir antes de tentar carregar e executar o pacote:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.ExistsOnSqlServer%2A>|    
    
 Para determinar programaticamente se existe uma pasta, chame um dos métodos a seguir antes de tentar listar os pacotes armazenados na pasta:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.FolderExistsOnSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
##  <a name="managing-packages-and-folders"></a><a name="managing"></a> Gerenciar pacotes e pastas    
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos adicionais para gerenciar pacotes e as pastas nas quais eles são armazenados.    
    
###  <a name="removing-a-package"></a><a name="managing_rempkg"></a> Remover um pacote    
 Para remover um pacote salvo programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="creating-a-folder"></a><a name="managing_create"></a> Criar uma pasta    
 Para criar uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="removing-a-folder"></a><a name="managing_remfldr"></a> Remover uma pasta    
 Para remover uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="renaming-a-folder"></a><a name="managing_rename"></a> Renomear uma pasta    
 Para renomear uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
## <a name="see-also"></a>Consulte Também    
 [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerar pacotes disponíveis programaticamente](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
