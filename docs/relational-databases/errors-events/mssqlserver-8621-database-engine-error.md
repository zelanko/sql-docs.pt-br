---
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1bae7c376307aee10024fba364ba1a2fe9eabd01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678204"
---
# <a name="mssqlserver8621"></a>MSSQLSERVER_8621
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|8621|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|OPTIMIZER_STACK_OVERFLOW_ERR|  
|Texto da mensagem|O processador de consultas ficou sem espaço de pilha suficiente durante a otimização da consulta. Simplifique a consulta.|  
  
## <a name="explanation"></a>Explicação  
É provável que a causa do erro seja o tamanho da consulta expandida. A consulta expandida substitui na consulta original as definições de cada uma das exibições, colunas computadas, funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e expressões de tabela comuns a que faz referência, além de ações em cascata, como atualizar índices secundários, exibições e gatilhos.  
  
É provável que a consulta seja grande em alguma dimensão; por exemplo, o número de tabelas referenciadas por definições de exibição ou uma expressão escalar muito grande.  
  
## <a name="user-action"></a>Ação do usuário  
Simplifique a consulta dividindo-a em várias consultas na dimensão maior. Primeiro remova todos os elementos da consulta que não são de fato necessários e, depois, tente adicionar uma tabela temporária e dividir a consulta em duas.  Apenas mover uma parte da consulta para uma subconsulta, função ou expressão de tabela comum não é suficiente, porque elas são recombinadas pelo compilador [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
