---
title: Notas (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21380decd228d82695c4ca9972852585a4fc3dbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes"></a>Notas de Versão
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Notas de versão do Microsoft ODBC Driver for SQL Server no Windows.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC 17.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows

**Recursos adicionados**:

Suporte para `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexão (para obter mais informações, consulte [usando sempre criptografado com o Driver ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlando a hora em que o cache local das chaves de criptografia de coluna existe, bem como liberar a ele
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que o aplicativo restringir as operações de AE para usar somente a lista especificada de chaves mestras de coluna


Suporte de autenticação interativa do Active Directory do Azure

[Correções de bugs](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] o Driver ODBC 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows

**Recursos adicionados**:

Sempre criptografado suporte para a API BCP

Novo atributo de cadeia de caracteres de conexão UseFMTOnly faz com que o driver usar metadados herdados em casos especiais que exigem a tabelas temporárias.

Suporte para a instância gerenciada do SQL Azure (visualização privada estendida). 
> [!NOTE]
> Há algumas diferenças ao usar a instância gerenciada:
> -   Não há suporte para FILESTREAM 
> -   Acesso de sistema de arquivos local não tem suporte, mas necessário para coisas como tracefiles 
> -   Crie a UDT do local não há suporte para o caminho 
> -   Não há suporte para a autenticação integrada do Windows 
> -   Não há suporte para o DTC 
> -   conta 'sa' não está presente (a conta padrão é chamada 'cloudSA')
> -   Erro de token de TDS (0xAA) retorna o nome de servidor incorreto
> -   Não há suporte para caracteres especiais no nome do banco de dados 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] não tem suporte
> -   As mensagens de erro são sempre mostradas em inglês, independentemente do idioma configurações (mesmo que o Azure) 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows  
 ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] adiciona suporte para [sempre criptografado](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Active Directory do Azure](../../../connect/odbc/using-azure-active-directory.md) quando usado em conjunto com o Microsoft SQL Server 2016.  Conexão correspondente pooling palavras-chave/atributos são descritos em [Driver Pooling Conexão com suporte no Driver ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows  
 ODBC Driver 13 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] inclui a funcionalidade anterior do ODBC Driver 11 para SQL Server e adiciona suporte para o Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>O que há de novo no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no Windows  
 ODBC Driver 11 para SQL Server contém novos [recursos](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md) , bem como todos os recursos que acompanham o ODBC no SQL Server 2012 Native Client.  
