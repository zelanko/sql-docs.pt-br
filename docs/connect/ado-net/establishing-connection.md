---
title: Estabelecer conexão
description: Diretrizes para se conectar a um SQL Server pelo provedor SqlClient.
ms.date: 11/13/2020
dev_langs:
- csharp
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: cb77d01ede16a6fa68aac6dcb49612ad8fd9a191
ms.sourcegitcommit: 7a3fdd3f282f634f7382790841d2c2a06c917011
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563073"
---
# <a name="establishing-connection"></a>Estabelecer conexão

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para se conectar ao Microsoft SQL Server, use o objeto <xref:Microsoft.Data.SqlClient.SqlConnection> do Provedor de Dados Microsoft SqlClient para SQL Server. Para armazenar e recuperar cadeias de conexão com segurança, confira [Proteger informações de conexão](protecting-connection-information.md).

## <a name="closing-connections"></a>Fechando conexões

É recomendável sempre fechar a conexão quando você terminar de usá-la para que a conexão possa ser retornada ao pool. O bloco `Using` no Visual Basic ou C# automaticamente descarta a conexão quando o código sai do bloco, mesmo no caso de uma exceção sem tratamento. Confira [Instrução using](/dotnet/csharp/language-reference/keywords/using-statement) e [Instrução Using](/dotnet/visual-basic/language-reference/statements/using-statement) para obter mais informações.

Você também pode usar os métodos `Close` ou `Dispose` do objeto de conexão. As conexões que não são fechadas explicitamente não podem ser adicionadas nem retornadas ao pool. Por exemplo, uma conexão que sai de escopo, mas que não foi fechada explicitamente será retornada somente para o pool de conexões se o tamanho do máximo tiver sido atingido e a conexão ainda estiver válida.

> [!NOTE]
> Não chame `Close` ou `Dispose` em um objeto **Connection**, um **DataReader** nem em nenhum outro objeto gerenciado no método `Finalize` de sua classe. Em um finalizador, libere somente recursos não gerenciados que sua classe possui diretamente. Se a classe não tiver nenhum recurso não gerenciado, não inclua um método `Finalize` em sua definição de classe. Para obter mais informações, confira [Coleta de lixo](/dotnet/standard/garbage-collection/index).

> [!NOTE]
> Eventos de logon e logout não serão gerados no servidor quando uma conexão for procurada de ou retornada para o pool de conexões, porque a conexão não é fechada realmente quando é retornada para o pool de conexões. Para obter mais informações, consulte [Pool de Conexões do SQL Server (ADO.NET)](sql-server-connection-pooling.md).

## <a name="connecting-to-sql-server"></a>Conectar-se ao SQL Server

Para obter nomes e valores válidos de formato de cadeia de caracteres, consulte a propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. Você também pode usar a classe <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> para criar cadeias de conexão sintaticamente válidas em tempo de execução. Para obter mais informações, confira [Construtores de cadeias de conexão](connection-string-builders.md).

O exemplo de código a seguir demonstra como criar e abrir uma conexão para um banco de dados do SQL Server.

[!code-csharp[SqlConnection.Open#1](~/../sqlclient/doc/samples/SqlConnection_Open.cs#1)]

### <a name="integrated-security-and-aspnet"></a>Segurança integrada e o ASP.NET

A Segurança integrada do SQL Server (também conhecida como conexões confiáveis) ajuda a fornecer proteção ao se conectar ao SQL Server, pois não expõe uma ID de usuário e senha na cadeia de conexão e é o método recomendado para autenticar uma conexão. A segurança integrada usa a identidade de segurança atual, ou símbolo, do processo em execução. Para aplicativos da área de trabalho, essa identidade normalmente é a identidade do usuário conectado no momento.

A identidade de segurança para aplicativos ASP.NET pode ser definida para uma das várias opções diferentes. Para compreender melhor a identidade de segurança que um aplicativo ASP.NET usa ao se conectar com o SQL Server, confira [Representação do ASP.NET](/previous-versions/aspnet/xh507fc5(v=vs.100)), [Autenticação do ASP.NET](/previous-versions/aspnet/eeyk640h(v=vs.100)) e [Como acessar o SQL Server usando a Segurança integrada do Windows](/previous-versions/aspnet/bsz5788z(v=vs.100)).

## <a name="see-also"></a>Confira também

- [Conectar-se a fontes de dados](connecting-to-data-source.md)
- [Cadeias de conexão](connection-strings.md)
