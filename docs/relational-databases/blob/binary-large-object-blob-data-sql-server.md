---
title: Dados de objeto binário grande (Blob) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e98651675b4fa159f172dbcf93b38174df2a7a7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765734"
---
# <a name="binary-large-object-blob-data-sql-server"></a>Dados de objeto binário grande (Blob) (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece soluções para armazenar arquivos e documentos no banco de dados ou em dispositivos de armazenamento remotos.  
  
## <a name="compare-options-for-storing-blobs-in-sql-server"></a>Comparar opções de armazenamento de blobs no SQL Server

Compare as vantagens de FILESTREAM, FileTables e Remote Blob Store. Consulte [Comparar opções de armazenamento de blobs &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md).
  
##  <a name="options-for-storing-blobs"></a>Opções de armazenamento de blobs  

### <a name="filestream-40sql-server41relational-databasesblobfilestream-sql-servermd"></a>[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  

O FILESTREAM permite que aplicativos baseados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]armazenem dados não estruturados, como documentos e imagens, no sistema de arquivos. Os aplicativos podem utilizar as APIs de streaming avançado e o desempenho do sistema de arquivos e, ao mesmo tempo, manter consistência transacional entre os dados não estruturados e os dados estruturados correspondentes.  
  
### <a name="filetables-40sql-server41relational-databasesblobfiletables-sql-servermd"></a>[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  

O recurso FileTable oferece suporte para namespace de arquivo do Windows e compatibilidade de aplicativos do Windows com dados de arquivo armazenados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O FileTable permite que um aplicativo integre seus componentes de armazenamento e gerenciamento de dados e forneça serviços integrados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , inclusive pesquisa de texto completo e pesquisa semântica, em dados não estruturados e metadados.  
  
 Em outras palavras, você pode armazenar arquivos e documentos em tabelas especiais no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , denominadas FileTables, mas acessá-los a partir de aplicativos do Windows como se eles estivessem armazenados no sistema de arquivos, sem fazer alterações nos seus aplicativos cliente.  
  
### <a name="remote-blob-store-40rbs41-40sql-server41relational-databasesblobremote-blob-store-rbs-sql-servermd"></a>[Remote Blob Store &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  

O RBS (Remote BLOB Store) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que os administradores de bancos de dados armazenem BLOBs (objetos binários grandes) em soluções de armazenamento de mercadorias, e não diretamente no servidor. Isso leva a uma grande economia de espaço e evita o desperdício de recursos caros de hardware de servidor. O RBS fornece um conjunto de bibliotecas de API que definem um modelo padronizado para que aplicativos acessem dados BLOB. O RBS também inclui ferramentas de manutenção, como coleta de lixo, para ajudar a gerenciar dados BLOB remotos.  
  
 O RBS está incluído na mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não é instalado pelo programa de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
