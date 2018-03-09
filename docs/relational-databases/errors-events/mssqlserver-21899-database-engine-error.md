---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 677f6c5b9a406bdc66d2d92bc696c59c74f77a51
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|21899|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21899|  
|Texto da mensagem|A consulta no publicador redirecionado '%s' para determinar se havia entradas de sysserver para os assinantes do publicador original '%s' falhou com o erro '%d', mensagem de erro '%s'.|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_redirected_publisher** consulta as tabelas de metadados de assinatura do banco de dados publicador no servidor remoto para determinar seus assinantes associados. O erro 21899 será retornado se esta consulta falhar. A consulta de validação requer acesso ao banco de dados publicado no publicador redirecionado. Se o logon especificado quando **sp_adddistpublisher** foi chamado para o publicador original não for autorizado a acessar o banco de dados publicado no publicador redirecionado, o erro 21899 será retornado.  
  
## <a name="user-action"></a>Ação do usuário  
Revise a mensagem de erro citada para determinar a causa da falha e execute a ação corretiva apropriada.  
  
