---
title: "Notas de Versão do SQL Server 2012 SP2 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 978e780dd19e34c27ceef49ff8388f6ae1f155ed
ms.openlocfilehash: ed00031d1f55fc6fda2ee1c37fe76f7637e8e891
ms.contentlocale: pt-br
ms.lasthandoff: 09/02/2017

---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
Este documento de Notas de Versão descreve os problemas com os quais você deve estar familiarizado antes de instalar ou solucionar problemas do SQL Server 2012 Service Pack 2. As Notas de Versão listadas aqui estão disponíveis somente online, e não em mídia de instalação. Elas são atualizadas periodicamente, conforme os problemas são descobertos. Veja os [bugs corrigidos no SQL Server 2012 Service Pack 2](http://support.microsoft.com/KB/2958429) para mais informações.  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>Escolha o arquivo correto para baixar e instalar  
Use a tabela abaixo para identificar o local e o nome do arquivo a ser baixado com base em sua versão atualmente instalada. As páginas de download têm requisitos de sistema e instruções básicas de instalação.  
  
||||  
|-|-|-|  
|**A versão atualmente instalada é...**|**E você quiser...**|**Baixar e instalar...**|  
|Instalações de 32 bits:|||  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 32 bits do SQL Server 2012 SP2|**SQLServer2012SP2-KB2958429-**<arch>**-**<lang id>**.exe** da [página de download do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Uma versão de 32 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 32 bits do SQL Server 2012 Express SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de somente ferramentas do cliente e de gerenciamento para SQL Server 2012 (incluindo SQL Server 2012 Management Studio)|Atualizar o cliente e as ferramentas de gerenciamento para a versão de 32 bits do SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits do SQL Server 2012 Management Studio Express|Atualizar para a versão de 32 bits do SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de qualquer edição do SQL Server 2012 e uma versão de 32 bits do cliente e das ferramentas de gerenciamento (incluindo SQL Server 2012 RTM Management Studio)|Atualizar todos os produtos para a versão de 32 bits do SQL Server 2012 SP2|**SQLEXPRADV_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express.](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 32 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) ou [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Atualizar as ferramentas para a versão de 32 bits do Microsoft SQL Server 2012 SP2 Feature Pack|Uma ou mais ferramentas na página de download do Microsoft [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|  
|Instalações de 64 bits:|||  
|Uma versão de 64 bits de qualquer edição do SQL Server 2012|Atualizar para a versão de 64 bits do SQL Server 2012 SP2|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe da [página de download do SQL Server 2012 SP2](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|Uma versão de 64 Bits do SQL Server 2012 RTM Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP2|**SQLEXPR_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits com somente o cliente e as ferramentas de gerenciamento para SQL Server 2012 SQL (incluindo SQL Server 2012 Management Studio)|Atualizar as ferramentas de cliente e gerenciamento para a versão de 64 bits do SQL Server 2012 SP2|**SQLEXPRWT_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits do SQL Server 2012 Management Studio Express|Atualizar para a versão de 64 bits do SQL Server 2012 SP2 Management Studio Express|**SQLManagementStudio_**<arch>**_**<lang>**.msi** da [página de download do SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|Uma versão de 64 bits de uma ou mais ferramentas do [Microsoft SQL Server 2012 RTM Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065) ou [Microsoft SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)|Atualizar as ferramentas para a versão de 64 bits do Microsoft SQL Server 2012 SP2 Feature Pack|Uma ou mais ferramentas na página de download do Microsoft [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)|  
  

