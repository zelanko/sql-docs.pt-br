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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a6ede05e340cbd2822cd72ceee514f6ce31a2755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766848"
---
# <a name="managing-packages-and-folders-programmatically"></a>Gerenciando pacotes e pastas programaticamente
  Ao trabalhar de forma programática com pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], convém determinar se um pacote ou pasta individual existe ou gerenciar as pastas em que os pacotes estão armazenados. A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece diversos métodos para atender a esses requisitos.  
  
##  <a name="exists"></a> Determinando se existe um pacote ou pasta  
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
  

  
##  <a name="managing"></a> Gerenciar pacotes e pastas  
 A classe <xref:Microsoft.SqlServer.Dts.Runtime.Application> do namespace <xref:Microsoft.SqlServer.Dts.Runtime> fornece métodos adicionais para gerenciar pacotes e as pastas nas quais eles são armazenados.  
  
###  <a name="managing_rempkg"></a> Remover um pacote  
 Para remover um pacote salvo programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFromSqlServer%2A>|  
  

  
###  <a name="managing_create"></a> Criar uma pasta  
 Para criar uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.CreateFolderOnSqlServer%2A>|  
  

  
###  <a name="managing_remfldr"></a> Remover uma pasta  
 Para remover uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RemoveFolderFromSqlServer%2A>|  
  
  
  
###  <a name="managing_rename"></a> Renomear uma pasta  
 Para renomear uma pasta de armazenamento programaticamente, chame um dos métodos seguintes:  
  
|Local de armazenamento|Método de chamada|  
|----------------------|--------------------|  
|Armazenamento de Pacotes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.RenameFolderOnSqlServer%2A>|  
  

  
![Ícone do Integration Services (pequeno)](../media/dts-16.gif "ícone do Integration Services (pequeno)")**mantenha-se para cima até o momento com o Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Pacotes &#40;Serviço SSIS&#41;](../service/package-management-ssis-service.md)   
 [Enumerar pacotes disponíveis programaticamente](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
