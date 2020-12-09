---
title: Guia de solução de problemas do SqlClient
description: Página que fornece resoluções para problemas comumente observados.
ms.date: 11/27/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 6cad6278eb6ac7b170ee108c1a3510db956ecb22
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96468078"
---
# <a name="sqlclient-troubleshooting-guide"></a>Guia de solução de problemas do SqlClient

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="exceptions-when-connecting-to-sql-server"></a>Exceções na conexão com o SQL Server

Existem vários motivos pelos quais a conexão pode não ser estabelecida. Confira abaixo algumas dicas de solução de problemas que podem ser usadas como um guia para analisar e solucionar vários deles.

### <a name="unable-to-load-native-sni-server-name-indication-library"></a>Não é possível carregar a biblioteca SNI (Indicação de Nome de Servidor) nativa

#### <a name="issues-in-net-framework-applications"></a>Problemas em aplicativos .NET Framework

Rastreamento de pilha observado:

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x64.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

```log
TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
DllNotFoundException: Unable to load DLL 'Microsoft.Data.SqlClient.SNI.x86.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

SNI é a biblioteca nativa do C++ da qual o SqlClient depende para várias operações de rede quando executado no Windows. Em aplicativos .NET Framework criados com o SDK de Projeto do MSBuild, as DLLs nativas não são gerenciadas com comandos de restauração. Portanto, um arquivo ".targets" está incluído no pacote NuGet "Microsoft.Data.SqlClient.SNI" que define as operações de "Cópia" necessárias.

O arquivo ".targets" incluído é referenciado automaticamente quando uma dependência direta é feita para a biblioteca "Microsoft.Data.SqlClient". Em cenários nos quais uma referência transitiva (indireta) é feita, esse arquivo ".targets" deve ser referenciado manualmente para garantir que as operações de "Cópia" possam ser executadas quando necessário.

**Solução recomendada:** verifique se o arquivo ".targets" está referenciado no arquivo ".csproj" do aplicativo para garantir que as operações de "Cópia" sejam executadas.

Esses destinos cobrem apenas aqueles conhecidos e comumente usados pela Microsoft. Se uma ferramenta ou um aplicativo externo definir destinos personalizados para copiar binários, novos destinos deverão ser definidos pelos mantenedores da ferramenta para garantir que DLLs SNI nativas sejam copiadas com os binários Microsoft.Data.SqlClient.dll e estejam disponíveis ao executar aplicativos clientes.

#### <a name="issues-in-net-core-applications"></a>Problemas em aplicativos .NET Core

Rastreamento de pilha observado:

```log
System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.TdsParser' threw an exception.
---> System.TypeInitializationException: The type initializer for 'Microsoft.Data.SqlClient.SNILoadHandle' threw an exception.
---> System.DllNotFoundException: Unable to load shared library 'Microsoft.Data.SqlClient.SNI.dll' or one of its dependencies.
```

> [!NOTE]
> Esse erro pode ocorrer apenas em aplicativos do Windows. Se ele ocorrer em um ambiente Unix, seu aplicativo precisará ser construído para ser direcionado adequadamente a um runtime do Unix, e não ao Windows.

SNI é a biblioteca nativa do C++ da qual o SqlClient depende para várias operações de rede quando executado no Windows. O Microsoft.Data.SqlClient não gerencia o carregamento/descarregamento dessa biblioteca no .NET Core.

**Solução recomendada:** verifique se as permissões "Executar" foram concedidas no sistema de arquivos em que as bibliotecas de runtime nativas são carregadas no processo do .NET Core. Se isso não resolver o problema, você poderá registrar um problema no repositório [dotnet/runtime](https://github.com/dotnet/runtime) para obter mais suporte.

#### <a name="native-sni-pdb-not-found-errors"></a>Erros da SNI nativa (pdb não encontrado)

Rastreamento de pilha observado:

```log
An assembly specified in the application dependencies manifest (sql2csv.deps.json) was not found:
  package: 'Microsoft.Data.SqlClient.SNI.runtime', version: '2.0.0'
  path: 'runtimes/win-x64/native/Microsoft.Data.SqlClient.SNI.pdb'
```

**Solução recomendada:** verifique se o aplicativo cliente faz referência à versão [v2.1.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient/2.1.0) mínima do pacote Microsoft.Data.SqlClient. Ao usar o EF Core, adicione uma referência a essa versão do pacote do Microsoft.Data.SqlClient diretamente para substituir a dependência.

### <a name="hostname-resolution-errors"></a>Erros de resolução de nome do host

Rastreamento de pilha observado:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 0 - No such host is known.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible.
Verify that the instance name is correct and that SQL Server is configured to allow remote connections.
(provider: TCP Provider, error: 35 - An internal exception was caught)
 ---> System.Net.Internals.SocketExceptionFactory+ExtendedSocketException (00000005, 0xFFFDFFFF): Name does not resolve
```

#### <a name="possible-reasons"></a>Possíveis motivos

