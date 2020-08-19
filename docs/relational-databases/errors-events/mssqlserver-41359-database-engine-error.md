---
description: MSSQLSERVER_41359
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5de7dc505b2c9ab2c56a4f830dd456acf988f00a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424328"
---
# <a name="mssqlserver_41359"></a>MSSQLSERVER_41359
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41359|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|Texto da mensagem|Uma consulta que acessa as tabelas com otimização de memória usando o nível de isolamento READ COMMITTED não pode acessar as tabelas baseadas em disco quando a opção READ_COMMITTED_SNAPSHOT do banco de dados é definida como ON. Forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica de tabela, como WITH (SNAPSHOT).|  
  
## <a name="explanation"></a>Explicação  
O banco de dados com READ_COMMITTED_SNAPSHOT=ON não oferece suporte a transações que acessam tabelas com otimização de memória e tabelas baseadas em disco.  
  
## <a name="user-action"></a>Ação do usuário  
Defina READ_COMMITTED_SNAPSHOT como OFF ou forneça um nível de isolamento com suporte para a tabela com otimização de memória usando uma dica no nível de tabela, como WITH (SNAPSHOT). Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
