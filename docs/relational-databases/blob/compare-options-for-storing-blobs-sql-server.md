---
title: Comparar opções para Armazenamento de Blobs (SQL Server) | Microsoft Docs
description: O SQL Server pode armazenar dados de blob (objeto binário grande) usados por aplicativos do Windows. Compare as opções neste banco de dados relacional para armazenamento de dados não estruturados.
ms.custom: ''
ms.date: 03/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7b0faae244963957eadb1bd894f90a88736427b4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768060"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>Comparar opções de armazenamento de Blobs (SQL Server)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Discute e compara as opções disponíveis para armazenar arquivos e documentos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="storing-files-in-the-database---benefits-and-expectations"></a><a name="Expectations"></a> Armazenando arquivos no banco de dados – Benefícios e expectativas

Um grande percentual de dados corporativos é não estruturado por natureza, e é normalmente armazenado como arquivos e documentos em sistemas de arquivos. A maioria desses dados é produzida, gerenciada e consumida por aplicativos que acessam os arquivos por meio de APIs do Windows. As empresas geralmente mantêm esses dados no sistema de arquivos, enquanto armazenam os metadados relacionados dos arquivos em um banco de dados relacional.

A integração de dados não estruturados no banco de dados relacional oferece os seguintes benefícios:

- Recursos de armazenamento integrado e gerenciamento de dados, inclusive backup.
- Serviços integrados, como pesquisa de texto completo e pesquisa semântica em dados e metadados.
- Facilidade de administração e gerenciamento de políticas nos dados não estruturados.

Geralmente, não tem sido conveniente armazenar dados não estruturados em um banco de dados relacional. Não é prático reescrever aplicativos estabelecidos (como Microsoft Word ou Adobe Reader) para interagir por meio de APIs de banco de dados relacional. Esses aplicativos esperam que os dados estejam acessíveis por meio de APIs do Windows. Os aplicativos têm estas expectativas:

- Aplicativos do Windows não estão cientes das transações de banco de dados e não as requerem.
- Aplicativos do Windows requerem compatibilidade com APIs do sistema de arquivos para dados de arquivos e diretórios.

Há muitos anos, o SQL Server não oferecia qualquer variedade de maneiras de armazenar dados não estruturados em um banco de dados relacional. No entanto, hoje oferece maneiras de armazenar dados não estruturados.

## <a name="filestream"></a><a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já tem o recurso FILESTREAM. O recurso FILESTREAM fornece armazenamento eficiente, gerenciamento e streaming de dados não estruturados armazenados como arquivos no sistema de arquivos. Entretanto, uma solução FILESTREAM exige a programação personalizada e não satisfaz o requisito de compatibilidade total de aplicativos do Windows, descrito anteriormente.

## <a name="filetables"></a><a name="FileTables"></a> Tabelas de arquivos

O recurso FileTable se baseia nos recursos existentes de FILESTREAM. O recurso FileTable permite que os clientes corporativos armazenem dados de arquivos não estruturados e hierarquias de diretório em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O recurso aborda os requisitos de acesso não transacional e compatibilidade de aplicativos do Windows para dados com base em arquivo.

## <a name="comparing-filestream-and-filetable"></a><a name="CompareFileTable"></a> Comparando FILESTREAM e FileTable

|Recurso|Servidor de arquivos e solução de banco de dados|Solução FILESTREAM|Solução FileTable|
|:------|:--------------------------------|:------------------|:-----------------|
|**Armazenamento único para tarefas de gerenciamento**|Não|Sim|**Sim**|
|**Conjunto único de serviços**: pesquisa, relatório, consulta etc.|Não|Sim|**Sim**|
|**Modelo de segurança integrada**|Não|Sim|**Sim**|
|**Atualizações in loco de dados FILESTREAM**|Sim|Não|**Sim**|
|**Hierarquia de arquivos e diretórios mantida no banco de dados**|Não|Não|**Sim**|
|**Compatibilidade de aplicativos do Windows**|Sim|Não|**Sim**|
|**Acesso relacional a atributos de arquivo**|Não|Não|**Sim**|

## <a name="comparing-filestream-and-remote-blob-store-rbs"></a><a name="CompareRBS"></a> Comparando FILESTREAM e repositório de BLOB remoto (RBS)

Outra opção para armazenar dados não estruturados envolve um RBS (Remote BLOB Store). Para saber mais, confira [RBS (Remote BLOB Store (SQL Server)](remote-blob-store-rbs-sql-server.md).

## <a name="more-information"></a><a name="more"></a> Mais informações

[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
[Remote Blob Store &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
