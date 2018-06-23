---
title: MSSQLSERVER_3169 | Microsoft Docs
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
- "3169"
helpviewer_keywords:
- 3169 (Database Engine error)
ms.assetid: 7d4dbed6-bb94-4908-bc03-2040a9cf63bc
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5df7d4d735c680d6924d2d0a63045bf878571b04
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116383"
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
 Determine a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo executada no servidor de origem. Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou com o botão direito do servidor e, em seguida, clique em **propriedades** ou tipo `SELECT @@VERSION` em uma janela de consulta. Abra o banco de dados usando a versão original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Investigue os recursos habilitados no banco de dados original na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Modifique essas configurações para funcionarem com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o banco de dados será restaurado.  
  
  