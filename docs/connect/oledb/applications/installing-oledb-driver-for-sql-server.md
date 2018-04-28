---
title: Instalar o Driver do OLE DB para SQL Server | Microsoft Docs
description: Instalar e desinstalar o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Active
ms.openlocfilehash: 154ac8409b27ee5f5fe02f7ed8e1e2aff7f61ff1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Instalar o Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Para instalar o Driver OLE DB para SQL Server, você precisa msoledbsql.msi installer.
Execute o instalador e faça as seleções preferenciais. O Driver OLE DB para SQL Server pode ser instalada lado a lado com versões anteriores do provedor Microsoft OLE DB.

O Driver OLE DB para arquivos do SQL Server (msoledbsql.dll, msoledbsqlr.rll) são instalados em `%SYSTEMROOT%\system32\` . Além disso, o x64 msoledbsql.msi instala os binários de 32 bits em `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]  
> Todas as configurações de registro apropriados para o Driver OLE DB para SQL Server são feitas como parte do processo de instalação.  

O Driver OLE DB para SQL Server cabeçalho e biblioteca de arquivos (msoledbsql.h e msoledbsql.lib) são instalados em `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`. Além disso, o x64 msoledbsql.msi instala os mesmos arquivos no `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`.  

Você pode distribuir o Driver do OLE DB para SQL Server por meio de msoledbsql.msi. Você talvez precise instalar o Driver do OLE DB para SQL Server quando você implanta um aplicativo. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, consulte [criação de um pacote de Bootstrapper personalizado para o Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667) e [Adding Custom Prerequisites](http://go.microsoft.com/fwlink/?LinkId=115668).  
  
X64 msoledbsql.msi também instala a versão de 32 bits do Driver do OLE DB para SQL Server. Se seu aplicativo tem como alvo uma plataforma diferente daquele que foi desenvolvido, você pode baixar versões do msoledbsql.msi para x64 e x86.

Quando você chama msoledbsql.msi, somente os componentes de cliente são instalados por padrão. O cliente são componentes são arquivos que oferecem suporte à execução de um aplicativo que foi desenvolvido usando o Driver do OLE DB para SQL Server. Para instalar também os componentes SDK, especifique `ADDLOCAL=All` na linha de comando. Por exemplo:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Instalação silenciosa  
 Se você usar a opção /passive, /qn, /qb ou opção /qr com msiexec, você também deve especificar IACCEPTMSOLEDBSQLLICENSETERMS = Sim, para indicar explicitamente que você aceitar os termos de licença do usuário final. Essa opção deve ser especificada totalmente em letras maiúsculas.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>Instalar o Driver do OLE DB para SQL Server como uma dependência  
É importante não desinstalar o Driver do OLE DB para SQL Server até que todos os aplicativos dependentes são desinstalados. Para fornecer aos usuários um aviso de que seu aplicativo depende de Driver do OLE DB para SQL Server, use a opção de instalação APPGUID no MSI da seguinte maneira:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

O valor passado para APPGUID é o seu código de produto específico. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.
A opção de APPGUID requer que executa o instalador em um Prompt de comando com privilégios elevados.

## <a name="see-also"></a>Consulte também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
