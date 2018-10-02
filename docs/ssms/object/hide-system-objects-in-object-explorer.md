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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18033b708c4ea909d941c5ceb01aca1f6caaab9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640746"
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
  
