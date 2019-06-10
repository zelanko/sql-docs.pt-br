---
title: Matriz de suporte do Microsoft JDBC Driver para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c5769e67-99f7-4bc1-a4fa-8941dad33d35
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f9e68149a567b2ccc7b4477e16e5ff39eedf1f6b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781458"
---
# <a name="microsoft-jdbc-driver-for-sql-server-support-matrix"></a>Matriz de suporte do Microsoft JDBC Driver para SQL Server
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Esta página contém a matriz de suporte e a política de ciclo de vida de suporte para o Microsoft JDBC Driver para SQL Server.  
  
## <a name="microsoft-jdbc-driver-support-lifecycle-matrix-and-policy"></a>Matriz e política de suporte do Microsoft JDBC Driver  
 A política de ciclo de vida de suporte da Microsoft (MSL) fornece informações transparentes e previsíveis sobre o ciclo de vida de suporte dos produtos da Microsoft. As versões de driver JDBC 3.0, 4.x, 6.x e 7.x têm cinco anos de suporte base a partir da data de lançamento do driver. O suporte base é definido no site do ciclo de vida de suporte da Microsoft.  
  
 As opções de suporte personalizado e estendido não estão disponíveis para Microsoft JDBC Driver.  
    
 Os Microsoft JDBC Drivers a seguir têm suporte até a data de fim do suporte indicada.  
  
|Nome do driver|Versão do pacote de driver|JAR(s) aplicáveis|Fim do Suporte Base|
|-|-|-|-|  
|Microsoft JDBC Driver 7.2 para SQL Server|7.2|mssql-jdbc-7.2.2.jre11.jar<br> mssql-jdbc-7.2.2.jre8.jar|16 de abril de 16 de 2024|
|Microsoft JDBC Driver 7.0 para SQL Server|7.0|mssql-jdbc-7.0.0.jre10.jar<br> mssql-jdbc-7.0.0.jre8.jar|31 de julho de 2023|  
|Microsoft JDBC Driver 6.4 para SQL Server|6.4|mssql-jdbc-6.4.0.jre9.jar<br> mssql-jdbc-6.4.0.jre8.jar<br> mssql-jdbc-6.4.0.jre7.jar|27 de fevereiro de 2023|    
|Microsoft JDBC Driver 6.2 para SQL Server|6.2|mssql-jdbc-6.2.2.jre8.jar<br> mssql-jdbc-6.2.2.jre7.jar|30 de junho de 2022|    
|Microsoft JDBC Driver 6.0 para SQL Server|6.0|sqljdbc42.jar<br>sqljdbc41.jar|14 de julho de 2021|    
|Microsoft JDBC Driver 4.2 para SQL Server|4.2|sqljdbc42.jar<br>sqljdbc41.jar|24 de agosto de 2020|  
|Microsoft JDBC Driver 4.1 para SQL Server|4.1|sqljdbc41.jar|12 de dezembro de 2019|  
  
 Os Microsoft JDBC Drivers a seguir não têm mais suporte.  
 
|Nome do driver|Versão do pacote de driver|Fim do Suporte Base|  
|-|-|-|
|Microsoft JDBC Driver 4.0 para SQL Server|4.0|6 de março de 2017|  
|Microsoft SQL Server JDBC Driver 3.0|3.0|23 de abril de 2015|  
|Microsoft SQL Server JDBC Driver 2.0|2.0|31 de dezembro de 2012|  
|Driver de JDBC 1.2 do Microsoft SQL Server 2005|1.2|25 de junho de 2011|  
|Microsoft SQL Server 2005 JDBC Driver 1.1|1.1|25 de junho de 2011|  
|Microsoft SQL Server 2005 JDBC Driver 1.0|1.0|25 de junho de 2011|  
|Microsoft SQL Server 2000 JDBC Driver|2000|9 de julho de 2010|  
  
## <a name="sql-version-compatibility"></a>Compatibilidade com versões do SQL  
  
