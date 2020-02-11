---
title: O SQLXML não é instalado no SQL Server
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c666d02449190ca6a88ac43c96ab7aee9676be4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75242652"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>O SQLXML não é instalado no SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Antes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o SQLXML 4.0 era lançado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazia parte da instalação padrão de todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com exceção da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a última versão do SQLXML (SQLXML 4.0 SP1) não está mais incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar o SQLXML 4,0 SP1, baixe-o no [local de instalação do sqlxml 4,0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Se um aplicativo for executado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no e exigir o SQLXML 4,0, você precisará baixar e instalar o SQLXML 4,0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento do SQLXML 4.0 SP1 com novos tipos de dados que usam o SQLOLEDB e o SQL Server Native Client OLE DB Provider  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o introduziu os seguintes tipos de dados, que os desenvolvedores que usam o SQLXML talvez queiram usar:  
  
-   **Data**  
  
-   **Hora**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Ao usar o SQLXML 4,0 SP1 com SQLOLEDB ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente nativo OLE DB de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], esses tipos aparecem como cadeias de caracteres para um desenvolvedor. O SQLXML 4,0 SP1 habilitará esses quatro novos tipos de dados como tipos escalares internos quando usados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o provedor de OLE DB de cliente nativo 11,0 ou posterior. Até que o SQLXML 4.0 SP1 seja baixado, o mapeamento desses tipos com tipos que não são de cadeias de caracteres pode provocar truncamento de alguns dados. Por exemplo, o mapeamento de **datetime2** para **xsd: Date** fará com que os dados sejam truncados para a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] precisão de **DateTime** de 3,33 milissegundos.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação do SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
