---
title: Instalar o Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Instalando e desinstalando o driver OLE DB para SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
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
ms.author: pelopes
ms.openlocfilehash: 08f33d84ee8c035e1e1d3818e2a036f96af2a280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989315"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Instalar o OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Para instalar o driver de OLE DB para SQL Server você precisa do instalador msoledbsql. msi.
Execute o instalador e faça suas seleções preferenciais. O driver OLE DB para SQL Server pode ser instalado lado a lado com versões anteriores de provedores de OLE DB da Microsoft.

O driver OLE DB para SQL Server arquivos (msoledbsql. dll, msoledbsqlr. rll) são instalados no `%SYSTEMROOT%\system32\` . Além disso, o x64 msoledbsql. msi instala binários de 32 `%SYSTEMROOT%\SysWOW64\`bits no.

> [!NOTE]  
> Todas as configurações de registro apropriadas para o driver de OLE DB para SQL Server são feitas como parte do processo de instalação.  

O driver de OLE DB para SQL Server cabeçalho e arquivos de biblioteca (msoledbsql. h e msoledbsql. lib) são `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`instalados no. Além disso, o msoledbsql. msi x64 instala os mesmos arquivos `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`no.  

Você pode distribuir OLE DB driver para SQL Server por meio de msoledbsql. msi. Talvez seja necessário instalar OLE DB driver para SQL Server quando você implantar um aplicativo. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, confira [Criando um pacote de bootstrapper personalizado para o Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) e [Adicionando pré-requisitos personalizados](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
O x64 msoledbsql. msi também instala a versão de 32 bits do driver OLE DB para SQL Server. Se o seu aplicativo se destina a uma plataforma diferente daquela em que foi desenvolvido, você pode baixar versões do msoledbsql. msi para x64 e x86.

Quando você invoca msoledbsql.msi, só os componentes cliente são instalados por padrão. Os componentes cliente são arquivos que dão suporte à execução de um aplicativo que foi desenvolvido usando o OLE DB Driver for SQL Server. Para instalar também os componentes SDK, especifique `ADDLOCAL=All` na linha de comando. Por exemplo:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Instalação silenciosa  
 Se você usar a opção /passive, /qn, /qb ou /qr com msiexec, também precisará especificar IACCEPTMSOLEDBSQLLICENSETERMS=YES, para indicar explicitamente que aceitou os termos da licença do usuário final. Essa opção deve ser especificada totalmente em letras maiúsculas.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>Instalando o driver OLE DB para SQL Server como uma dependência  
É importante não desinstalar OLE DB driver para SQL Server até que todos os aplicativos dependentes sejam desinstalados. Para fornecer aos usuários um aviso de que seu aplicativo depende do driver OLE DB para SQL Server, use a opção de instalação APPGUID em seu MSI, da seguinte maneira:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

O valor passado para APPGUID é o seu código de produto específico. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.
A opção APPGUID requer a execução do instalador em um prompt de comandos com privilégios elevados.

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
