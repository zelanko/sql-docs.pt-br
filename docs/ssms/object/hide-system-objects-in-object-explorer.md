---
title: Ocultar objetos do sistema no Pesquisador de Objetos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- hiding system objects
- system objects [SQL Server]
- objects [SQL Server], hiding
- Object Explorer, hiding objects
ms.assetid: c01d8804-838c-4f75-b78c-80e41e4fffdc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 05864efb35ecd5fcd49e8f8b90cd8093984a9f78
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001949"
---
# <a name="hide-system-objects-in-object-explorer"></a>Ocultar objetos do sistema no Pesquisador de Objetos
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Este tópico descreve como ocultar objetos do sistema no Pesquisador de Objetos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O nó **Bancos de Dados** do Pesquisador de Objetos contém objetos do sistema, como os bancos de dados do sistema. Use as páginas **Ferramentas**/**Opções** para ocultar os objetos do sistema. Alguns objetos do sistema, como funções de sistema e tipos de dados do sistema, não são afetados por essa configuração.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-hide-system-objects-in-object-explorer"></a>Para ocultar objetos do sistema no Pesquisador de Objetos  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na página **Ambiente/Inicialização** , selecione **Ocultar objetos do sistema no Pesquisador de Objetos**e clique em **OK**.  
  
3.  Na caixa de diálogo **SQL Server Management Studio** , clique em **OK** para reconhecer que o SQL Server Management Studio deve ser reiniciado para que a alteração entre em vigor.  
  
4.  Feche e reabra o SQL Server Management Studio.  
  
