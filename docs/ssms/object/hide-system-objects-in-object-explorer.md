---
title: Ocultar objetos do sistema no Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: 5b36198aba754f8424e29ba529fe936516213cad
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102919"
---
# <a name="hide-system-objects-in-object-explorer"></a>Ocultar objetos do sistema no Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este tópico descreve como ocultar objetos do sistema no Pesquisador de Objetos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O nó **Bancos de Dados** do Pesquisador de Objetos contém objetos do sistema, como os bancos de dados do sistema. Use as páginas **Ferramentas**/**Opções** para ocultar os objetos do sistema. Alguns objetos do sistema, como funções de sistema e tipos de dados do sistema, não são afetados por essa configuração.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-hide-system-objects-in-object-explorer"></a>Para ocultar objetos do sistema no Pesquisador de Objetos  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na página **Ambiente/Inicialização** , selecione **Ocultar objetos do sistema no Pesquisador de Objetos**e clique em **OK**.  
  
3.  Na caixa de diálogo **SQL Server Management Studio** , clique em **OK** para reconhecer que o SQL Server Management Studio deve ser reiniciado para que a alteração entre em vigor.  
  
4.  Feche e reabra o SQL Server Management Studio.  
  
