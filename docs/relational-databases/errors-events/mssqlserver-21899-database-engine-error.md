---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d84ae2c0694616e9600dca72075dba6a0a8467c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
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
  
