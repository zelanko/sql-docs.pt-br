---
title: Dando suporte a dados XML | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 32b7217e-1f0c-473d-9a45-176daa81584e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f98ef1cbff732bc969b8eea45ad38ee2f158fa73
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622054"
---
# <a name="supporting-xml-data"></a>Dando suporte a dados XML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um tipo de dados **xml** que permite armazenar fragmentos e documentos XML em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O tipo de dados **xml** é interno no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tem algumas semelhanças com outros tipos internos, como **int** e **varchar**. Como outros tipos internos, é possível usar o tipo de dados **xml** como: um tipo de variável, um tipo de parâmetro, um tipo de retorno de função ou um tipo de coluna quando você cria uma tabela; ou em funções [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST e CONVERT. No driver JDBC, o tipo de dados **xml** pode ser mapeado como um objeto de Cadeia de Caracteres, matriz de bytes, fluxo, CLOB, BLOB ou SQLXML. String é o mapeamento padrão.  
  
 O driver JDBC fornece suporte para a API do JDBC 4.0, que apresenta a interface SQLXML. A interface SQLXML define métodos para interagir com dados XML e manipulá-los. O **SQLXML** é um tipo de dados do JDBC 4.0 e ele mapeia para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **xml** tipo de dados. Portanto, para usar o tipo de dados SQLXML nos aplicativos, você deve definir o classpath para incluir o arquivo sqljdbc4.jar. Se o aplicativo tentar usar o sqljdbc3.jar ao acessar o objeto SQLXML e seus métodos, uma exceção será lançada.  
  
> [!IMPORTANT]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre valida os dados XML antes de armazená-los na coluna do banco de dados. Os aplicativos podem usar o tipo de dados **SQLXML**, pois o driver JDBC mapeia esse tipo de dados automaticamente para o tipo de dados **xml**. O suporte ao **SQLXML** está disponível na sqljdbc4.jar. Ver [requisitos do sistema para o Driver JDBC](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md) para obter a lista de versões do JRE com suporte a [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)].  
  
 Os tópicos desta seção descrevem a interface SQLXML e como programar em relação ao tipo de dados **SQLXML** usando os métodos da API JDBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Interface SQLXML](../../connect/jdbc/sqlxml-interface.md)|Descreve a interface SQLXML e seus métodos.|  
|[Programando com SQLXML](../../connect/jdbc/programming-with-sqlxml.md)|Descreve como usar os métodos API do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para armazenar e recuperar dados XML em e de um banco de dados relacional com o tipo de dados **SQLXML** Java. Além disso, contém informações sobre os tipos de objetos SQLXML e fornece uma lista de diretrizes e limitações importantes ao usar objetos SQLXML.|  
  
## <a name="see-also"></a>Consulte Também  
 [Noções básicas sobre os tipos de dados do JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
