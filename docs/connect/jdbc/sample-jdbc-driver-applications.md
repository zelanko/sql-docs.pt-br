---
title: Aplicativos de exemplo do JDBC Driver
description: Os aplicativos de exemplo do JDBC Driver for SQL Server demonstram vários recursos e boas práticas de programação que você pode seguir ao usar o JDBC Driver.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e55eb9d0e710ba41089dcb014e9e626343ea4e91
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634258"
---
# <a name="sample-jdbc-driver-applications"></a>Aplicativos de exemplo do JDBC Driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os aplicativos de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstram vários recursos do driver JDBC. Além disso, eles demonstram práticas de programação recomendadas que você pode seguir ao usar o driver JDBC com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Todos os aplicativos de exemplo estão contidos em arquivos de código * .java que podem ser compilados e executados em seu computador local e eles estão localizados em várias subpastas no seguinte local:  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

Os tópicos nesta seção descrevem como configurar e executar os aplicativos de exemplo e incluem uma discussão do que os aplicativos de exemplo demonstram.  
  
## <a name="in-this-section"></a>Nesta seção  
  
| Tópico                                                                                                        | Descrição                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Conectando e recuperando dados](connecting-and-retrieving-data.md)                       | Estes aplicativos de exemplo demonstram como conectar-se a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles também demonstram diferentes maneiras de recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. |
| [Trabalhando com tipos de dados &#40;JDBC&#41;](working-with-data-types-jdbc.md)                 | Estes aplicativos de exemplo demonstram como usar os métodos de tipo de dados do driver JDBC para trabalhar usando dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                           |
| [Trabalhando com conjuntos de resultados](../../connect/jdbc/working-with-result-sets.md)                                   | Estes aplicativos de exemplo demonstram como usar conjuntos de resultados para processar dados contidos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].                                                                                                         |
| [Manipular dados grandes](../../connect/jdbc/working-with-large-data.md)                                     | Estes aplicativos de exemplo demonstram como usar buffer adaptável para recuperar dados de valor grande de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem a sobrecarga de cursores de servidor.                                                      |
| [Descoberta e classificação de dados SQL](../../connect/jdbc/data-discovery-classification-sample.md) | Este aplicativo de exemplo demonstra como recuperar informações de Descoberta e Classificação de Dados contidas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um objeto ResultSet usando o JDBC Driver.                                      |
  
## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
