---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 991757d1bfeae8ecc0dec3a69d82c3dcab6415b1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531648"
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
  
```sql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  
