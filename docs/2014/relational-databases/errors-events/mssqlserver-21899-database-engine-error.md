---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cb1af04b56685d0e1b5a703b812d08d88909b693
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034572"
---
# <a name="mssqlserver_21899"></a>MSSQLSERVER_21899
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21899|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21899|  
|Texto da mensagem|A consulta no publicador redirecionado '%s' para determinar se havia entradas de sysserver para os assinantes do publicador original '%s' falhou com o erro '%d', mensagem de erro '%s'.|  
  
## <a name="explanation"></a>Explicação  
 `sp_validate_redirected_publisher` consulta as tabelas de metadados de assinatura do banco de dados publicador no servidor remoto para determinar seus assinantes associados. O erro 21899 será retornado se esta consulta falhar. A consulta de validação requer acesso ao banco de dados publicado no publicador redirecionado. Se o logon tiver especificado quando `sp_adddistpublisher` foi chamado, o publicador original não será autorizado a acessar o banco de dados publicado no publicador redirecionado; o erro 21899 será retornado.  
  
## <a name="user-action"></a>Ação do usuário  
 Revise a mensagem de erro citada para determinar a causa da falha e execute a ação corretiva apropriada.  
  
  
