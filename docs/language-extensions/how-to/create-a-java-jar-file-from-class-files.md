---
title: Criar um arquivo jar Java com base em arquivos de classe
titleSuffix: SQL Server Language Extensions
description: Saiba como criar um arquivo jar Java com base em arquivos de classe
author: dphansen
ms.author: davidph
ms.date: 07/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cec311a28f9d5119b5a0aeb696597e8b34ba25a
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "73588770"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Criar um arquivo jar Java com base em arquivos de classe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Ao usar [extensões de linguagem do SQL Server](../language-extensions-overview.md) e executar um código Java, é recomendável empacotar seus arquivos de classe em um arquivo jar.

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

+ [Como chamar Java no SQL Server](../how-to/call-java-from-sql.md)