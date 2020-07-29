---
title: Instalar o Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Instalar e desinstalar o Driver do OLE DB para SQL Server. Para instalar o Driver do OLE DB para SQL Server, você precisa do instalador msoledbsql.msi
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
ms.openlocfilehash: 1edd1c6e7a118e152fc1f8e85203434347061da5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007060"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Instalar o OLE DB Driver for SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Para instalar o Driver do OLE DB para SQL Server, você precisa do instalador msoledbsql.msi.
Execute o instalador e faça suas seleções preferenciais. O Driver do OLE DB para SQL Server pode ser instalado lado a lado com versões anteriores de provedores do Microsoft OLE DB.

Os arquivos do Driver do OLE DB para SQL Server (msoledbsql.dll, msoledbsqlr.rll) são instalados em `%SYSTEMROOT%\system32\`. Além disso, o msoledbsql.msi x64 instala binários de 32 bits em `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]  
> Todas as configurações adequadas do Registro são feitas para o Driver do OLE DB para SQL Server como parte do processo de instalação.  

Os arquivos de biblioteca e de cabeçalho do Driver do OLE DB para SQL Server (msoledbsql.h and msoledbsql.lib) são instalados em `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`. Além disso, o msoledbsql.msi x64 instala os mesmos arquivos em `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`.  

Você pode distribuir o Driver do OLE DB para SQL Server por meio de msoledbsql.msi. Talvez seja necessário instalar o Driver do OLE DB para SQL Server ao implantar um aplicativo. Uma maneira de instalar vários pacotes em um processo que, para o usuário, parece ser uma única instalação é usar a tecnologia de encadeador e bootstrapper. Para obter mais informações, confira [Criando um pacote de bootstrapper personalizado para o Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) e [Adicionando pré-requisitos personalizados](https://go.microsoft.com/fwlink/?LinkId=115668).  
  
O msoledbsql.msi x64 também instala a versão de 32 bits do Driver do OLE DB para SQL Server. Se o aplicativo for projetado para uma plataforma diferente daquela em que foi desenvolvido, você poderá baixar as versões do msoledbsql.msi para x64 e x86.

Quando você invoca msoledbsql.msi, só os componentes cliente são instalados por padrão. Os componentes cliente são arquivos que dão suporte à execução de um aplicativo que foi desenvolvido usando o OLE DB Driver for SQL Server. Para instalar também os componentes SDK, especifique `ADDLOCAL=All` na linha de comando. Por exemplo:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Instalação silenciosa  
 Se você usar a opção /passive, /qn, /qb ou /qr com msiexec, também precisará especificar IACCEPTMSOLEDBSQLLICENSETERMS=YES, para indicar explicitamente que aceitou os termos da licença do usuário final. Essa opção deve ser especificada totalmente em letras maiúsculas.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>Instalar o Driver do OLE DB para SQL Server como uma dependência  
É importante não desinstalar o Driver do OLE DB para SQL Server até que todos os aplicativos dependentes sejam desinstalados. Para dar aos usuários um aviso de que o aplicativo depende do Driver do OLE DB para SQL Server, use a opção de instalação APPGUID no MSI, da seguinte maneira:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

O valor passado para APPGUID é o seu código de produto específico. É preciso criar um código de produto ao usar o Microsoft Installer para agrupar o programa de instalação do aplicativo.
A opção APPGUID requer a execução do instalador em um prompt de comandos com privilégios elevados.

## <a name="see-also"></a>Consulte Também  
 [Criação de aplicativos com o Driver do OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
