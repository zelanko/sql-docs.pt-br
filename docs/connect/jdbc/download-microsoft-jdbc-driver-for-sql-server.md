---
title: Baixe o Microsoft JDBC Driver para SQL Server
description: Baixe o Microsoft JDBC Driver for SQL Server para desenvolver aplicativos Java que se conectam ao SQL Server e ao Banco de Dados SQL do Azure.
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d48c3f0384a805debe13472fae1841515207d160
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042439"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Baixe o Microsoft JDBC Driver para SQL Server

O Microsoft JDBC Driver para SQL Server é um driver JDBC Tipo 4 que fornece conectividade de banco de dados por meio das APIs (interfaces de programação de aplicativo) padrão JDBC disponíveis na plataforma Java. Downloads do driver estão disponíveis para todos os usuários sem custo adicional. Eles fornecem acesso ao SQL Server por meio de qualquer aplicativo Java, servidor de aplicativos ou miniaplicativo habilitado para Java.

## <a name="download"></a>Baixar

A versão 8.4 é a versão mais recente em GA (disponibilidade geral). Ela dá suporte ao Java 8, 11 e 14. Se precisar executar em um runtime Java mais antigo, confira a [Matriz de suporte à especificação JDBC e Java](microsoft-jdbc-driver-for-sql-server-support-matrix.md#java-and-jdbc-specification-support) para ver se há alguma versão de driver com suporte que você pode usar. Estamos aperfeiçoando continuamente o suporte à conectividade com Java. Portanto, é altamente recomendável que você trabalhe com a versão mais recente do Microsoft JDBC driver.

**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.4 para SQL Server (zip)](https://go.microsoft.com/fwlink/?linkid=2137600)**  
**[![Baixar](../../ssms/media/download-icon.png) Baixar o Microsoft JDBC Driver 8.4 para SQL Server (tar.gz)](https://go.microsoft.com/fwlink/?linkid=2137502)**  

### <a name="version-information"></a>Informações da versão

- Número da versão: 8.4.1
- Lançado: 27 de agosto de 2020

Quando você baixa o driver, há vários arquivos JAR. O nome do arquivo JAR indica a versão do Java que é compatível com ele.

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse a [versão do site em inglês dos EUA](https://aka.ms/downloadmssqljdbcenglish). Você pode baixar idiomas diferentes do site da versão em inglês dos EUA selecionando [idiomas disponíveis](#available-languages).

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do Microsoft JDBC Driver para SQL Server está disponível nos seguintes idiomas:

Microsoft JDBC Driver 8.4.1 para SQL Server (zip): [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40a)

Microsoft JDBC Driver 8.4.1 para SQL Server (tar.gz): [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40a)

### <a name="release-notes"></a>Notas de versão

Para conhecer os detalhes desta versão, confira [as notas sobre a versão](release-notes-for-the-jdbc-driver.md) e os [requisitos do sistema](system-requirements-for-the-jdbc-driver.md).

### <a name="previous-releases"></a>Versões anteriores

Para baixar versões anteriores, confira [versões anteriores do Microsoft JDBC Driver para SQL Server](release-notes-for-the-jdbc-driver.md#previous-releases).

## <a name="using-the-jdbc-driver-with-maven-central"></a>Como usar o JDBC Driver com o Maven Central

É possível incluir o JDBC Driver em um projeto Maven ao adicioná-lo como uma dependência no arquivo POM.XML com o código a seguir:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>Drivers sem suporte

As versões de driver sem suporte não estão disponíveis para download aqui. Estamos aperfeiçoando continuamente o suporte à conectividade com Java. Portanto, é altamente recomendável que você trabalhe com a versão mais recente do Microsoft JDBC driver.  
  
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o Microsoft JDBC Driver para SQL Server, confira [Visão geral do JDBC Driver](overview-of-the-jdbc-driver.md) e [repositório GitHub do JDBC Driver](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md).
