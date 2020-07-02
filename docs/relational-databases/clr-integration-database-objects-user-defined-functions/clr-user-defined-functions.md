---
title: Funções CLR definidas pelo usuário | Microsoft Docs
description: SQL Server integração CLR permite que você crie funções de agregação, valores de tabela e valores de escala definidos pelo usuário em qualquer linguagem de programação de .NET Framework.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: fe481b1a49f8eba69bbf913e49f398c86244b952
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727860"
---
# <a name="clr-user-defined-functions"></a>Funções CLR definidas pelo usuário
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  As funções definidas pelo usuário são rotinas que podem obter parâmetros, executar cálculos ou outras ações e retornar um resultado. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], é possível escrever funções definidas pelo usuário em qualquer linguagem de programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Há dois tipos de funções: escalar, que retorna um único valor, e com valor de tabela, que retorna um conjunto de linhas.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Funções de valor escalar CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-scalar-valued-functions.md)  
 Abrange requisitos de implementação e exemplos de funções com valor escalar.  
  
 [Funções com valor de tabela CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
 Aborda como implementar e usar funções com valor de tabela (TVFs), além das diferenças entre TVFs CLR e [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Agregações CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)  
 Descreve como implementar e usar agregações definidas pelo usuário.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)  
  
  
