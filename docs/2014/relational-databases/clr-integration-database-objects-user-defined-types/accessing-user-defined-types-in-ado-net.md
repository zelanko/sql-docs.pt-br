---
title: Acessando tipos definidos pelo usuário no ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c4266cde6caa32aaee9eeabc5ead52dfd94bbd14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116382"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
  Tipos definidos pelo usuário (UDTs) são gravados usando qualquer um dos idiomas com suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] common language runtime .NET Framework (CLR) que produzem código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como a definição de coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes, ou como um argumento de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] função ou procedimento armazenado.  
  
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
  
  