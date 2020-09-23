---
title: Alterar a versão padrão do runtime da linguagem R ou Python
description: Saiba como alterar a versão padrão do runtime do R ou Python usada por uma instância SQL com SQL Server 2017 Machine Learning Services ou SQL Server R Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/14/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: d730ead0a11c240284ecb9a902a90eaedc5b1bb6
ms.sourcegitcommit: 5f658b286f56001b055a8898d97e74906516dc99
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009353"
---
# <a name="change-the-default-r-or-python-language-runtime-version"></a>Alterar a versão padrão do runtime da linguagem R ou Python

[!INCLUDE[SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

Este artigo descreve como alterar a versão padrão do R ou do Python usada em [SQL Server 2016 R Services](../r/sql-server-r-services.md) ou [SQL Server 2017 Machine Learning Services](../sql-server-machine-learning-services.md).

A seguir, são listadas as versões do runtime do R e do Python que estão incluídas nas diferentes versões do SQL Server.

| Versão do SQL Server | Serviço | Atualização Cumulativa | Versões de runtime do R | Versão de runtime do Python |
|-|-|-|-|-|
| SQL Server 2016 | R Services | RTM – SP2 CU13 | 3.2.2 | Não disponível |
| SQL Server 2016 | R Services | SP2 CU14 e posteriores | 3.2.2 e 3.5.2 | Não disponível |
| Microsoft SQL Server 2017 | Serviços de Machine Learning | RTM – CU21 | 3.3.3 | 3.5.2 |
| Microsoft SQL Server 2017 | Serviços de Machine Learning | CU22 e posteriores | 3.3.3 e 3.5.2 | 3.5.2 e 3.7.2 |

## <a name="prerequisites"></a>Pré-requisitos

Você precisa instalar uma CU (atualização cumulativa) para alterar a versão padrão do runtime da linguagem R ou Python:

- **SQL Server 2016:** CU (atualização cumulativa) 14 do SP (Service Pack) 2 ou posterior
- **SQL Server 2017:** CU (atualização cumulativa) 22 ou posterior

Para baixar a atualização cumulativa mais recente, confira [Atualizações mais recentes para o Microsoft SQL Server](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md).

> [!NOTE]
> Se você corrigir a atualização cumulativa com uma nova instalação do SQL Server, somente as versões mais recentes do runtime do R e do Python serão instaladas.

## <a name="change-r-runtime-version"></a>Alterar versão do runtime do R

Se você tiver instalado uma das atualizações cumulativas acima para SQL Server 2016 ou 2017, poderá ter várias versões do R em uma instância SQL. Cada versão está contida em uma subpasta da pasta de instância com o nome `R_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* (a pasta da instalação original pode não ter um número de versão anexado ao nome da pasta).

Se você instalar uma CU contendo R 3.5, a nova pasta `R_SERVICES` será:

- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.<INSTANCE_NAME>\R_SERVICES.3.5`
- SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\R_SERVICES.3.5`

Cada instância SQL usa uma dessas versões como a versão padrão do R. Você pode alterar a versão padrão usando o utilitário de linha de comando **RegisterRext.exe**. O utilitário está localizado na pasta do R em cada instância SQL:

*&lt;Caminho da instância SQL&gt;* \R_SERVICES.n.n\library\RevoScaleR\rxLibs\x64\RegisterRext.exe

> [!Note]
> A funcionalidade descrita neste artigo está disponível apenas com a cópia de **RegisterRext.exe** incluída nas CUs do SQL. Não use a cópia que veio com a instalação original do SQL.

Para alterar a versão de runtime do R, passe os seguintes argumentos de linha de comando para **RegisterRext.exe**:

- `/configure` – obrigatório, especifica que você está configurando a versão padrão do R.

- `/instance:`*&lt;nome da instância&gt;* – opcional, a instância que você deseja configurar. Se não for especificado, a instância padrão será configurada.

- `/rhome:`*&lt;caminho para a pasta R[n.n]&gt;* – opcional, caminho para a pasta de versão de runtime que você deseja definir como a versão padrão do R.

  Se você não especificar /rhome, o caminho configurado será o caminho no qual **RegisterRext.exe** está localizado.

### <a name="examples"></a>Exemplos

Veja a seguir exemplos de como alterar a versão do runtime do R no SQL Server 2016 e 2017.

#### <a name="change-r-runtime-version-in-sql-server-2016"></a>Alterar a versão do runtime do R no SQL Server 2016

Por exemplo, para configurar **R 3.5** como a versão padrão do R para a instância MSSQLSERVER01 no SQL Server 2016:

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

#### <a name="change-r-runtime-version-in-sql-server-2017"></a>Alterar a versão do runtime do R no SQL Server 2017

Por exemplo, para configurar **R 3.5** como a versão padrão do R para a instância MSSQLSERVER01 no SQL Server 2017:

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

Nesses exemplos, você não precisa incluir o argumento `/rhome`, já que está especificando a mesma pasta em que **RegisterRext.exe** está localizado.

## <a name="change-python-runtime-version"></a>Alterar a versão do runtime do Python

Se você instalou a CU22 ou posterior para SQL Server 2017, poderá ter várias versões do Python em uma instância SQL. Cada versão está contida em uma subpasta da pasta de instância com o nome `PYTHON_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* (a pasta da instalação original pode não ter um número de versão anexado ao nome da pasta).

Por exemplo, se você instalar uma CU contendo Python 3.7, uma pasta `PYTHON_SERVICES` será criada:

`C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\PYTHON_SERVICES.3.7`  

Cada instância SQL usa uma dessas versões como a versão padrão do Python. Você pode alterar a versão padrão usando o utilitário de linha de comando **RegisterRExt.exe**. O utilitário está localizado nas pastas do Python em cada instância SQL:

*&lt;Caminho da instância SQL&gt;* `\PYTHON_SERVICES.n.n\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.exe`

> [!Note]
> A funcionalidade descrita neste artigo está disponível apenas com a cópia de **RegisterRExt.exe** incluída nas CUs do SQL. Não use a cópia que veio com a instalação original do SQL.

Para alterar a versão de runtime do Python, passe os seguintes argumentos de linha de comando para **RegisterRext.exe**:

- `/configure` – obrigatório, especifica que você está configurando a versão padrão do Python.

- `/python` – especifica que você está configurando a versão padrão do Python. Opcional se você especificar `/pythonhome`.

- `/instance:`*&lt;nome da instância&gt;* – opcional, a instância que você deseja configurar. Se não for especificado, a instância padrão será configurada.

- `/pythonhome:`*&lt;caminho para a pasta PYTHON_SERVICES[n.n]&gt;* – opcional, caminho para a pasta de versão de runtime que você deseja definir como a versão padrão do Python.

  Se você não especificar /pythonhome, o caminho configurado será o caminho no qual **RegisterRExt.exe** está localizado.

### <a name="example"></a>Exemplo

Por exemplo, para configurar **Python 3.7** como a versão padrão do Python para a instância MSSQLSERVER01 no SQL Server 2017:

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7\Lib\site-packages\revoscalepy\rxLibs"

.\RegisterRext.exe /configure /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

Nesse exemplo, você não precisa incluir o argumento `/pythonhome`, já que está especificando a mesma pasta em que **RegisterRext.exe** está localizado.

## <a name="remove-a-runtime-version"></a>Remover uma versão de runtime

Para remover uma versão do R ou do Python, use **RegisterRExt.exe** com o argumento da linha de comando `/cleanup`, usando os mesmos argumentos `/rhome`, `/pythonhome` e `/instance` descritos anteriormente.

Por exemplo, para remover a pasta **R 3.2** da instância MSSQLSERVER01:

```cmd
.\RegisterRext.exe /cleanup /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES" /instance:MSSQLSERVER01
```

Por exemplo, para remover a pasta **Python 3.7** da instância MSSQLSERVER01:

```cmd
.\RegisterRExt.exe /cleanup /python /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

**RegisterRext.exe** solicitará que você confirme a limpeza do runtime do R especificado:

> *Tem certeza de que deseja excluir permanentemente o runtime fornecido junto com todos os pacotes instalados nele? \[Sim(Y)/Não(N)/Padrão(Yes)\]:*

Para confirmar, responda `Y` ou pressione Enter. Como alternativa, você pode ignorar esse prompt passando `/y` ou `/Yes` junto com a opção `/cleanup`.

> [!NOTE]
> Você só poderá remover uma versão se ela não estiver configurada como padrão e não estiver sendo usada para executar **RegisterRext.exe**.

## <a name="next-steps"></a>Próximas etapas

- [Obter informações sobre o pacote do R](../package-management/r-package-information.md)
- [Obter informações sobre o pacote do Python](../package-management/python-package-information.md)
- [Instalar pacotes com ferramentas de R](../package-management/install-r-packages-standard-tools.md)
- [Instalar pacotes com ferramentas do Python](../package-management/install-python-packages-standard-tools.md)
