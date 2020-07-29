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
ms.openlocfilehash: a105dde9046167257a86705f678466872785b4be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85735087"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Criar um arquivo jar Java com base em arquivos de classe
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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