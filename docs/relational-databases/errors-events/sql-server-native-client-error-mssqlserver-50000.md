---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f872d7d0a2495e747ae0b3d63997f7270c585c53
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>Erro do SQL Server Native Client MSSQLSERVER_50000
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|Versão do Produto|11.0|  
|ID do evento|50000|  
|Origem do evento|SETUP|  
|Componente|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro de rede ao tentar ler a partir do arquivo '%. * ls'.|  
  
## <a name="explanation"></a>Explicação  
 Foi feita uma tentativa de instalar (ou atualizar) o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client em um computador onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client já foi instalado e onde a instalação existente era de um arquivo MSI que foi renomeado de sqlncli.msi.  
  
## <a name="user-action"></a>Ação do usuário  
 Para resolver este erro, desinstale a versão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para evitar esse erro, não instale o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client de um arquivo MSI que não seja denominado sqlncli.msi.  
  
## <a name="internal-only"></a>Somente interno  
  
