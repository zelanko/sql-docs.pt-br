---
title: Perguntas frequentes para Linux e macOS ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99b92271060cbe670b48058e988b104aa296474b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731524"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Perguntas frequentes para Linux e macOS ODBC
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Veja a seguir respostas para perguntas sobre o driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Linux e no macOS.
  
## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Como os aplicativos ODBC existentes no Linux ou no macOS funcionam com o driver?**  
Você deve ser capaz de compilar e executar os aplicativos ODBC que você vem compilando e executando no Linux ou no macOS usando outros drivers. 
  
**Com quais recursos do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] essa versão do driver é compatível?**

O driver ODBC no Linux e no macOS dá suporte a todos os recursos de servidor no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], exceto LocalDB. Para obter mais informações sobre os recursos com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [Diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**O driver é compatível com a autenticação Kerberos?**  
Sim. Se você tiver uma configuração de ambiente existente do Kerberos, você deve ser capaz de se conectar a servidores usando o `Trusted_Connection=Yes` DSN ou conexão a opção de cadeia de caracteres. Para obter mais informações, consulte [Como usar autenticação integrada](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Qual codificação Unicode um aplicativo deve usar?**  
UTF-8 para dados SQL_CHAR e UTF-16 para dados SQL_WCHAR.  

**Há exemplos de ODBC que eu possa baixar e executar com o driver para experimentar ou avaliar?**

Consulte [Use Existing MSDN C++ ODBC Samples for the ODBC Driver on Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) para obter um exemplo. Isso também é aplicável para o driver ODBC do macOS. 

**É o driver ODBC no Linux ou macOS software livre?**

Não, os drivers ODBC no Linux e macOS não são um produto de software livre.  

## <a name="see-also"></a>Consulte Também
[Instalando o Microsoft ODBC Driver for SQL Server em Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
