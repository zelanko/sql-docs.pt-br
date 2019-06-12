---
title: Rastreamento de acesso a dados com o driver ODBC no Linux e no macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data access tracing
- tracing
ms.assetid: 3149173a-588e-47a0-9f50-edb8e9adf5e8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 23d867bba50a42dc55f4095abbfd92129df634be
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66785872"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Rastreamento de acesso a dados com o driver ODBC no Linux e no macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O Gerenciador de Driver unixODBC no macOS e Linux dá suporte a rastreamento de entrada de chamadas de API do ODBC e sair do Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Para rastrear o comportamento do aplicativo ODBC, edite o `odbcinst.ini` do arquivo `[ODBC]` seção para definir os valores `Trace=Yes` e `TraceFile` para o caminho do arquivo que contém o rastreamento de saída; por exemplo:

```ini
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(Você também pode usar `/dev/stdout` ou qualquer outro nome de dispositivo para enviar a saída de lá, em vez de em um arquivo persistente de rastreamento.) Com as configurações acima, sempre que um aplicativo carrega o Gerenciador de Driver unixODBC ele registrará todas as chamadas de API ODBC que ela executada no arquivo de saída.

Depois de concluir o rastreamento do aplicativo, remova `Trace=Yes` do `odbcinst.ini` para evitar a penalidade de desempenho de rastreamento de arquivo e verifique se todos os arquivos desnecessários de rastreamento são removidos.

O rastreamento se aplica a todos os aplicativos que usam o driver no `odbcinst.ini`. Para não rastrear todos os aplicativos (por exemplo, para evitar a divulgação de informações confidenciais por usuário), você pode rastrear uma instância de aplicativo individual, fornecendo o local de um `odbcinst.ini` privado, usando a variável de ambiente `ODBCSYSINI`. Por exemplo:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

Nesse caso, você pode adicionar `Trace=Yes` para o `[ODBC Driver 13 for SQL Server]` seção `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinando qual arquivo odbc.ini o driver está usando

Os drivers ODBC do Linux e macOS não souber quais `odbc.ini` está em uso ou o caminho para o `odbc.ini` arquivo. No entanto, informações sobre quais `odbc.ini` arquivo está em uso está disponível das ferramentas unixODBC `odbc_config` e `odbcinst`e para a documentação do Gerenciador de Driver unixODBC.

Por exemplo, o comando a seguir imprime (entre outras informações) o local dos arquivos `odbc.ini` do sistema e do usuário que contêm, respectivamente, os DSNs do sistema e do usuário:

```
$ odbcinst -j
unixODBC 2.3.1
DRIVERS............: /etc/odbcinst.ini
SYSTEM DATA SOURCES: /etc/odbc.ini
FILE DATA SOURCES..: /etc/ODBCDataSources
USER DATA SOURCES..: /home/odbcuser/.odbc.ini`
SQLULEN Size.......: 8
SQLLEN Size........: 8
SQLSETPOSIROW Size.: 8
```

O [documentação do unixODBC](http://www.unixodbc.org/doc/UserManual/) explica as diferenças entre o usuário e DSNs do sistema. Em Resumo:

- DSNs do usuário---esses são os DSNs que só estão disponíveis para um usuário específico. Os usuários podem conectar-se usando, adicionar, modificar e remover seus próprios DSNs do usuário. DSNs do usuário são armazenados em um arquivo no diretório base do usuário, ou em um subdiretório dele.

- DSNs de sistema---esses DSNs estão disponíveis para todos os usuários no sistema conectar-se de usá-los, mas podem apenas ser adicionados, modificados e removidos por um administrador de sistema. Se um usuário tiver um DSN de usuário com o mesmo nome como um DSN de sistema, o DSN de usuário será usado em conexões que o usuário.

## <a name="see-also"></a>Consulte Também

- [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
