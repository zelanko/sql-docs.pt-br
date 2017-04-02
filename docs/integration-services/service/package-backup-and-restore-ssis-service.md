---
title: "Backup e restaura&#231;&#227;o de pacotes (servi&#231;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pacotes do SSIS, backup e restauração"
  - "fazendo backup de pacotes [Integration Services]"
  - "pacotes [Integration Services], backup e restauração"
  - "pacotes do SQL Server Integration Services, backup e restauração"
  - "restaurando pacotes [Integration Services]"
  - "pacotes do Integration Services, backup e restauração"
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Backup e restaura&#231;&#227;o de pacotes (servi&#231;o SSIS)
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes podem ser salvos no sistema de arquivos ou no msdb, um banco de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os pacotes salvos no msdb podem ter backup e serem restaurados usando recursos de backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como fazer backups e restauração do banco de dados msdb, clique em um dos seguintes tópicos:  
  
-   [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui o utilitário de prompt de comando **dtutil** (dtutil.exec), que pode ser usado para gerenciar pacotes. Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## Arquivos de configuração  
 Qualquer arquivo de configuração incluído nos pacotes é armazenado no sistema de arquivos. Esses arquivos não são salvos ao fazer o backup do banco de dados msdb; portanto, você deve verificar se o backup é realizado regularmente em todos os arquivos de configuração como parte de seu plano para proteger os pacotes salvos no msdb. Para incluir as configurações no backup do banco de dados msdb, você deve considerar o uso do tipo de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em vez das configurações baseadas em arquivos.  
  
## Pacotes armazenados no sistema de arquivos  
 O backup de pacotes salvos no sistema de arquivos deveria ser incluído no plano de backup do sistema de arquivos do servidor. O arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], com o nome padrão de MsDtsSrvr.ini.xml, lista no servidor as pastas monitoradas pelo serviço. Você deve verificar se essas pastas têm backup. Além disso, os pacotes podem ser armazenados em outras pastas no servidor e você deve verificar se essas pastas estão incluídas no backup.  
  
  