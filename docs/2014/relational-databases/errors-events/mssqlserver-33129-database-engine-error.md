---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b879bcb492783eec2cbca121f2596d096e2f673f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120368"
---
# <a name="mssqlserver33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|33129|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CANNOT_DISABLE_WIN_GROUP|  
|Texto da mensagem|Não é possível usar ALTER_LOGIN com o argumento DISABLE para negar acesso a um grupo do Windows.|  
  
## <a name="explanation"></a>Explicação  
 Esta mensagem ocorre na tentativa de desabilitar o logon de um Grupo do Windows.  
  
## <a name="user-action"></a>Ação do usuário  
 O logon de um Grupo do Windows não pode ser desabilitado. Para remover temporariamente a permissão de acesso concedida a um Grupo do Windows, revogue (REVOKE) a permissão CONNECT do logon para o Grupo do Windows. Os usuários do Windows possivelmente ainda deverão ter acesso por meio do logon individual ou através de outro Grupo do Windows. O exemplo a seguir revoga a permissão connect no Grupo de Contabilidade do domínio WESTCOAST.  
  
```tsql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  