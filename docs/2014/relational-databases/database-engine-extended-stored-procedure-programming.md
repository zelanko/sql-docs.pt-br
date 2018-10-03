---
title: Programação do procedimento armazenado estendido do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], programming
- stored procedures [SQL Server], extended
- Database Engine [SQL Server], stored procedures
- macros [SQL Server]
- Extended Stored Procedure API [SQL Server]
ms.assetid: 158a6765-0542-4e84-b5ab-f173d946ef5e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 94be87d9dc0725961200af983e79bc608a2056f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100606"
---
# <a name="database-engine-extended-stored-procedure-programming"></a>Programação do procedimento armazenado estendido do mecanismo do banco de dados
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR. Para obter mais informações, consulte [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 A API de procedimento armazenado estendido do [!INCLUDE[msCoName](../includes/msconame-md.md)] fornece uma API (interface de programação de aplicativo) com base no servidor para estender a funcionalidade do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A API consiste em funções e macros do C e do C++ usadas para compilar aplicativos nas seguintes categorias: procedimentos armazenados estendidos e aplicativos de gateway.  
  
 Os procedimentos armazenados estendidos permitem que você crie suas próprias rotinas externas em uma linguagem de programação, como C. Os procedimentos armazenados estendidos aparecem para o usuário como procedimentos armazenados comuns e são executados como estes. Os parâmetros podem ser passados a procedimentos armazenados estendidos e eles podem retornar resultados e status.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Programando procedimentos armazenados estendidos](extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)  
 Explica como criar, gerenciar e usar procedimentos armazenados estendidos.  
  
 [Referência do programador de procedimentos armazenados estendidos](extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
 Contém tópicos de referência da API de procedimento armazenado estendido.  
  
  
