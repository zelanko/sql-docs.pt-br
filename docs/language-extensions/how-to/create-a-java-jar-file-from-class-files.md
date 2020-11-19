---
title: Criar um arquivo jar Java com base em arquivos de classe
description: Empacote seus arquivos de classe em um arquivo JAR ao usar as Extensões de Linguagem do SQL Server para executar o código Java.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: how-to
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 076b20d277ef8608fd8c9fc30b4bce303d4ef06b
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870152"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Criar um arquivo jar Java com base em arquivos de classe
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Saiba como empacotar seus arquivos de classe em um arquivo jar enquanto usa as [Extensões de Linguagem do SQL Server](../language-extensions-overview.md) para executar código Java. Recomendamos que você empacote seus arquivos.

## <a name="create-a-jar-file"></a>Criar um arquivo de jar

Para criar um jar com base em arquivos de classe, navegue até a pasta que contém o arquivo de classe e execute este comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Verifique se o caminho até `jar.exe` faz parte da variável de caminho do sistema. Como alternativa, especifique o caminho completo para o jar que pode ser encontrado em `/bin` na pasta JDK. Por exemplo:

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar o runtime Java nas Extensões de Linguagem do SQL Server](../how-to/call-java-from-sql.md)