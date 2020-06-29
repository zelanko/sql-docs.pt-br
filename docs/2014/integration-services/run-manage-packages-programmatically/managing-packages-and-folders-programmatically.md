---
title: Gerenciar pacotes e pastas programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 5baa8949fc74d92c3a4bcae46dbe4f9c7e1b9f40
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422693"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gerenciando pacotes e pastas programaticamente
  Ao trabalhar de forma programática com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], convém determinar se um pacote ou pasta individual existe ou gerenciar as pastas em que os pacotes estão armazenados. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.  
  
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
  

  
##  <a name="managing-packages-and-folders"></a><a name="managing"></a> Gerenciar pacotes e pastas  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos adicionais para gerenciar pacotes e as pastas nas quais eles são armazenados.  
  
###  <a name="removing-a-package"></a><a name="managing_rempkg"></a> Remover um pacote  
 Para remover um pacote salvo programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="creating-a-folder"></a><a name="managing_create"></a> Criar uma pasta  
 Para criar uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="removing-a-folder"></a><a name="managing_remfldr"></a> Remover uma pasta  
 Para remover uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="renaming-a-folder"></a><a name="managing_rename"></a> Renomear uma pasta  
 Para renomear uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de Pacotes &#40;serviço SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerando pacotes disponíveis programaticamente](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
