---
title: Acessando tipos definidos pelo usuário no ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62ae1ba46066a71d874dd63cc6e18a4a88960465
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349268"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tipos definidos pelo usuário (UDTs) são escritos usando qualquer um dos idiomas com suporte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] do .NET Framework CLR (CLR) que produzem código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como definição da coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] lote, ou como um argumento de uma [!INCLUDE[tsql](../../includes/tsql-md.md)] função ou procedimento armazenado.  
  
 No ADO.NET, o **System.Data.SqlClient** provedor expõe UDTs das seguintes maneiras:  
  
-   Por meio de **SqlDataReader** como um objeto.  
  
-   Por meio de **SqlDataReader** como bytes brutos.  
  
-   Como um parâmetro de um **SqlParameter** objeto.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Recuperando dados UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Descreve como recuperar dados UDT e como especificar parâmetros.  
  
 [Atualizando colunas UDT com DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Descreve como trabalhar com UDTs em **DataSets** e como atualizar dados UDT usando **DataAdapters**.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos definidos pelo usuário do CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
