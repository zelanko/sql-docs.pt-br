---
description: MSSQLSERVER_15599
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eca555fb3ced04a0258db78c89c53e8cef9d9c20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333812"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|15599|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto da mensagem|Auditoria e permissões não podem ser definidas em objetos temporários locais.|  
  
## <a name="explanation"></a>Explicação  
Auditoria e permissões não têm nenhum efeito quando definidas para objetos temporários locais ou globais. As instruções não resultam em um erro (as operações retornarão com êxito), mas não têm efeito.  
  
Esse comportamento não mudou. No entanto, a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa mensagem informativa alerta o usuário.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhuma ação é necessária, mas considere remover as instruções que tentam definir auditoria ou permissões em objetos temporários locais ou globais.  
  
