---
title: Acessando tipos definidos pelo usuário no ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 893b2c69a20974bb379cc032f442e5fcb3525ec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919681"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
  Tipos definidos pelo usuário (UDTs) são escritos usando qualquer um dos idiomas com suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] do .NET Framework CLR (CLR) que produzem código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
 No ADO.NET, o provedor `System.Data.SqlClient` expõe UDTs dos seguintes modos:  
  
-   Por meio do `System.Data.SqlClient.SqlDataReader` como um objeto.  
  
-   Por meio do `SqlDataReader` como bytes brutos.  
  
-   Como um parâmetro de um objeto `System.Data.SqlClient.SqlParameter`.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Recuperando dados UDT](accessing-user-defined-types-retrieving-udt-data.md)  
 Descreve como recuperar dados UDT e como especificar parâmetros.  
  
 [Atualizando colunas UDT com DataAdapters](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Descreve como trabalhar com UDTs em `DataSets` e como atualizar dados UDT usando `DataAdapters`.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos definidos pelo usuário do CLR](clr-user-defined-types.md)  
  
  
