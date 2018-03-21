---
title: "Programação do procedimento armazenado estendido do Mecanismo de Banco de Dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], programming
- stored procedures [SQL Server], extended
- Database Engine [SQL Server], stored procedures
- macros [SQL Server]
- Extended Stored Procedure API [SQL Server]
ms.assetid: 158a6765-0542-4e84-b5ab-f173d946ef5e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ab25407220d400923cb48e3cc77c4e54326488c8
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="database-engine-extended-stored-procedure-programming"></a>Programação do procedimento armazenado estendido do mecanismo do banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR. Para obter mais informações, consulte [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 A API de procedimento armazenado estendido do [!INCLUDE[msCoName](../includes/msconame-md.md)] fornece uma API (interface de programação de aplicativo) com base no servidor para estender a funcionalidade do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A API consiste em funções e macros do C e do C++ usadas para compilar aplicativos nas seguintes categorias: procedimentos armazenados estendidos e aplicativos de gateway.  
  
 Os procedimentos armazenados estendidos permitem que você crie suas próprias rotinas externas em uma linguagem de programação, como C. Os procedimentos armazenados estendidos aparecem para o usuário como procedimentos armazenados comuns e são executados como estes. Os parâmetros podem ser passados a procedimentos armazenados estendidos e eles podem retornar resultados e status.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Programando procedimentos armazenados estendidos](../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)  
 Explica como criar, gerenciar e usar procedimentos armazenados estendidos.  
  
 [Referência do programador de procedimentos armazenados estendidos](../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
 Contém tópicos de referência da API de procedimento armazenado estendido.  
  
  
