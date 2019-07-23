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
ms.openlocfilehash: 1fa39cd11f70a661de5c284e56f2ccc0f7a5777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008825"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Rastreamento de acesso a dados com o driver ODBC no Linux e no macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O Gerenciador de driver unixODBC no macOS e Linux dá suporte ao rastreamento de entrada de chamada à API ODBC e à [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]saída do driver ODBC para o.

Para rastrear o comportamento do ODBC do `odbcinst.ini` aplicativo, edite a `[ODBC]` seção do arquivo para definir `Trace=Yes` os `TraceFile` valores e para o caminho do arquivo que deve conter a saída do rastreamento; por exemplo:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(Você também pode usar `/dev/stdout` ou qualquer outro nome de dispositivo para enviar a saída de rastreamento em vez de para um arquivo persistente.) Com as configurações acima, sempre que um aplicativo carrega o Gerenciador de driver unixODBC, ele registrará todas as chamadas de API ODBC que ele realizou no arquivo de saída.

Depois de concluir o rastreamento do aplicativo, `Trace=Yes` remova- `odbcinst.ini` o do arquivo para evitar a penalidade de desempenho do rastreamento e certifique-se de que todos os arquivos de rastreamento desnecessários sejam removidos.

O rastreamento se aplica a todos os aplicativos que usam o driver no `odbcinst.ini`. Para não rastrear todos os aplicativos (por exemplo, para evitar a divulgação de informações confidenciais por usuário), você pode rastrear uma instância de aplicativo individual, fornecendo o local de um `odbcinst.ini` privado, usando a variável de ambiente `ODBCSYSINI`. Por exemplo:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

Nesse caso, você pode adicionar `Trace=Yes` `[ODBC Driver 13 for SQL Server]` à seção de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinando qual arquivo odbc.ini o driver está usando

Os drivers de ODBC para Linux e MacOS não sabem `odbc.ini` qual está em uso ou o caminho para o `odbc.ini` arquivo. No entanto, as `odbc.ini` informações sobre qual arquivo está em uso estão disponíveis nas `odbc_config` ferramentas `odbcinst`do unixODBC e e na documentação do Gerenciador de driver do unixODBC.

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

A [documentação do unixODBC](http://www.unixodbc.org/doc/UserManual/) explica as diferenças entre os DSNs do usuário e do sistema. Em Resumo:

- Os DSNs de usuário---são DSNs que só estão disponíveis para um usuário específico. Os usuários podem se conectar usando, adicionar, modificar e remover seus próprios DSNs de usuário. Os DSNs de usuário são armazenados em um arquivo no diretório base do usuário ou em um subdiretório dele.

- Os DSNs de sistema---esses DSNs estão disponíveis para cada usuário no sistema se conectar usando-os, mas só podem ser adicionados, modificados e removidos por um administrador do sistema. Se um usuário tiver um DSN de usuário com o mesmo nome que um DSN de sistema, o DSN de usuário será usado nas conexões por esse usuário.

## <a name="see-also"></a>Consulte Também

- [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
