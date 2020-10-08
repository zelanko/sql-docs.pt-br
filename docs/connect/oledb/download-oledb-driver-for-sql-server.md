---
title: Baixar o Driver do Microsoft OLE DB para SQL Server | Microsoft Docs
description: Baixe o Driver do Microsoft OLE DB para SQL Server a fim de desenvolver aplicativos nativos do Windows que se conectam ao SQL Server e ao Banco de Dados SQL do Azure.
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4424f11e4b8d31c964d024b3ecaf90bec0cd7c21
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727335"
---
# <a name="download-microsoft-ole-db-driver-for-sql-server"></a>Baixar o Driver do Microsoft OLE DB para SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

O Driver do OLE DB para SQL Server é uma API (interface de programação de aplicativo) de acesso a dados autônoma, usada para OLE DB. O Driver do OLE DB para SQL Server está disponível no Windows e oferece o driver do OLE DB do SQL em uma DLL (biblioteca de vínculo dinâmico).

## <a name="download"></a>Baixar

O instalador redistribuível do Driver do Microsoft OLE DB para SQL Server instala os componentes cliente necessários durante o tempo de execução para aproveitar os recursos mais recentes do SQL Server. Da versão 18.3 em diante, o instalador também inclui e instala a Biblioteca de Autenticação do Microsoft do Active Directory (ADAL.dll).

O Driver do Microsoft OLE DB 18.4 para SQL Server é a versão de GA (disponibilidade geral) mais recente. Se você tiver uma versão anterior do Driver do Microsoft OLE DB 18 para SQL Server instalada, a instalação do 18.4 fará um upgrade para o 18.4.

**[![Download](../../ssms/media/download-icon.png) Baixar o Driver do Microsoft OLE DB para SQL Server (x64)](https://go.microsoft.com/fwlink/?linkid=2129954)**  
**[![Download](../../ssms/media/download-icon.png) Baixar o Driver do Microsoft OLE DB para SQL Server (x86)](https://go.microsoft.com/fwlink/?linkid=2131003)**  

### <a name="version-information"></a>Informações da versão

- Número da versão: 18.4.0
- Lançado: Mai 30, 2020

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse a [versão do site em inglês dos EUA](). Você pode baixar idiomas diferentes do site da versão em inglês dos EUA selecionando [idiomas disponíveis](#available-languages).

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do Driver do Microsoft OLE DB para SQL Server pode ser instalada nos seguintes idiomas:

Driver do Microsoft OLE DB 18.4 para SQL Server (x64):  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)

Driver do Microsoft OLE DB 18.4 para SQL Server (x86):  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)

## <a name="release-notes"></a>Notas de versão

Para saber detalhes sobre esta versão, confira [as notas sobre a versão](release-notes-for-oledb-driver-for-sql-server.md).

## <a name="previous-releases"></a>Versões anteriores

[Versões anteriores do Driver do Microsoft OLE DB para SQL Server](release-notes-for-oledb-driver-for-sql-server.md#previous-releases)

## <a name="see-also"></a>Confira também

[Notas de versão do Microsoft OLE DB Driver for SQL Server](release-notes-for-oledb-driver-for-sql-server.md)  
[Requisitos do sistema para o OLE DB Driver para SQL Server](system-requirements-for-oledb-driver-for-sql-server.md)  
[Políticas de suporte do OLE DB Driver para SQL Server](applications\support-policies-for-oledb-driver-for-sql-server.md)  
[Quando usar o Driver do OLE DB para SQL Server](when-to-use-oledb-driver-for-sql-server.md)  
[Instalação do Driver do OLE DB para SQL Server](applications/installing-oledb-driver-for-sql-server.md)