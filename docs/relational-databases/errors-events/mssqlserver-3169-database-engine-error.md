---
title: MSSQLSERVER_3169 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9638b59b34c8b110a5dca72a274d923a02119cbf
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3169"></a>MSSQLSERVER_3169
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3169|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NA|  
|Texto da mensagem|O backup do banco de dados foi feito em um servidor que executa a versão %ls. Essa versão é incompatível com esse servidor que está executando a versão %ls. Restaure o banco de dados em um servidor que dê suporte ao backup ou use um backup compatível com esse servidor.|  
  
## <a name="explanation"></a>Explicação  
Determinados recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afetam a estrutura dos arquivos de banco de dados. Quando você restaura um banco de dados em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível que o formato de arquivo não seja compatível com uma versão diferente do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
Por exemplo, esse erro pode ser causado pelo uso do formato vardecimalstorage em uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, pela tentativa de restaurar os arquivos de banco de dados em uma versão anterior ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2.  
  
## <a name="user-action"></a>Ação do usuário  
Determine a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada no servidor de origem. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no servidor e, em seguida, clique em **Propriedades** ou digite **SELECT @@VERSION** em uma janela de consulta. Abra o banco de dados usando a versão original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Investigue os recursos habilitados no banco de dados original na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique essas configurações para funcionarem com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o banco de dados será restaurado.  
  

