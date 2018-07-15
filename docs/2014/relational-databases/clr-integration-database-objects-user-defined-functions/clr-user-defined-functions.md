---
title: Funções CLR definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
caps.latest.revision: 45
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fbdb8fad94b76b0f9f30dde59896caebd8603c10
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349228"
---
# <a name="clr-user-defined-functions"></a>Funções CLR definidas pelo usuário
  As funções definidas pelo usuário são rotinas que podem obter parâmetros, executar cálculos ou outras ações e retornar um resultado. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], é possível escrever funções definidas pelo usuário em qualquer linguagem de programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Há dois tipos de funções: escalar, que retorna um único valor, e com valor de tabela, que retorna um conjunto de linhas.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Funções de valor escalar do CLR](clr-scalar-valued-functions.md)  
 Abrange requisitos de implementação e exemplos de funções com valor escalar.  
  
 [Funções com valor de tabela do CLR](clr-table-valued-functions.md)  
 Aborda como implementar e usar funções com valor de tabela (TVFs), além das diferenças entre TVFs CLR e [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Agregações do CLR definidas pelo usuário](clr-user-defined-aggregates.md)  
 Descreve como implementar e usar agregações definidas pelo usuário.  
  
## <a name="see-also"></a>Consulte também  
 [Funções definidas pelo usuário](../user-defined-functions/user-defined-functions.md)  
  
  
