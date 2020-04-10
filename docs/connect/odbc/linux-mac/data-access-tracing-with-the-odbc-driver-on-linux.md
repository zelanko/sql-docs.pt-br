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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6abf282656681d3f798215282adb784b29c3846
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921986"
---
# <a name="data-access-tracing-with-the-odbc-driver-on-linux-and-macos"></a>Rastreamento de acesso a dados com o driver ODBC no Linux e no macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O Gerenciador de driver unixODBC no macOS e Linux dá suporte ao rastreamento de entrada de chamada à API do ODBC e à saída do Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

Para rastrear o comportamento do ODBC do aplicativo, edite a seção `[ODBC]` do arquivo `odbcinst.ini` para definir os valores `Trace=Yes` e `TraceFile` para o caminho do arquivo que deve conter a saída do rastreamento; por exemplo:

```ini
[ODBC]
Trace=Yes
TraceFile=/home/myappuser/odbctrace.log
```

(Você também pode usar `/dev/stdout` ou qualquer outro nome de dispositivo como o destino de envio da saída do rastreamento, em vez de enviá-la para um arquivo persistente.) Com as configurações acima, sempre que um aplicativo carregar o Gerenciador do Driver unixODBC, ele registrará todas as chamadas à API do ODBC que ele realizou no arquivo de saída.

Depois de concluir o rastreamento do aplicativo, remova `Trace=Yes` do arquivo `odbcinst.ini` para evitar prejudicar o desempenho de rastreamento e verifique se os arquivos de rastreamento desnecessários foram removidos.

O rastreamento se aplica a todos os aplicativos que usam o driver no `odbcinst.ini`. Para não rastrear todos os aplicativos (por exemplo, para evitar a divulgação de informações confidenciais por usuário), você pode rastrear uma instância de aplicativo individual, fornecendo o local de um `odbcinst.ini` privado, usando a variável de ambiente `ODBCSYSINI`. Por exemplo:

```bash
$ ODBCSYSINI=/home/myappuser myapp
```

Nesse caso, você pode adicionar `Trace=Yes` à seção `[ODBC Driver 13 for SQL Server]` de `/home/myappuser/odbcinst.ini`.

## <a name="determining-which-odbcini-file-the-driver-is-using"></a>Determinando qual arquivo odbc.ini o driver está usando

Os drivers ODBC para Linux e macOS não sabem qual `odbc.ini` está em uso, nem o caminho para o arquivo `odbc.ini`. No entanto, informações sobre qual arquivo `odbc.ini` está em uso estão disponíveis nas ferramentas unixODBC `odbc_config` e `odbcinst` e na documentação do Gerenciador de Driver unixODBC.

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

A documentação do [unixODBC](http://www.unixodbc.org/doc/UserManual/) explica as diferenças entre os DSNs do usuário e do sistema. Em resumo:

- DSNs de usuário – são DSNs que só estão disponíveis para um usuário específico. Os usuários podem se conectar usando os próprios DSNs de usuário, bem como adicioná-los, modificá-los e removê-los. Os DSNs de usuário são armazenados em um arquivo no diretório base do usuário ou em um subdiretório dele.

- DSNs de sistema – esses DSNs estão disponíveis para cada usuário no sistema se conectar usando-os, mas só podem ser adicionados, modificados e removidos por um administrador do sistema. Se um usuário tiver um DSN de usuário com o mesmo nome que um DSN de sistema, o DSN de usuário será usado nas conexões por esse usuário.

## <a name="see-also"></a>Consulte Também

- [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md)
