---
title: Notas de versão (OLE DB Driver para SQL Server) | Microsoft Docs
ms.date: 05/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 969caa46506c9fd19410c5ace753076b3ba02fbe
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65619990"
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
| Suporte para codificação do servidor UTF-8. | &bull; &nbsp; [Suporte a UTF-8 no OLE DB Driver para SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Suporte para autenticação do Azure Active Directory. | &bull; &nbsp; [Como usar o Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Julho de 2018

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `UseFMTONLY` e para a propriedade de inicialização `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.<br/><br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o OLE DB Driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Versão incorreta do arquivo de formato BCP corrigida. | O Driver do OLE DB 18.0 define incorretamente a versão do arquivo de formato BCP para 18.0 em vez de 11.0.<br/><br/>Arquivos de formato gerados pelo Driver do OLE DB 18.0 não podem ser lidos pelo Driver do OLE DB 18.1.<br/><br/>Se precisar usar arquivos de formato gerados pela versão anterior do driver com o novo driver, você poderá editar manualmente os arquivos para alterar a versão para 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `MultiSubnetFailover` e para a propriedade de inicialização `SSPROP_INIT_MULTISUBNETFAILOVER`. | &bull; &nbsp; [Suporte do OLE DB Driver para SQL Server para alta disponibilidade e recuperação de desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o OLE DB Driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
