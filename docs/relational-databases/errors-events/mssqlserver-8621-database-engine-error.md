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
ms.openlocfilehash: 60e0dac3f266a3f2bdd2b7135f987619a7bc5ab7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727486"
---
# <a name="mssqlserver_8621"></a>MSSQLSERVER_8621
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|8621|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|OPTIMIZER_STACK_OVERFLOW_ERR|  
|Texto da mensagem|O processador de consultas ficou sem espaço de pilha suficiente durante a otimização da consulta. Simplifique a consulta.|  
  
## <a name="explanation"></a>Explicação  
É provável que a causa do erro seja o tamanho da consulta expandida. A consulta expandida substitui na consulta original as definições de cada uma das exibições, colunas computadas, funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e expressões de tabela comuns a que faz referência, além de ações em cascata, como atualizar índices secundários, exibições e gatilhos.  
  
É provável que a consulta seja grande em alguma dimensão; por exemplo, o número de tabelas referenciadas por definições de exibição ou uma expressão escalar muito grande.  
  
## <a name="user-action"></a>Ação do usuário  
Simplifique a consulta dividindo-a em várias consultas na dimensão maior. Primeiro remova todos os elementos da consulta que não são de fato necessários e, depois, tente adicionar uma tabela temporária e dividir a consulta em duas.  Apenas mover uma parte da consulta para uma subconsulta, função ou expressão de tabela comum não é suficiente, porque elas são recombinadas pelo compilador [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
