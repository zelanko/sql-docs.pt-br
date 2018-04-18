---
title: Instalando o SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
caps.latest.revision: 44
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 04bce15ac37963dd165b9c265a88778d99839cb4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="installing-sql-server-native-client"></a>Instalando o SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > Para conteúdo relacionado a versões anteriores do SQL Server, consulte [instalar o SQL Server Native Client](https://msdn.microsoft.com/en-US/library/ms131321(SQL.120).aspx).

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 é instalado quando você instala [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]. 
 
 Não há nenhum SQL Server 2016 Native Client. Para obter mais informações, consulte [SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md). 
 
Você também pode obter sqlncli.msi na página da Web do SQL Server 2012 Feature Pack. Para baixar a versão mais recente do o SQL Server Native Client, vá para [Microsoft® SQL Server® 2012 Feature Pack](http://www.microsoft.com/en-us/download/confirmation.aspx?id=29065). Se uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client anteriores ao SQL Server 2012 também é instalado no computador, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 será instalada lado a lado com a versão anterior.  
  
 Os arquivos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll e s11ch_sqlncli.chm) são instalados no seguinte local:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Todas as configurações do Registro apropriadas para o provedor OLE DB do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o driver ODBC do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client fazem parte do processo de instalação.  
  
 Os arquivos de biblioteca e cabeçalho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h e sqlncli11.lib) são instalados no seguinte local:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Além de instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalação, também é um programa de instalação redistribuível chamado sqlncli.msi, que pode ser encontrado na [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] disco de instalação no seguinte local: `%CD%\Setup\`.  
  
 Você pode distribuir o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client através do sqlncli.msi. Talvez seja necessário instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ao implantar um aplicativo. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, consulte [criação de um pacote de Bootstrapper personalizado para o Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667) e [Adding Custom Prerequisites](http://go.microsoft.com/fwlink/?LinkId=115668).  
  
 As versões para x64 e Itanium de sqlncli.msi também instalam a versão de 32 bits do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Se o aplicativo foi projetado para uma plataforma diferente daquela em que foi desenvolvido, você poderá baixar as versões do sqlncli.msi para x64, Itanium e x86 do Centro de Download da Microsoft.  
  
 Quando você invoca o sqlncli.msi, só os componentes cliente são instalados por padrão. Os componentes cliente são arquivos que oferecem suporte à execução de um aplicativo que foi desenvolvido usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para instalar também os componentes SDK, especifique `ADDLOCAL=All` na linha de comando. Por exemplo:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Instalação silenciosa  
 Se você usar a opção /passive, /qn, /qb, or /qr com msiexec, também deverá especificar IACCEPTSQLNCLILICENSETERMS=YES, para indicar explicitamente que aceitou os termos da licença do usuário final. Essa opção deve ser especificada totalmente em letras maiúsculas.  
  
## <a name="uninstalling-sql-server-native-client"></a>Desinstalando o SQL Server Native Client  
 Como aplicativos, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ferramentas dependem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, é importante não desinstalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client até que todos os aplicativos dependentes são desinstalados. Para usuários de provedor com um aviso de que seu aplicativo depende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, use a opção de instalação APPGUID no MSI da seguinte maneira:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 O valor passado para APPGUID é o seu código de produto específico. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [Tópicos de instruções de instalação](http://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
