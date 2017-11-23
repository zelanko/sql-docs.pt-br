---
title: GetPathLocator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs: TSQL
helpviewer_keywords: GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 30e1f626885e850d8aca6cc30360033c055855f2
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna a ID do localizador do caminho do arquivo ou diretório especificado em uma FileTable.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://msdn.microsoft.com/library/bb500435.aspx)).|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>Argumentos  
 *filenamespace_path*  
 Um caminho de namespace na FileTable. O caminho do namespace é do tipo **nvarchar (max)**.  
  
 Quando o banco de dados pertence a um grupo de disponibilidade AlwaysOn, então o **GetPathLocator** função aceita o nome de rede virtual (VNN) ou o nome do computador.  
  
## <a name="return-type"></a>Tipo de retorno  
 **hierarchyid**  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="examples"></a>Exemplos  
 Você pode usar o **GetPathLocator** funcionar quando você estiver migrando arquivos de um servidor de arquivos para uma FileTable. Neste cenário, você deseja mover os arquivos para a FileTable e, em seguida, substituir o caminho UNC original de cada arquivo com o caminho UNC da FileTable. Para obter um exemplo completo, consulte [carregar arquivos em FileTables](../../relational-databases/blob/load-files-into-filetables.md).  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
