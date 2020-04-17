---
title: Conjuntos (Motor de Banco de Dados) | Microsoft Docs
description: Uma instância do SQL Server pode hospedar conjuntos que implantam funções, procedimentos, gatilhos e agregados e tipos definidos pelo usuário escritos em uma linguagem CLR.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
ms.openlocfilehash: 386e1980ae19ba4f98222b51a4955b024f815083
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488065"
---
# <a name="assemblies-database-engine"></a>Assemblies (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os tópicos desta seção fornecem informações para ajudá-lo a entender, projetar e implementar assemblies.  
  
 Os conjuntos são arquivos DLL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usados em uma instância de implantação de funções, procedimentos armazenados, gatilhos, agregados definidos pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] usuário e tipos definidos pelo [!INCLUDE[tsql](../../includes/tsql-md.md)]usuário que são gravados em uma das linguagens de código gerenciadas hospedadas pelo tempo de execução do idioma comum (CLR), em vez de em .  
  
 Um assembly no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um objeto que faz referência a um módulo de aplicativo gerenciado (arquivo .dll) criado em CLR do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Um assembly contém metadados de classe e código gerenciado. Carregar um assembly para uma instância do SQL Server é a primeira etapa da criação de qualquer um dos objetos de banco de dados a seguir:  
  
-   Funções CLR. Para obter mais informações, consulte [Criar funções CLR](../../relational-databases/user-defined-functions/create-clr-functions.md).  
  
-   Procedimentos armazenados CLR Para obter mais informações, consulte [CLR Stored Procedures](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33).  
  
-   Gatilhos CLR. Para obter mais informações, consulte [Criar gatilhos CLR](../../relational-databases/triggers/create-clr-triggers.md).  
  
-   Funções de agregação definidas pelo usuário. Para obter mais informações, consulte [Criar agregados definidos pelo usuário](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md).  
  
-   Tipos definidos pelo usuário. Para obter mais informações, confira [Usando tipos definidos pelo usuário](../../relational-databases/native-client/features/using-user-defined-types.md).  
  
 Os assemblies executam as funções a seguir no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Contêm o código gerenciado que executa a funcionalidade de um ou mais dos objetos de banco de dados CLR listados anteriormente.  
  
-   Contêm metadados que incluem o número de versão e cultura do assembly, uma chave pública opcional que identifica exclusivamente a lista de classes do assembly, os métodos definidos no assembly e a arquitetura do processador do assembly.  
  
-   Gerenciam nível de acesso do código gerenciado a recursos externos, regulando permissões de acesso a código.  
  
-   Contêm metadados sobre dependências em outros assemblies referenciados pelo assembly.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criação de Assemblies](../../relational-databases/clr-integration/assemblies-designing.md)|Explica o que levar em consideração antes de criar um assembly. Inclui assemblies de empacotamento, permissões de acesso a código e outras restrições.|  
|[Implementando assemblies](../../relational-databases/clr-integration/assemblies-implementing.md)|Explica como criar e eliminar assemblies, como e quando modificar assemblies e como recuperar metadados sobre assemblies.|  
|[Obtendo informações sobre assemblies](../../relational-databases/clr-integration/assemblies-getting-information.md)|Lista as exibições do catálogo e funções que podem ser consultadas para metadados sobre assemblies.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
