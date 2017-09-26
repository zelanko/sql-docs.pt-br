---
title: Gerenciando pacotes e pastas programaticamente | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- enumerators [Integration Services]
- packages [Integration Services], managing
- custom enumerators [Integration Services]
ms.assetid: ec59b75d-ba09-44ac-9039-9d593bb462d9
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a40acf3a586c74119d948291fd179f78833cb37a
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="managing-packages-and-folders-programmatically"></a>Gerenciando pacotes e pastas programaticamente
<a name="top"></a>Ao trabalhar programaticamente com [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes, talvez você queira determinar se existe um pacote ou pasta individual, ou para gerenciar as pastas nas quais os pacotes são armazenados. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.    
    
##  <a name="exists"></a>Determinando se existe um pacote ou pasta    
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
    
##  <a name="managing"></a>Gerenciando pacotes e pastas    
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos adicionais para gerenciar pacotes e as pastas nas quais eles são armazenados.    
    
###  <a name="managing_rempkg"></a>Remoção de um pacote    
 Para remover um pacote salvo programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="managing_create"></a>Criando uma pasta    
 Para criar uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="managing_remfldr"></a>Remoção de uma pasta    
 Para remover uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
###  <a name="managing_rename"></a>Renomeando uma pasta    
 Para renomear uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:    
    
|Local de armazenamento|Método de chamada|    
|----------------------|--------------------|    
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|    
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|    
    
 [Voltar ao início](#top)    
    
## <a name="see-also"></a>Consulte também    
 [Pacote de gerenciamento &#40; Serviço do SSIS &#41;](../../integration-services/service/package-management-ssis-service.md)     
 [Enumerar pacotes disponíveis programaticamente](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)    
    
  
