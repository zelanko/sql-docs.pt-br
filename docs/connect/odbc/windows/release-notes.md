---
title: Release Notes (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: cb599d59a374fc09dbc0009f0288296cc1df9d9d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702061"
---
# <a name="release-notes"></a>Notas de Versão
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Notas de versão do Microsoft ODBC Driver for SQL Server no Windows.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows

**Recursos adicionados**:

Classificação de dados para o banco de dados SQL e SQL Server, para obter mais informações consulte [classificação de dados](../data-classification.md)

Suporte para codificação do servidor UTF-8

[Correções de bugs](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows

**Recursos adicionados**:

Suporte para `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexão (para obter mais informações, consulte [usando o Always Encrypted com o Driver ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar a hora em que existe no cache local de chaves de criptografia de coluna, bem como liberar a ele
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que o aplicativo restringir as operações de AE para usar somente a lista especificada de chaves mestras de coluna


Suporte a autenticação interativa do Azure Active Directory

[Correções de bugs](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows

**Recursos adicionados**:

Always Encripted dá suporte para a API BCP

Novo atributo de cadeia de caracteres de conexão UseFMTOnly faz com que o driver usar metadados herdados em casos especiais que exigem a tabelas temporárias.

Suporte para a instância gerenciada do SQL do Azure (versão prévia privada estendida). 
> [!NOTE]
> Há várias diferenças ao usar a instância gerenciada:
> -   Não há suporte para FILESTREAM 
> -   Acesso de sistema de arquivos local não tem suporte, mas necessário para coisas como tracefiles 
> -   Criar o UDT de local não há suporte para o caminho 
> -   Não há suporte para a autenticação integrada do Windows 
> -   Não há suporte para DTC 
> -   conta 'sa' não está presente (a conta padrão é chamada 'cloudSA')
> -   Erro de token de TDS (0xAA) retorna o nome de servidor incorreto
> -   Não há suporte para caracteres especiais no nome do banco de dados 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] não tem suporte
> -   As mensagens de erro são sempre mostradas em inglês, independentemente da linguagem configurações (mesmo que o Azure) 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows  
 ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adiciona suporte para [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [do Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) quando usado em conjunto com o Microsoft SQL Server 2016.  Conexão correspondente pooling palavras-chave/atributos são descritos em [Driver Pooling Conexão com suporte no Driver ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows  
 ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui a funcionalidade anterior do ODBC Driver 11 para SQL Server e adiciona suporte para Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novidades do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no Windows  
 O ODBC Driver 11 for SQL Server contém novos [recursos](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md), bem como todos os recursos que acompanham o ODBC no SQL Server 2012 Native Client.  
