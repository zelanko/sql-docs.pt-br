---
description: Permissões de pasta e arquivo (Master Data Services)
title: Permissões de pasta e arquivo
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- security [Master Data Services], file and folder
- folders [Master Data Services]
- files [Master Data Services]
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0d06fb6aaacdac159ab9241209c862e22758e999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88388822"
---
# <a name="folder-and-file-permissions-master-data-services"></a>Permissões de pasta e arquivo (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Quando você instala o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], as pastas e arquivos são instalados no sistema de arquivos no caminho de instalação especificado para recursos compartilhados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se você usar o caminho de instalação padrão para recursos compartilhados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o caminho de instalação para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] será *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services. Embora seja possível alterar o caminho de instalação de recursos compartilhados, considere as permissões que são herdadas da pasta pai e as permissões que são definidas explicitamente para o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## <a name="inherited-permissions"></a>Permissões herdadas  
 A pasta **Microsoft SQL Server** , a pasta **Master Data Services** e a maioria das subpastas e arquivos herda permissões da pasta pai especificada na Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se você escolher o local de instalação padrão, a pasta pai da qual as permissões são herdadas será *drive*:\Program Files. A tabela a seguir descreve as permissões padrão para **Arquivos de Programas**.  
  
> [!NOTE]  
>  Se você modificar as permissões padrão de **Arquivos de Programas**ou escolher outro local de instalação, as pastas e arquivos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] herdarão as permissões da respectiva pasta pai e as permissões poderão diferir das que são descritas na tabela a seguir.  
  
###### <a name="program-files-default-permissions"></a>Permissões padrão de Arquivos de Programas  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|CREATOR OWNER|Permissões especiais|  
|SYSTEM|Permissões especiais|  
|Administradores|Permissões especiais|  
|Usuários|Ler & executar, listar conteúdo da pasta, leitura|  
|TrustedInstaller|Listar conteúdo de pasta, permissões especiais|  
  
## <a name="explicit-permissions"></a>Permissões explícitas  
 A pasta **MDSTempDir** e o arquivo Web.config do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (na pasta **WebApplication** ) não herdam permissões. Eles têm permissões que são definidas explicitamente quando você instala o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], independentemente do caminho de instalação escolhido. Não modifique essas permissões.  
  
###### <a name="mdstempdir-permissions"></a>Permissões de MDSTempDir  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|SYSTEM|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
|Administradores|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
|MDS_ServiceAccounts|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
  
###### <a name="webconfig-permissions"></a>Permissões de Web.config  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|SYSTEM|Controle completo, modificar, ler & executar, leitura, gravação|  
|Administradores|Controle completo, modificar, ler & executar, leitura, gravação|  
|MDS_ServiceAccounts|Ler & executar, leitura|  
  
 Para obter mais informações sobre o conteúdo do arquivo Web.config do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Referência de configuração da Web &#40;Master Data Services&#41;](../master-data-services/web-configuration-reference-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  
