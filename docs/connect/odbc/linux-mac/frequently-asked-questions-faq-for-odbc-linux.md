---
title: Perguntas frequentes (FAQ) para Linux ODBC e macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17d25f6084e136736dbc4c8a8ff3cb019ce4692e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Perguntas frequentes (FAQ) para Linux ODBC e macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

A seguir há respostas para perguntas sobre o Driver ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em Linux e macOS.
  
## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Como os aplicativos ODBC existentes no Linux ou macOS funcionam com o driver?**  
Você deve ser capaz de compilar e executar os aplicativos ODBC que você compilar e executar em Linux ou macOS usando outros drivers. 
  
**Quais recursos do [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] essa versão do driver suporta?**

O driver ODBC no Linux e macOS dá suporte a todos os recursos de servidor no [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] exceto LocalDB. Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] recursos com suporte, consulte [diretrizes de programação](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**O driver dá suporte à autenticação Kerberos?**  
Sim. Se você tiver uma configuração de ambiente existente do Kerberos, você deve ser capaz de se conectar a servidores usando o `Trusted_Connection=Yes` DSN ou conexão opção de cadeia de caracteres. Para obter mais informações, consulte [usando a autenticação integrada](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**Qual codificação Unicode um aplicativo deve usar?**  
UTF-8 para dados SQL_CHAR e UTF-16 para dados SQL_WCHAR.  

**Há exemplos ODBC que eu possa baixar e executar com o driver para experimentar ou avaliar?**

Consulte [Use Existing MSDN C++ ODBC Samples for the ODBC Driver on Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) para obter um exemplo. Isso também é aplicável para o driver ODBC macOS. 

**O driver ODBC no Linux ou macOS Abrir fonte?**

Não, os drivers ODBC no Linux e macOS não são um produto de software livre.  

## <a name="see-also"></a>Consulte também
[Instalando o Microsoft ODBC Driver for SQL Server no Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