- O protocolo TCP/Pipes Nomeados não está habilitado no SQL Server

  **Solução recomendada:** habilite o protocolo TCP/Pipes Nomeados na instância do SQL Server por meio do console do SQL Server Configuration Manager.

- Nome do host não conhecido

  **Solução recomendada:** verifique se o nome do host é resolvido para o endereço IP do servidor do cliente em que a conexão está sendo iniciada.


### <a name="login-phase-errors"></a>Erros de fase de logon

Rastreamentos de pilha observados:

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): A connection was successfully established with the server, but then an error occurred during the pre-login handshake.
(provider: SSL Provider, error: 31 - Encryption(ssl/tls) handshake failed)
System.IO.EndOfStreamException: End of stream reached
```

```log
A connection was successfully established with the server, but then an error occurred during the login process.
(provider: SSL Provider, error: 0 - The target principal name is incorrect.)
```

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Connection Timeout Expired. The timeout period elapsed during the post-login phase. The connection could have timed out while waiting for server to complete the login process and respond; Or it could have timed out while attempting to create multiple active connections.
The duration spent while attempting to connect to this server was - [Pre-Login] initialization=837; handshake=394; [Login] initialization=3; authentication=15; [Post-Login] complete=1027;
---> System.ComponentModel.Win32Exception (258): Unknown error 258
at Microsoft.Data.SqlClient.SqlInternalConnection.OnError(SqlException exception, Boolean breakConnection, Action1 wrapCloseInAction)
```

#### <a name="possible-reasons-and-solutions"></a>Possíveis motivos e soluções

- O SQL Server não dá suporte ao TLS 1.2

  Esse erro normalmente ocorre em ambientes de cliente, como contêineres de imagem do Docker, clientes UNIX ou clientes do Windows, em que o TLS 1.2 é o protocolo TLS mínimo com suporte.

  **Solução recomendada:** instale as atualizações mais recentes das versões com suporte do SQL Server<sup>1</sup> e verifique se o protocolo TLS 1.2 está habilitado no servidor.

  _<sup>1</sup> Confira o [Ciclo de vida de suporte do driver SqlClient](sqlclient-driver-support-lifecycle.md) para ver uma lista de versões do SQL Server com suporte em diferentes versões do Microsoft.Data.SqlClient._

  **Solução não segura:** defina as configurações de TLS/SSL no ambiente de cliente/imagem do Docker para se conectar ao TLS 1.0.

  ```docker
  MinProtocol = TLSv1
  CipherString = DEFAULT@SECLEVEL=1
  ```

  > [!NOTE]
  > Ao se conectar ao Microsoft.Data.SqlClient v2.0+ por meio de um ambiente Windows/Linux com TLS 1.0 ou TLS 1.1, uma mensagem de aviso de segurança será gerada se o SQL Server de destino e o cliente não puderem negociar, no mínimo, o TLS versão 1.2 ao estabelecer a conexão: `Security Warning: The negotiated <TLS1.0 | TLS1.1> is an insecure protocol and is supported for backward compatibility only. The recommended protocol version is TLS 1.2 and later.`

- Criptografia imposta do SQL Server

  Se o servidor de destino for uma instância SQL do Azure ou um SQL Server local com a propriedade "Forçar Criptografia" ativada, uma conexão criptografada será feita, para a qual o cliente deve estabelecer confiança com o servidor.

  **Solução recomendada:** há duas opções disponíveis para corrigir esse problema:

    1. Instalar o certificado TLS/SSL do SQL Server de destino no ambiente do cliente. Ele será validado se a criptografia for necessária.
    2. Definir a propriedade "Confiar no Certificado do Servidor = verdadeiro" na cadeia de conexão.

  **Solução não segura:** desabilite a configuração "Forçar Criptografia" no SQL Server.

- Certificados TLS/SSL não assinados com SHA-256 ou superior.

  **Solução recomendada:** gere um novo certificado TLS/SSL para o servidor cujo hash seja assinado com pelo menos o algoritmo de hash SHA-256.

### <a name="connection-pool-exhaustion-errors"></a>Erros de esgotamento do pool de conexões

Rastreamento de pilha observado:

```log
System.InvalidOperationException: Timeout expired. The timeout period elapsed prior to obtaining a connection from the pool.
This may have occurred because all pooled connections were in use and max pool size was reached.
```

#### <a name="possible-reasons-and-solutions"></a>Possíveis motivos e soluções

O aplicativo cliente está abrindo mais conexões do que o pool de conexão pode manter em atividade em determinado momento.

**Solução recomendada:** configure a propriedade de conexão "Tamanho Máximo do Pool" para um valor mais alto e feche as conexões não utilizadas em tempo hábil.

## <a name="contact-support"></a>Contatar o suporte

Se este guia não resolver seus problemas de conectividade, você poderá exibir os problemas existentes no repositório [dotnet/sqlclient](https://github.com/dotnet/SqlClient) e abrir um novo problema, se necessário.
