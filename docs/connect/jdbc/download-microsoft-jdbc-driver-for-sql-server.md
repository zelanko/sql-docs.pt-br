---
title: Baixe o Microsoft JDBC Driver para SQL Server
description: Baixe o Microsoft JDBC Driver para SQL Server para desenvolver aplicativos Java que se conectam ao SQL Server.
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc273bccf054408f48e7bb2bd0409a31bb18bd18
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682001"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Baixe o Microsoft JDBC Driver para SQL Server

Este artigo fornece links de download para o Microsoft JDBC Driver para SQL Server. Este driver permite que você desenvolva aplicativos Java que se conectam ao SQL Server.  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>Downloads disponíveis do JDBC Driver para SQL Server

Use os links na tabela a seguir para baixar o Microsoft JDBC Driver mais recente para SQL Server que corresponda ao seu Java Runtime Environment (JRE):

| Versão | Data de liberação | Versões do Java |
|---|---|---|
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 01/08/2019 | JRE 8, 11, 12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 17/04/2019 | JRE 8, 11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 31/07/2018 | JRE 8, 10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 26/03/2018 | JRE 7, 8, 9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 12/02/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 27/02/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 4,2](https://go.microsoft.com/fwlink/?linkid=841534) | 26/02/2018 | JRE 7, 8 |
| [Microsoft JDBC Driver 4,1](https://go.microsoft.com/fwlink/?linkid=841533) | 27/02/2018 | JRE 7 |

Quando você baixa o driver, há vários arquivos JAR. O nome do arquivo JAR indica a versão do Java que ele suporta. Para obter mais informações sobre cada versão, consulte as [notas de versão](release-notes-for-the-jdbc-driver.md) e [os requisitos do sistema](system-requirements-for-the-jdbc-driver.md).

## <a name="using-the-jdbc-driver-with-maven-central"></a>Como usar o JDBC Driver com o Maven Central

É possível incluir o JDBC Driver em um projeto Maven ao adicioná-lo como uma dependência no arquivo POM.XML com o código a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>Drivers sem suporte

As versões de driver sem suporte não estão disponíveis para download aqui. Estamos aperfeiçoando continuamente o suporte à conectividade com Java. Portanto, é altamente recomendável que você trabalhe com a versão mais recente do Microsoft JDBC driver.  
  
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Microsoft JDBC Driver para SQL Server, consulte [visão geral do driver JDBC](overview-of-the-jdbc-driver.md) e o [repositório GitHub do driver JDBC](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md).
