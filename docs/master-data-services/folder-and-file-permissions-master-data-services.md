---
title: "Permiss&#245;es de pasta e arquivo (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "segurança [Master Data Services], arquivo e pasta"
  - "pastas [Master Data Services]"
  - "arquivos [Master Data Services]"
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Permiss&#245;es de pasta e arquivo (Master Data Services)
  Quando você instala o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], as pastas e arquivos são instalados no sistema de arquivos no caminho de instalação especificado para recursos compartilhados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se você usar o caminho de instalação padrão para recursos compartilhados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o caminho de instalação para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] será *drive*:\Program Files\Microsoft SQL Server\130\Master Data Services. Embora seja possível alterar o caminho de instalação de recursos compartilhados, considere as permissões que são herdadas da pasta pai e as permissões que são definidas explicitamente para o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## Permissões herdadas  
 A pasta **Microsoft SQL Server**, a pasta **Master Data Services** e a maioria das subpastas e arquivos herda permissões da pasta pai especificada na Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se você escolher o local de instalação padrão, a pasta pai da qual as permissões são herdadas será *drive*:\Program Files. A tabela a seguir descreve as permissões padrão para **Arquivos de Programas**.  
  
> [!NOTE]  
>  Se você modificar as permissões padrão de **Arquivos de Programas** ou escolher outro local de instalação, as pastas e arquivos do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] herdarão as permissões da respectiva pasta pai e as permissões poderão diferir das que são descritas na tabela a seguir.  
  
###### Permissões padrão de Arquivos de Programas  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|CREATOR OWNER|Permissões especiais|  
|SYSTEM|Permissões especiais|  
|Administradores|Permissões especiais|  
|Usuários|Ler & executar, listar conteúdo da pasta, leitura|  
|TrustedInstaller|Listar conteúdo de pasta, permissões especiais|  
  
## Permissões explícitas  
 A pasta **MDSTempDir** e o arquivo Web.config do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (na pasta **WebApplication**) não herdam permissões. Eles têm permissões que são definidas explicitamente quando você instala o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], independentemente do caminho de instalação escolhido. Não modifique essas permissões.  
  
###### Permissões de MDSTempDir  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|SYSTEM|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
|Administradores|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
|MDS_ServiceAccounts|Modificar, ler & executar, listar conteúdo da pasta, leitura, gravação|  
  
###### Permissões de Web.config  
  
|Nome do grupo ou conta|Permissões|  
|---------------------------|-----------------|  
|SYSTEM|Controle completo, modificar, ler & executar, leitura, gravação|  
|Administradores|Controle completo, modificar, ler & executar, leitura, gravação|  
|MDS_ServiceAccounts|Ler & executar, leitura|  
  
 Para obter mais informações sobre o conteúdo do arquivo Web.config do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Referência de configuração da Web &#40;Master Data Services&#41;](../master-data-services/web-configuration-reference-master-data-services.md).  
  
## Consulte também  
 [Instalar o Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  