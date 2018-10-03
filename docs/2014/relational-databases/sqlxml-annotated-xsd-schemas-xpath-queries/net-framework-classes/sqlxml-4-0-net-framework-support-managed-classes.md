---
title: Classes gerenciadas SQLXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- .NET Framework [SQLXML], Managed Classes
- SQL Server .NET Data Provider
- Managed Classes [SQLXML], about managed classes
- providers [SQLXML], SQL Server .NET Data Provider
- data providers [SQLXML], SQL Server .NET Data Provider
- Managed Classes [SQLXML]
- XML [SQLXML]
- SQLXML Managed Classes
- providers [SQLXML], SQLXML Managed Classes
- data providers [SQLXML], SQLXML Managed Classes
- SQLXML, Managed Classes
ms.assetid: 73a5faeb-dabf-4895-acb5-a9651b646065
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1809e1e075f39f3785e0ceb6116683d3824ed0b2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197376"
---
# <a name="sqlxml-managed-classes"></a>Classes gerenciadas SQLXML
  As classes gerenciadas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML expõem a funcionalidade do SQLXML 4.0 dentro do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Com as classes gerenciadas SQLXML, você pode escrever um aplicativo C# para acessar dados XML de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], trazer os dados para o ambiente .NET Framework, processar os dados e enviar as atualizações de volta para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como um DiffGram para aplicar as atualizações. Use um esquema de mapeamento ao aplicar atualizações a um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando classes gerenciadas SQLXML. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 Para usar as classes gerenciadas SQLXML com o SQLXML 4.0, é necessário instalar o Microsoft Visual Studio.  
  
> [!NOTE]  
>  O .NET Framework inclui o .NET Data Provider do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse provedor pode ser usado para acessar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no ambiente .NET; contudo, ele pode tratar somente consultas SQL tradicionais (ou seja, consultas de bancos de dados relacionais com a exceção de consultas XML FOR XML). Não é possível executar modelos XML ou consultas XPath do servidor no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelo do objeto de classes gerenciadas do SQLXML](../../../database-engine/dev-guide/sqlxml-managed-classes-object-model.md)  
 Documenta classes gerenciadas SQLXML e suas propriedades e métodos.  
  
 [Usando as classes gerenciadas do SQLXML](sqlxml-4-0-net-framework-support-managed-classes.md)  
 Fornece exemplos de uso de classes gerenciadas SQLXML.  
  
  
