---
title: "Personalizar o comportamento de separadores de palavras com um dicion&#225;rio personalizado | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Personalizar o comportamento de separadores de palavras com um dicion&#225;rio personalizado
  Você pode personalizar o comportamento do separador de palavras por um idioma específico criando um arquivo de dicionário personalizado específico do idioma. Por exemplo, você pode impedir que o separador de palavras quebre certas condições ou padrões.  
  
 Para obter mais informações, consulte o seguinte artigo do SharePoint:  
  
 [Crie um dicionário personalizado (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque arquivos de dicionário personalizados na seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Depois de criar ou alterar arquivos de dicionário personalizados, reinicie o Lançador de Daemon de texto completo SQL com o seguinte comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  