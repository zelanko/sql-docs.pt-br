---
title: Cenários de uso e exemplos para integração Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155013"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>Cenários de uso e exemplos para a integração de CLR (Common Language Runtime)
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui aplicativos de exemplo, exemplos de pacote e vários exemplos de codificação que você pode usar para conhecer os recursos de programação da integração CLR (common language runtime).  
  
 Para projetos completos do Visual Studio implementando esses exemplos e materiais adicionais, visite [Microsoft SQL Server Community Projects & Samples CodePlex](https://go.microsoft.com/fwlink/?LinkID=193935).  
  
|Nome|Descrição|  
|----------|-----------------|  
|[Acessando código nativo em uma UDF CLR](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|Mostra como invocar uma função em código C++ nativo (não gerenciado) a partir de uma função definida pelo usuário em um assembly, no seu banco de dados.|  
|[Exemplo de parâmetro de matriz](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|Demonstra como criar, atualizar ou excluir um conjunto de linhas em um banco de dados, passando uma matriz de informações de um cliente para um procedimento armazenado de integração CLR no servidor. Isso é feito com um UDT.|  
|[Exemplo de UDT de reconhecimento de calendário data e hora](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|Define dois UDTs que fornecem controle de datas e horas com reconhecimento de calendário.|  
|[Exemplo de transações CLR](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|Demonstra como controlar transações por meio de as APIs gerenciadas localizadas no namespace System.Transactions.|  
|[Criação de Contact usando CLR e XML](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|O exemplo Contact do SQL Server fornece alguns utilitários úteis que formam uma camada de funcionalidade extra no banco de dados de exemplo base AdventureWorks2012. O primeiro utilitário cria registros de contato para vários tipos de pessoas envolvidas no banco de dados AdventureWorks2012. As informações de contato são especificadas por meio de XML e são passadas para um procedimento armazenado baseado no C# ou no VB para criar o XML e colocá-las nas tabelas adequadas no banco de dados.|  
|[Função de conversão e tipo de moeda](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|Define um tipo de dados Currency definido pelo usuário por meio do C#.|  
|[Manipulando objetos grandes usando CLR](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|Demonstra a transferência de LOBs (objetos binários grandes) entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um sistema de arquivos acessível ao servidor usando procedimentos armazenados CLR.|  
|[Exemplo pronto do Olá, Mundo](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|Demonstra as operações básicas para criar, implantar e testar um procedimento armazenado internacionalizado simples baseado na integração CLR.|  
|[Exemplo Olá, Mundo](../../../2014/database-engine/dev-guide/hello-world-sample.md)|Demonstra as operações básicas para criar, implantar e testar um procedimento armazenado baseado em integração CLR simples.|  
|[Exemplo de acesso a dados em processo](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|Contém várias funções simples que demonstram vários recursos do provedor de acesso de dados CLR em processo.|  
|[Exemplo de conjunto de resultados](../../../2014/database-engine/dev-guide/result-set-sample.md)|Demonstra como executar comandos durante a leitura dos resultados de uma consulta, sem abrir uma nova conexão e sem ler todos os resultados na memória.|  
|[Exemplo Send DataSet](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|Demonstra como retornar um conjunto de dados baseado no ADO.NET em um procedimento armazenado de servidor baseado em CLR como um conjunto de resultados para o cliente.|  
|[Exemplo Funções de utilitário de cadeia de caracteres](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|Contém uma TVF (função com valor de tabela) de fluxo, escrita em Visual C# e Visual Basic, que divide uma cadeia de caracteres separada por vírgulas em uma tabela com uma coluna.|  
|[Exemplo de manipulação de cadeias de caracteres com reconhecimento de suplementares](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|Mostra a implementação de cinco funções de cadeia de caracteres do [!INCLUDE[tsql](../../includes/tsql-md.md)] com reconhecimento de suplementares que podem tratar cadeias de caracteres Unicode e substitutas.|  
|[Utilitários UDT](../../../2014/database-engine/dev-guide/udt-utilities.md)|Contém várias funções de UDT (utilitário de tipo de dados definido pelo usuário).|  
|[Limpeza de assembly não usado](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|Contém um procedimento armazenado .NET que exclui assemblies não usados no banco de dados atual por meio de consulta dos catálogos de metadados.|  
|[Tipo Definido pelo Usuário](../../../2014/database-engine/dev-guide/user-defined-type.md)|Mostra a criação e o uso de um UDT simples no [!INCLUDE[tsql](../../includes/tsql-md.md)] e em um aplicativo cliente por meio de System.Data.SqlClient.|  
|[UTF8 Tipo de dados definido pelo usuário de cadeia de caracteres &#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|Demonstra a implementação de um UDT que estende o sistema de tipos do banco de dados para fornecer armazenamento de valores UTF8 codificados.|  
  
  
