---
title: Criar um arquivo jar Java com base em arquivos de classe
description: Saiba como criar um arquivo jar Java com base em arquivos de classe
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53eb4b8da04a799461dcb1e0cb32feff2fe6f
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658863"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Criar um arquivo jar Java com base em arquivos de classe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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