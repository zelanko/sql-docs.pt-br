---
title: Assemblies (mecanismo de banco de dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 157f43f4646c6c935da7884a0fdae93c9676e6fe
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37354958"
---
# <a name="assemblies-database-engine"></a>Assemblies (Mecanismo de Banco de Dados)
  Os tópicos desta seção fornecem informações para ajudá-lo a entender, projetar e implementar assemblies.  
  
 Assemblies são arquivos DLL usados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para implantar funções, procedimentos armazenados, gatilhos, agregações definidas pelo usuário e tipos definidos pelo usuário que são escritos em uma das linguagens de código gerenciado hospedadas pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] runtime de linguagem comum (CLR), em vez de usar [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Um assembly no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é um objeto que faz referência a um módulo de aplicativo gerenciado (arquivo .dll) criado em CLR do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Um assembly contém metadados de classe e código gerenciado. Carregar um assembly para uma instância do SQL Server é a primeira etapa da criação de qualquer um dos objetos de banco de dados a seguir:  
  
-   Funções CLR. Para obter mais informações, consulte [criar funções de CLR](../user-defined-functions/create-clr-functions.md).  
  
-   Procedimentos armazenados CLR Para obter mais informações, consulte [procedimentos armazenados CLR](../../database-engine/dev-guide/clr-stored-procedures.md).  
  
-   Gatilhos CLR. Para obter mais informações, consulte [criar gatilhos de CLR](../triggers/create-clr-triggers.md).  
  
-   Funções de agregação definidas pelo usuário. Para obter mais informações, consulte [agregações definidas pelo usuário criar](../user-defined-functions/create-user-defined-aggregates.md).  
  
-   Tipos definidos pelo usuário. Para obter mais informações, consulte [Using User-Defined tipos](../native-client/features/using-user-defined-types.md).  
  
 Os assemblies executam as funções a seguir no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Contêm o código gerenciado que executa a funcionalidade de um ou mais dos objetos de banco de dados CLR listados anteriormente.  
  
-   Contêm metadados que incluem o número de versão e cultura do assembly, uma chave pública opcional que identifica exclusivamente a lista de classes do assembly, os métodos definidos no assembly e a arquitetura do processador do assembly.  
  
-   Gerenciam nível de acesso do código gerenciado a recursos externos, regulando permissões de acesso a código.  
  
-   Contêm metadados sobre dependências em outros assemblies referenciados pelo assembly.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Criação de Assemblies](assemblies-designing.md)|Explica o que levar em consideração antes de criar um assembly. Inclui assemblies de empacotamento, permissões de acesso a código e outras restrições.|  
|[Implementando assemblies](assemblies-implementing.md)|Explica como criar e eliminar assemblies, como e quando modificar assemblies e como recuperar metadados sobre assemblies.|  
|[Obtendo informações sobre assemblies](assemblies-getting-information.md)|Lista as exibições do catálogo e funções que podem ser consultadas para metadados sobre assemblies.|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
