---
title: A propriedade ServerName (classe SqlServerAlias) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ServerName Property (SqlServerAlias Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ServerName property
ms.assetid: 58c82b19-b548-42fa-9c5a-059b606da097
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 317035d73eae387b9de06324415b795693527489
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119475"
---
# <a name="servername-property-sqlserveralias-class"></a>Propriedade ServerName (classe SqlServerAlias)
  Obtém o nome da instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] especificado pelo alias de conexão do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.ServerName [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServerAlias](sqlserveralias-class.md) que representa um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor da cadeia de caracteres que especifica o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] referenciado pelo alias de conexão do servidor.  
  
## <a name="remarks"></a>Remarks  
  