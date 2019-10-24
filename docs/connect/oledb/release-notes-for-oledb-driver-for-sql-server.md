---
title: Notas de versão (OLE DB Driver para SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 350856cc27bdec601e0db2998f9ff9953cdf6ec7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381729"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de versão do Driver do Microsoft OLE DB para SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página discute o que foi adicionado em cada versão do Driver do Microsoft OLE DB para SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1830"></a>18.3.0

Outubro de 2019

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para autenticação do Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Como usar o Azure Active Directory](features/using-azure-active-directory.md). |
| Suporte para ADAL (Biblioteca de Autenticação do Active Directory inserida). | Uma instalação separada da ADAL não é mais necessária para usar determinados métodos de autenticação. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Lógica drop index corrigida em [IIndexDefinition::D ropindex](https://go.microsoft.com/fwlink/?linkid=2106448). | As versões anteriores do driver de OLE DB não podem cancelar um índice de chave primária quando a ID do esquema e a ID de usuário do proprietário do índice não são iguais. |
| &nbsp; | &nbsp; |

## <a name="1823"></a>18.2.3

Junho de 2019

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para atualizações de driver do SQL Server mídia removível. | Essa melhoria permite atualizações de driver diretamente do SQL Server mídia removível. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

Maio de 2019

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Corrigida autenticação não interativa do Azure Active Directory em MTA (Multi-Threaded Apartment). | O Driver do OLE DB 18.2.1 tenta incorretamente alterar o modelo de simultaneidade COM em um apartment que foi inicializado anteriormente como MTA (Multi-Threaded). Como resultado, em um aplicativo que faz com que mais de uma chamada subsequente a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) ou [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) antes de chamar a interface [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), o driver falha em se conectar ao usar qualquer um dos modos de autenticação do Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

Fevereiro de 2019

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para codificação do servidor UTF-8. | [Suporte a UTF-8 no Driver do OLE DB para SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Suporte para autenticação do Azure Active Directory. | [Como usar o Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Julho de 2018

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `UseFMTONLY` e para a propriedade de inicialização `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.<br/><br/>Para obter mais informações, consulte: [usando palavras-chave de cadeia de conexão com OLE DB driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Versão incorreta do arquivo de formato BCP corrigida. | O Driver do OLE DB 18.0 define incorretamente a versão do arquivo de formato BCP para 18.0 em vez de 11.0.<br/>Arquivos de formato gerados pelo Driver do OLE DB 18.0 não podem ser lidos pelo Driver do OLE DB 18.1.<br/>Se precisar usar arquivos de formato gerados pela versão anterior do driver com o novo driver, você poderá editar manualmente os arquivos para alterar a versão para 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `MultiSubnetFailover` e para a propriedade de inicialização `SSPROP_INIT_MULTISUBNETFAILOVER`. | Para obter mais informações, consulte:<br/>&bull; &nbsp; [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md),<br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o OLE DB Driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
