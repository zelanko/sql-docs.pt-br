---
title: O SQLXML não é instalado no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a300c3e5c3f5bc800637ef4c31c886a23db8b544
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367258"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>O SQLXML não é instalado no SQL Server
  Antes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], o SQLXML 4.0 era lançado com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazia parte da instalação padrão de todas as versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com exceção da [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], a última versão do SQLXML (SQLXML 4.0 SP1) não está mais incluída no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar o SQLXML 4.0 SP1 quando ele estiver disponível, baixe-o do [local de instalação do SQLXML SP1](https://www.microsoft.com/download/details.aspx?id=3522).  
  
 Se um aplicativo executar no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exigir o SQLXML 4.0, e o computador não tiver o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], você deve baixar e instalar o SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento do SQLXML 4.0 SP1 com novos tipos de dados que usam o SQLOLEDB e o SQL Server Native Client OLE DB Provider  
 O [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduz os seguintes tipos de dados que os desenvolvedores que usam o SQLXML talvez queiram usar:  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 Ao usar o SQLXML 4.0 SP1 com o SQLOLEDB (do Windows Data Access Components, anteriormente Microsoft Data Access Components) ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], esses novos tipos aparecerão como cadeias de caracteres para um desenvolvedor. O SQLXML 4.0 SP1 habilitará esses quatro novos tipos de dados como tipos escalares internos quando usados com o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0. Até que o SQLXML 4.0 SP1 seja baixado, o mapeamento desses tipos com tipos que não são de cadeias de caracteres pode provocar truncamento de alguns dados. Por exemplo, o mapeamento `DateTime2` à `xsd:date` fará com que dados sejam truncados para o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` precisão de 3,33 milissegundos.  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos de programação do SQLXML 4.0](sqlxml-4-0-programming-concepts.md)  
  
  
