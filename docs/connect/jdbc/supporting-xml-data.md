---
title: Dando suporte a dados XML | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f561c72cda30a9f62e202cbd612725d02b7f408
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="supporting-xml-data"></a>Dando suporte a dados XML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Fornece um **xml** tipo de dados que permite armazenar documentos XML e fragmentos em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. O **xml** tipo de dados é um tipo de dados internos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]e é em algumas semelhanças com outros tipos internos, como **int** e **varchar**. Como outros tipos internos, você pode usar o **xml** como tipo de dados: um tipo de variável, um tipo de parâmetro, um tipo de retorno de função ou uma coluna de tipo quando você cria uma tabela; ou em [!INCLUDE[tsql](../../includes/tsql_md.md)] funções CAST e CONVERT. No driver JDBC, o **xml** tipo de dados pode ser mapeado como uma cadeia de caracteres, a matriz de bytes, o fluxo, o objeto CLOB, BLOB ou SQLXML. String é o mapeamento padrão.  
  
 O driver JDBC fornece suporte para a API do JDBC 4.0, que apresenta a interface SQLXML. A interface SQLXML define métodos para interagir com dados XML e manipulá-los. O **SQLXML** é um tipo de dados do JDBC 4.0 e ele mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de dados. Portanto, para usar o tipo de dados SQLXML nos aplicativos, você deve definir o classpath para incluir o arquivo sqljdbc4.jar. Se o aplicativo tentar usar o sqljdbc3.jar ao acessar o objeto SQLXML e seus métodos, uma exceção será lançada.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]sempre valida os dados XML antes de armazená-lo na coluna de banco de dados. Os aplicativos podem usar **SQLXML** tipo de dados, pois o driver JDBC mapeia para o **xml** automaticamente, o tipo de dados. O **SQLXML** suporte está disponível na sqljdbc4.jar. Consulte [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para a lista de versões do JRE com suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Os tópicos nesta seção descrevem a interface SQLXML e como programar em relação a **SQLXML** tipo de dados usando os métodos da API do JDBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Interface SQLXML](../../connect/jdbc/sqlxml-interface.md)|Descreve a interface SQLXML e seus métodos.|  
|[Programando com SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Descreve como usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] métodos da API para armazenar e recuperar dados XML em e de um banco de dados relacional com o **SQLXML** tipo de dados Java. Além disso, contém informações sobre os tipos de objetos SQLXML e fornece uma lista de diretrizes e limitações importantes ao usar objetos SQLXML.|  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
