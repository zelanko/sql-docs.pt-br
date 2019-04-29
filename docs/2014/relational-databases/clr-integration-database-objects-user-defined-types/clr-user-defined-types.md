---
title: Tipos CLR definidos pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7044fdc4c29110870e20cd2f9fe4f2140659e551
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874434"
---
# <a name="clr-user-defined-types"></a>Tipos CLR definidos pelo usuário
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá a possibilidade para criar objetos de banco de dados programados em um assembly criado no CLR (Common Language Runtime) do .NET Framework. Os objetos do banco de dados que podem usufruir o modelo de programação avançado fornecido pelo CLR incluem gatilhos, procedimentos armazenados, funções, funções de agregação e tipos.  
  
> [!NOTE]  
>  Por padrão, a possibilidade de executar código do CLR está definida como OFF no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O CLR pode ser habilitado usando o **sp_configure** procedimento armazenado do sistema.  
  
 Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], você pode usar tipos definidos pelo usuário (UDTs) para estender o sistema de tipo escalar do servidor, permitindo o armazenamento de objetos CLR em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. As UDTs podem conter vários elementos e apresentar comportamentos, o que as diferencia dos tipos de dados de alias tradicionais, que consistem em um único tipo de dados de sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Como as UDTs são acessadas pelo sistema como um todo, seu uso em tipos de dados complexos pode apresentar um impacto negativo em relação ao desempenho. Dados complexos costumam ser mais bem modelados usando linhas e tabelas tradicionais. As UDTs do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são bem-apropriadas ao seguinte:  
  
-   Tipos de data, hora, moeda e numéricos estendidos  
  
-   Aplicativos geoespaciais  
  
-   Dados codificados ou criptografados  
  
 O processo de desenvolvimento das UDTs no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste nas seguintes etapas:  
  
1.  **Codifique e compile o assembly que define a UDT.** As UDTs são definidas usando qualquer um dos idiomas com suporte pelo.NET Framework common language runtime (CLR) que produzem código verificável. Isso inclui o Visual C# e o Visual Basic .NET. Os dados são expostos como campos e propriedades de uma classe ou estrutura do .NET Framework, e os comportamentos são definidos pelos métodos da classe ou estrutura.  
  
2.  **Registre o assembly.** As UDTs podem ser implantadas por meio da interface do usuário do Visual Studio em um projeto de banco de dados ou usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY, que copia o assembly que contém a classe ou a estrutura para um banco de dados.  
  
3.  **Crie a UDT no SQL Server.** Uma vez que o assembly está carregado em um banco de dados de host, você usa a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE para criar uma UDT e expor os membros da classe ou da estrutura como membros da UDT. As UDTs só existem no contexto de um único banco de dados e, uma vez registradas, não têm dependências quanto a arquivos externos nos quais foram criados.  
  
    > [!NOTE]  
    >  Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], não havia suporte para UDTs criadas em assemblies do .NET Framework. No entanto, você ainda pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados de alias, usando **sp_addtype**. A sintaxe de CREATE TYPE pode ser usada para criar tanto tipos de dados definidos nativos definidos pelo usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quanto UDTs.  
  
4.  **Criar tabelas, variáveis ou parâmetros usando a UDT** começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], um tipo definido pelo usuário pode ser usado como definição da coluna de uma tabela, como uma variável em uma [!INCLUDE[tsql](../../includes/tsql-md.md)] lote, ou como um argumento de um [!INCLUDE[tsql](../../includes/tsql-md.md)] de função ou armazenados procedimento.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criando um tipo definido pelo usuário](creating-user-defined-types.md)  
 Descreve como criar UDTs.  
  
 [Registrando tipos definidos pelo usuário no SQL Server](registering-user-defined-types-in-sql-server.md)  
 Descreve como registrar e gerenciar UDTs no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Trabalhando com tipos de dados definidos pelo usuário no SQL Server](working-with-user-defined-types-in-sql-server.md)  
 Descreve como criar consultas que usam UDTs.  
  
 [Acessando tipos definidos pelo usuário no ADO.NET](accessing-user-defined-types-in-ado-net.md)  
 Descreve como trabalhar com UDTs que usam o provedor de dados .NET Framework do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ADO.NET.  
  
  
