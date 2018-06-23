---
title: MSSQLSERVER_948 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "948"
helpviewer_keywords:
- 948 (Database Engine error)
ms.assetid: 95c4ad45-a518-4165-a5c4-6e6b932b0570
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: cb36765216f906b92cdd6b87e7890b94f3b15d37
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122409"
---
# <a name="mssqlserver948"></a>MSSQLSERVER_948
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|948|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NA|  
|Texto da mensagem|O banco de dados '%.*ls' não pode ser aberto porque sua versão é a %d. Esse servidor oferece suporte à versão %d e anteriores. Não há suporte para um caminho de downgrade.|  
  
## <a name="explanation"></a>Explicação  
 Determinados recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afetam a estrutura dos arquivos de banco de dados. Quando você anexa um banco de dados a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível que o formato de arquivo não seja compatível com uma versão diferente do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Por exemplo, esse erro pode ser causado pelo uso de um formato de armazenamento vardecimal em uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, depois, pela tentativa de anexar os arquivos de banco de dados a uma versão anterior a do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2.  
  
## <a name="user-action"></a>Ação do usuário  
 Determine a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada no servidor de origem. Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou com o botão direito do servidor e, em seguida, clique em **propriedades** ou tipo `SELECT @@VERSION` em uma janela de consulta. Abra o banco de dados usando a versão original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Investigue os recursos habilitados no banco de dados original na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique essas configurações para trabalhar com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual será anexado o banco de dados.  
  
  