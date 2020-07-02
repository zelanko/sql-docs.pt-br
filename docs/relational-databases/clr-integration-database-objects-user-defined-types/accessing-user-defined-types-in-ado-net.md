---
title: Acessando tipos definidos pelo usuário em ADO.NET | Microsoft Docs
description: Os UDTs, escritos em .NET Framework linguagens CLR, permitem que um banco de dados SQL Server armazene objetos e estruturas de dado personalizadas. No ADO.NET, um provedor expõe UDTs.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: cbbff72ab506238ec2134da8a91f91e3a315eb3f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727854"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Os tipos definidos pelo usuário (UDTs) são escritos usando qualquer um dos idiomas compatíveis com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) que produz código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
 No ADO.NET, o provedor **System. Data. SqlClient** expõe UDTs das seguintes maneiras:  
  
-   Por meio de **System. Data. SqlClient. SqlDataReader** como um objeto.  
  
-   Por meio do **SqlDataReader** como bytes brutos.  
  
-   Como um parâmetro de um objeto **System. Data. SqlClient. SqlParameter** .  
  
## <a name="in-this-section"></a>Nesta seção  
 [Recuperando dados UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Descreve como recuperar dados UDT e como especificar parâmetros.  
  
 [Atualizando colunas UDT com DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Descreve como trabalhar com UDTs em **DataSets** e como atualizar dados UDT usando **DataAdapters**.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
