---
title: "Acessando tipos definidos pelo usuário no ADO.NET | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 267f7513c3cc7342106b04232c137ffdd1621cf9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Tipos definidos pelo usuário (UDTs) são gravados usando qualquer um dos idiomas com suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] common language runtime .NET Framework (CLR) que produzem código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como a definição de coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes, ou como um argumento de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] função ou procedimento armazenado.  
  
 No ADO.NET, o **SqlClient** provedor expõe UDTs das seguintes maneiras:  
  
-   Por meio de **System.Data.SqlClient.SqlDataReader** como um objeto.  
  
-   Por meio de **SqlDataReader** como bytes brutos.  
  
-   Como um parâmetro de um **SqlParameter** objeto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Recuperando dados UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Descreve como recuperar dados UDT e como especificar parâmetros.  
  
 [Atualizando colunas UDT com DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Descreve como trabalhar com UDTs em **conjuntos de dados** e como atualizar dados UDT usando **DataAdapters**.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos definidos pelo usuário do CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
