---
title: SDK de extensibilidade da Microsoft para Java para SQL Server
description: Como implementar um programa Java para SQL Server usando o SDK de extensibilidade da Microsoft para Java.
ms.prod: sql
ms.technology: language-extensions
ms.date: 08/21/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f2c1e7eb5b5410ad0c12b8dec6f451b7572f0e36
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "73588790"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>SDK de extensibilidade da Microsoft para Java para SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como implementar um programa Java para SQL Server usando o SDK de extensibilidade da Microsoft para Java. O SDK é uma interface para a extensão de linguagem Java que é usado para trocar dados com SQL Server e para executar código Java do SQL Server.

O SDK é instalado como parte do SQL Server 2019 versão Release Candidate 1 no Windows e no Linux:

+ Caminho de instalação padrão no Windows: **[diretório base de instalação da instância]\MSSQL\Binn\mssql-java-lang-extension.jar**
+ Caminho de instalação padrão no Linux: **/opt/mssql/lib/mssql-java-lang-extension.jar**

O código é de software livre e pode ser encontrado no [Repositório GitHub de Extensões de Linguagem do SQL Server](https://github.com/microsoft/sql-server-language-extensions).

## <a name="implementation-requirements"></a>Requisitos de implementação

A interface do SDK define um conjunto de requisitos que precisam ser atendidos para que o SQL Server se comunique com o runtime do Java. Para usar o SDK, você precisa seguir algumas regras de implementação em sua classe principal. O SQL Server pode executar um método específico na classe Java e trocar dados usando a extensão de linguagem Java.

Para obter um exemplo de como você pode usar o SDK, confira o [Tutorial: Pesquisar uma cadeia de caracteres usando regex (expressões regulares) em Java](../tutorials/search-for-string-using-regular-expressions-in-java.md).

## <a name="sdk-classes"></a>Classes de SDK

O SDK consiste em três classes.

Duas classes abstratas que definem a interface que a extensão Java usa para trocar dados com o SQL Server:

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

A terceira classe é uma classe auxiliar, que contém uma implementação de um objeto de conjunto de dados. É uma classe opcional que você pode usar, o que torna mais fácil começar. Você também pode usar sua própria implementação de uma classe desse tipo.

- **PrimitiveDataset**

Abaixo, você encontrará descrições de cada classe no SDK. O código-fonte das classes de SDK está disponível no [Repositório GitHub de extensões de linguagem do SQL Server](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/java/sdk).

### <a name="class-abstractsqlserverextensionexecutor"></a>Classe: AbstractSqlServerExtensionExecutor

A classe abstrata **AbstractSqlServerExtensionExecutor** contém a interface usada para executar o código Java pela extensão de linguagem Java para SQL Server.

Sua classe Java principal precisa herdar dessa classe. Herdar dessa classe significa que há certos métodos na classe que você precisa implementar em sua própria classe.

Para herdar dessa classe abstrata, você estende com o nome da classe abstrata na declaração de classe:

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

No mínimo, sua classe principal precisa implementar o método execute(...).

#### <a name="method-execute"></a>Método Execute

O método Execute é o método que é chamado no SQL Server por meio da extensão de linguagem Java para invocar o código Java do SQL Server. É um método-chave em que você inclui as operações principais que deseja executar no SQL Server.

Para passar argumentos de método para o Java no SQL Server, use o parâmetro `@param` no `sp_execute_external_script`. O método **execute** recebe argumentos dessa maneira.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

#### <a name="method-init"></a>Método Init

O método Init é executado após o construtor e antes do método Execute. Todas as operações que precisam ser executadas antes do execute(...) podem ser feitas neste método.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="class-abstractsqlserverextensiondataset"></a>Classe: AbstractSqlServerExtensionDataset

A classe abstrata **AbstractSqlServerExtensionDataset** contém a interface para manipular dados de entrada e saída usados pela extensão Java.


### <a name="class-primitivedataset"></a>Classe: PrimitiveDataset

A classe **PrimitiveDataset** é uma implementação de **AbstractSqlServerExtensionDataset** que armazena tipos simples como matrizes primitivas.

Ela é fornecida no SDK simplesmente como uma classe auxiliar opcional. Se você não usar essa classe, precisará implementar sua própria classe que herda de **AbstractSqlServerExtensionDataset**.  

## <a name="next-steps"></a>Próximas etapas

+ [Tutorial: Pesquisar uma cadeia de caracteres usando regex (expressões regulares) em Java](../tutorials/search-for-string-using-regular-expressions-in-java.md)
+ [Como chamar Java no SQL Server](call-java-from-sql.md)
