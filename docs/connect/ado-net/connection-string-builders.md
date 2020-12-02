---
title: Construtores de cadeia de conexão
description: Saiba mais sobre as classes de construtores de cadeias de conexão usadas por diferentes provedores no ADO.NET, todas herdadas de DbConnectionStringBuilder.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 8434b608-c4d3-43d3-8ae3-6d8c6b726759
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 74031c0c3711ce768b919692fde0cb687060f227
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126338"
---
# <a name="connection-string-builders"></a>Construtores de cadeia de conexão

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Nas versões anteriores do ADO.NET, não existia a verificação de cadeias de conexão com valores de cadeia concatenados no tempo de compilação. Portanto, no tempo de execução, uma palavra-chave incorreta gerava uma <xref:System.ArgumentException>. O Provedor de Dados do Microsoft SqlClient para SQL Server inclui a classe de construtor de cadeias de conexão fortemente tipada <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=nameWithType>, herdada de <xref:System.Data.Common.DbConnectionStringBuilder>.

## <a name="connection-string-injection-attacks"></a>Ataques de injeção de cadeias de conexão

Um ataque de injeção de cadeia de conexão pode ocorrer quando a concatenação de cadeias dinâmicas é usada para criar cadeias de conexão com base na entrada do usuário. Se a cadeia de caracteres não for validada e o texto mal-intencionado ou os caracteres não forem escapados, um invasor poderá potencialmente acessar dados confidenciais ou outros recursos no servidor. Por exemplo, um invasor pode montar um ataque fornecendo um ponto e vírgula e acrescentando outro valor. A cadeia de conexão é analisada usando um algoritmo "**o último ganha**", e a entrada hostil é substituída por um valor legítimo.

As classes de construtores de cadeias de conexão são criadas para eliminar hipóteses e proteger contra erros de sintaxe e vulnerabilidades à segurança. Elas fornecem métodos e propriedades correspondentes aos pares chave-valor conhecidos e permitidos pelo provedor de dados. Cada classe mantém uma coleção fixa de sinônimos e pode converter um sinônimo no nome da chave conhecida correspondente. As verificações são executadas para pares chave-valor válidos e um par inválido gera uma exceção. Além disso, os valores injetados são tratados de maneira segura.

O exemplo a seguir demonstra como <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> trata um valor adicional inserido para a configuração `Initial Catalog`.

[!code-csharp[SqlConnectionStringBuilder_InjectionAttack#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_InjectionAttack.cs#1)]

A saída mostra que o <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> o tratou corretamente por meio do escape do valor extra entre aspas duplas em vez de anexá-lo à cadeia de conexão como um novo par chave-valor.

```output
data source=(local);Integrated Security=True;
initial catalog="AdventureWorks;NewValue=Bad"
```

## <a name="building-connection-strings-from-configuration-files"></a>Construindo cadeias de conexão a partir de arquivos de configuração

Se determinados elementos de uma cadeia de conexão forem conhecidos antecipadamente, eles poderão ser armazenados em um arquivo de configuração e recuperados em tempo de execução para construir uma cadeia de conexão completa. Por exemplo, o nome do banco de dados pode ser conhecido com antecedência, mas não o nome do servidor. Ou, talvez, você deseje que um usuário forneça um nome e uma senha em tempo de execução, sem que possa injetar outros valores na cadeia de conexão.

Um dos construtores sobrecarregados de um construtor de cadeias de conexão obtém um <xref:System.String> como argumento, o que permite a você fornecer uma cadeia de conexão parcial que depois poderá ser concluída pela entrada do usuário. A cadeia de conexão parcial pode ser armazenada em um arquivo de configuração e recuperada em tempo de execução.

> [!NOTE]
> O namespace <xref:System.Configuration> permite acesso programático aos arquivos de configuração que usam <xref:System.Web.Configuration.WebConfigurationManager> para aplicativos Web e <xref:System.Configuration.ConfigurationManager> para aplicativos do Windows. Para saber mais sobre como trabalhar com cadeias de conexão e arquivos de configuração, confira [Cadeias de conexão e arquivos de configuração](connection-strings-and-configuration-files.md).

### <a name="example"></a>Exemplo

Este exemplo demonstra como recuperar uma cadeia de conexão parcial de um arquivo de configuração e concluí-la definindo as propriedades <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>, <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserID%2A> e <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.Password%2A> do <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>. O arquivo de configuração é definido como a seguir.

```xml
<connectionStrings>
  <clear/>
  <add name="partialConnectString"
    connectionString="Initial Catalog=Northwind;"
    providerName="Microsoft.Data.SqlClient" />
</connectionStrings>
```

> [!NOTE]
> Você deve definir uma referência à `System.Configuration.dll` em seu projeto para que o código seja executado.

[!code-csharp[DataWorks SqlConnectionStringBuilder.UserNamePwd#1](~/../sqlclient/doc/samples/SqlConnectionStringBuilder_UserNamePwd.cs#1)]
  
## <a name="see-also"></a>Confira também

- [Cadeias de conexão](connection-strings.md)
