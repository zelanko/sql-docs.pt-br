---
title: Notas de versão (OLE DB Driver para SQL Server) | Microsoft Docs
ms.date: 02/27/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 8c06b83241f377aa05d7e5c0e4cb0d83a424f15a
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866220"
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

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2117515)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2117517)  

Lançado: Outubro de 2019

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para autenticação do Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Como usar o Azure Active Directory](features/using-azure-active-directory.md). |
| Incluir a Biblioteca de Autenticação do Azure Active Directory (adal.dll) no instalador | Agora incluída na instalação do driver base, ela atualizará as instalações existentes da Biblioteca de Autenticação do Microsoft Active Directory para SQL Server, removendo-as da lista de aplicativos instalados no Windows. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Correção de lógica DROP INDEX em [IIndexDefinition::DropIndex](https://go.microsoft.com/fwlink/?linkid=2106448). | As versões anteriores do driver do OLE DB não podem remover um índice de chave primária quando a ID do esquema e a ID de usuário do proprietário do índice não são iguais. |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>Versões anteriores

Baixe versões anteriores do driver do OLE DB nos links para download nas seções a seguir:

## <a name="1823"></a>18.2.3

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2119554)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2119738)  

Lançado: Junho de 2019

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para atualizações de driver da mídia removível do SQL Server. | Esse aprimoramento permite atualizações de driver diretamente da mídia removível do SQL Server. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2118512)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2118415)  

Lançado: Maio de 2019

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Corrigida autenticação não interativa do Azure Active Directory em MTA (Multi-Threaded Apartment). | O Driver do OLE DB 18.2.1 tenta incorretamente alterar o modelo de simultaneidade COM em um apartment que foi inicializado anteriormente como MTA (Multi-Threaded). Como resultado, em um aplicativo que faz com que mais de uma chamada subsequente a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) ou [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) antes de chamar a interface [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), o driver falha em se conectar ao usar qualquer um dos modos de autenticação do Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2118511)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2118278)  

Lançado: Fevereiro de 2019

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para codificação do servidor UTF-8. | [Suporte a UTF-8 no Driver do OLE DB para SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Suporte para autenticação do Azure Active Directory. | [Como usar o Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2118506)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2118509)  

Lançado: Julho de 2018

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `UseFMTONLY` e para a propriedade de inicialização `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.<br/><br/>Para obter mais informações, consulte: [Como usar palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Versão incorreta do arquivo de formato BCP corrigida. | O Driver do OLE DB 18.0 define incorretamente a versão do arquivo de formato BCP para 18.0 em vez de 11.0.<br/>Arquivos de formato gerados pelo Driver do OLE DB 18.0 não podem ser lidos pelo Driver do OLE DB 18.1.<br/>Se precisar usar arquivos de formato gerados pela versão anterior do driver com o novo driver, você poderá editar manualmente os arquivos para alterar a versão para 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2118504)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2118277)  

Lançado: Março de 2018

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `MultiSubnetFailover` e para a propriedade de inicialização `SSPROP_INIT_MULTISUBNETFAILOVER`. | Para obter mais informações, consulte:<br/>&bull; &nbsp; [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md),<br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
