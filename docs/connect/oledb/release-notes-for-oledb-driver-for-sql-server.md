---
title: Notas de versão (OLE DB Driver para SQL Server) | Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161763"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de versão do Microsoft OLE DB Driver para SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Esta página discute o que foi adicionado em cada versão do Driver da Microsoft OLE DB para SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

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
| Suporte para o `UseFMTONLY` palavra-chave da cadeia de conexão e para o `SSPROP_INIT_USEFMTONLY` propriedade de inicialização. | `UseFMTONLY` Controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.<br/><br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o OLE DB Driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Fixo versão incorreta do arquivo de formato BCP. | O 18.0 do Driver de banco de dados OLE incorretamente define a versão do arquivo de formato BCP para 18.0, em vez de como 11.0.<br/><br/>Arquivos de formato gerados pelo 18.0 do Driver de banco de dados OLE não podem ser lido pelo 18.1 do Driver de banco de dados OLE.<br/><br/>Se você precisar usar arquivos de formato gerados pela versão anterior do driver com o novo driver, você pode editar manualmente os arquivos para alterar a versão 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para o `MultiSubnetFailover` palavra-chave da cadeia de conexão e o `SSPROP_INIT_MULTISUBNETFAILOVER` propriedade de inicialização. | &bull; &nbsp; [Suporte do OLE DB Driver para SQL Server para alta disponibilidade e recuperação de desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o OLE DB Driver para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
