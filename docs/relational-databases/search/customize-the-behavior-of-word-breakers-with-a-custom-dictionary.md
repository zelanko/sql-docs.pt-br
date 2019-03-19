---
title: Personalizar o comportamento de separadores de palavras com um dicionário personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 957b9e6834e4f590a1ef71a515d287a88fe6cc93
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973765"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>Personalizar o comportamento de separadores de palavras com um dicionário personalizado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode personalizar o comportamento do separador de palavras por um idioma específico criando um arquivo de dicionário personalizado específico do idioma. Por exemplo, você pode impedir que o separador de palavras quebre certas condições ou padrões.  
  
 Para obter mais informações, consulte o seguinte artigo do SharePoint:  
  
 [Crie um dicionário personalizado (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=215011)  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], coloque arquivos de dicionário personalizados na seguinte pasta:  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 Depois de criar ou alterar arquivos de dicionário personalizados, reinicie o Lançador de Daemon de texto completo SQL com o seguinte comando:  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