|Versão do driver|SQL Server 2008|SQL Server 2008R2|SQL Server 2012|Banco de dados SQL do Azure|PDW 2008R2 AU3<sup>4</sup>|SQL Server 2014|SQL Server 2016|SQL Server 2017|Instância Gerenciada do SQL do Azure (Versão Prévia Privada Estendida)|  
|-|-|-|-|-|-|-|-|-|-|
|7.2|N|S|S|S|S|S|S|S|S|  
|7.0|N|S|S|S|S|S|S|S|S|  
|6.4|N|S|S|S|S|S|S|S|S|  
|6.2|S|S|S|S|S|S|S|S|N|
|6.1|S|S|S|S|S|S|S|N|N|
|6.0|S|S|S|S|S|S|S|N|N|
|4.2|S|S|S|S|S|S|S|N|N|
|4.1|S|S|S|S|S|S|S|N|N|
|4.0|S|S|S|S|S|S|S|N|N|
|3.0|S|S|S<sup>1</sup>|S<sup>2</sup>|N|S<sup>5</sup>|N|N|N|
|2.0|S<sup>3</sup>|S<sup>3</sup>|N|N|N|N|N|N|N|
|1.2|S<sup>3</sup>|N|N|N|N|N|N|N|N|
|1.1|N|N|N|N|N|N|N|N|N|  
|1.0|N|N|N|N|N|N|N|N|N|  
|2000|N|N|N|N|N|N|N|N|N|  
  
 <sup>1</sup>O Microsoft SQL Server JDBC Driver versão 3.0 pode conectar-se ao SQL Server 2012 como um cliente de nível inferior.  
  
 <sup>2</sup>O suporte ao Banco de dados SQL do Azure foi introduzido no driver 3.0 como um hotfix. Recomendamos que os clientes Banco de dados SQL do Azure usem a versão disponível mais recente do driver.  
  
 <sup>3</sup>O Microsoft SQL Server JDBC Driver versão 2.0 e o Microsoft SQL Server 2005 JDBC Driver versão 1.2 podem conectar-se ao SQL Server 2008 como um cliente de nível inferior. Quando são permitidas conversões de nível inferior, os aplicativos podem executar consultas e atualizações nos novos tipos de dados do SQL Server 2008, como time, date, datetime2, datetimeoffset e FILESTREAM. Para obter mais informações sobre como usar esses novos tipos de dados com o driver JDBC, consulte  [Working with SQL Server 2008 Date/Time Data Types using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145198) e  [Working with SQL Server 2008 FileStream using JDBC Driver](https://go.microsoft.com/fwlink/?LinkId=145199). Para obter mais informações sobre a compatibilidade de nível inferior desses novos tipos de dados, consulte os tópicos  [Usando dados de data e hora](https://go.microsoft.com/fwlink/?LinkId=145211)e  [Suporte a FILESTREAM](https://go.microsoft.com/fwlink/?LinkId=145212) nos Manuais Online do Microsoft SQL Server.  
  
 <sup>4</sup>O suporte para conexões entre o Microsoft JDBC Driver e o Parallel Data Warehouse foi introduzido pela primeira vez no Microsoft JDBC Driver 4.0 para SQL Server e no Microsoft SQL Server 2008 R2 Parallel Data Warehouse Appliance Atualização 3.  
  
 <sup>5</sup>O Microsoft SQL Server JDBC Driver versão 3.0 pode conectar-se ao SQL Server 2014 como um cliente de nível inferior.  
  
## <a name="java-and-jdbc-specification-support"></a>Java e suporte à especificação JDBC  
  
|Versão do driver JDBC|Versões do JRE|Versão da API do JDBC| 
|-|-|-|  
|7.2|1.8, 11|4.2, 4.3 (parcialmente)|
|7.0|1.8, 10|4.2, 4.3 (parcialmente)|
|6.4|1.7, 1.8, 9|4.1, 4.2, 4.3 (parcialmente)|  
|6.2|1.7, 1.8|4.1, 4.2|  
|6.1|1.7, 1.8|4.1, 4.2|  
|6.0|1.7, 1.8|4.1, 4.2|  
|4.2|1.7, 1.8|4.1, 4.2|  
|4.1|1.7|4.0|  
|4.0|1.5, 1.6, 1.7|3.0, 4.0|  
|3.0|1.5, 1.6,|3.0, 4.0|  
|2.0|1.5, 1.6|3.0, 4.0|  
|1.2|1.4, 1.5, 1.6|3.0|  
|1.1|1.4|3.0|  
|1.0|1.4|3.0|  
|2000|1.4|3.0|  
  
## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte  
 O Microsoft JDBC driver foi criado para funcionar em qualquer sistema operacional com suporte ao uso de uma Máquina Virtual Java (JVM). Algumas plataformas normalmente usadas incluem Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2008 R2, Windows Vista, Linux, Unix, AIX e MacOS, entre outras.  
  
 A equipe de produto do JDBC testa o driver nos sistemas operacionais Windows, Sun Solaris, SUSE Linux e RedHat Linux.  O suporte ao cliente está disponível para clientes em todas as plataformas. No entanto, podemos solicitar que você reproduza o problema em uma plataforma como o Windows.  
  
## <a name="application-server-support"></a>Suporte a servidor de aplicativos  
 O Microsoft JDBC Driver para SQL Server é testado em diversos servidores de aplicativos.  Consulte o fornecedor do seu servidor de aplicativos para obter detalhes adicionais sobre qual versão do driver é compatível com seus produtos.  
  
  
