---
title: "Personalizar o comportamento de separadores de palavras com um dicionário personalizado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9325fc9817b8c0f57ebeb9c6a0e9ae8f29b899cc
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizar o comportamento de separadores de palavras com um dicionário personalizado
  Você pode personalizar o comportamento do separador de palavras por um idioma específico criando um arquivo de dicionário personalizado específico do idioma. Por exemplo, você pode impedir que o separador de palavras quebre certas condições ou padrões.  
  
 Para obter mais informações, consulte o seguinte artigo do SharePoint:  
  
 [Crie um dicionário personalizado (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque arquivos de dicionário personalizados na seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Depois de criar ou alterar arquivos de dicionário personalizados, reinicie o Lançador de Daemon de texto completo SQL com o seguinte comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  

