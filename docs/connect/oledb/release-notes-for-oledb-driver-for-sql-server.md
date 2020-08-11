---
title: Notas sobre a versão do Driver do OLE DB
description: Este artigo de notas sobre a versão descreve as alterações em cada versão do Driver do Microsoft OLE DB para SQL Server.
ms.date: 05/25/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 296efcdd888e2424cfb80f40221f7d8f65acab89
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011912"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de versão do Driver do Microsoft OLE DB para SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Esta página discute o que foi adicionado em cada versão do Driver do Microsoft OLE DB para SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1840"></a>18.4.0
![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2129954)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2131003)  

Lançado: Maio de 2020

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2129954&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2131003&clcid=0x40a)  

### <a name="features-added"></a>Recursos adicionados

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para TNIR (Resolução IP de Rede Transparente) |[TNIR (Resolução IP de Rede Transparente)](features/using-transparent-network-ip-resolution.md)|
| Suporte para codificação do cliente em UTF-8 | [Suporte ao UTF-8 no OLE DB Driver for SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md) |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Corrigidos vários bugs na interface [ISequentialStream](https://docs.microsoft.com/previous-versions/windows/desktop/ms718035(v=vs.85)) | Alguns bugs que afetam páginas de código multibyte faziam com que a interface relatasse prematuramente o fim do fluxo durante a operação de leitura.|
| Corrigida uma perda de memória na interface [IOpenRowset::OpenRowset](https://docs.microsoft.com/previous-versions/windows/desktop/ms716724(v=vs.85)) | Foi corrigida uma perda de memória na interface [IOpenRowset::OpenRowset](https://docs.microsoft.com/previous-versions/windows/desktop/ms716724(v=vs.85)) quando a propriedade `SSPROP_IRowsetFastLoad` estava habilitada. |
| Corrigido um bug em cenários envolvendo um tipo de dados `sql_variant` e cadeias de caracteres não ASCII. | A execução de determinados cenários envolvendo um tipo de dados `sql_variant` e cadeias de caracteres não ASCII pode resultar em dados corrompidos. Para obter detalhes, confira: [Problemas conhecidos](ole-db-data-types/ssvariant-structure.md#known-issues). |
| Corrigidos problemas com o botão *Testar Conexão* na [caixa de diálogo de configuração do UDL](help-topics/data-link-pages.md) | O botão *Testar Conexão* na [caixa de diálogo de configuração do UDL](help-topics/data-link-pages.md) agora honra as propriedades de inicialização definidas na guia *Todos*. |
| Corrigida a manipulação do valor padrão da propriedade `SSPROP_INIT_PACKETSIZE` | Corrigido um erro inesperado quando a propriedade `SSPROP_INIT_PACKETSIZE` era definida com o valor padrão de `0`. Para conhecer os detalhes dessa propriedade, confira [Propriedades de inicialização e autorização](ole-db-data-source-objects/initialization-and-authorization-properties.md). |
| Corrigidos problemas de estouro de buffer em [IBCPSession](ole-db-interfaces/ibcpsession-ole-db.md) | Corrigidos problemas de estouro de buffer ao usar arquivos de dados malformados. |
| Corrigidos problemas de acessibilidade | Corrigidos problemas de acessibilidade na interface do usuário do instalador e na [caixa de diálogo de Logon do SQL Server](help-topics/sql-server-login-dialog.md) (leitura de conteúdo, tabulações). |

## <a name="previous-releases"></a>Versões anteriores

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
| Incluir a Biblioteca de Autenticação do Azure Active Directory (adal.dll) no instalador | Agora incluída na instalação do driver base, o instalador do OLE DB atualizará as instalações existentes da Biblioteca de Autenticação do Microsoft Active Directory para SQL Server, removendo-as da lista de aplicativos instalados no Windows. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bugs corrigidos

| Correções de bugs | Detalhes |
| :-------- | :------ |
| Correção de lógica DROP INDEX em [IIndexDefinition::DropIndex](https://go.microsoft.com/fwlink/?linkid=2106448). | As versões anteriores do driver do OLE DB não podem remover um índice de chave primária quando a ID do esquema e a ID de usuário do proprietário do índice não são iguais. |
| &nbsp; | &nbsp; |

Baixe versões anteriores do driver do OLE DB nos links para download nas seções a seguir:

## <a name="1823"></a>18.2.3

![download](../../ssms/media/download-icon.png) [Baixar o instalador x64](https://go.microsoft.com/fwlink/?linkid=2119554)  
![download](../../ssms/media/download-icon.png) [Baixar o instalador x86](https://go.microsoft.com/fwlink/?linkid=2119738)  

Lançado: Junho de 2019

Se precisar baixar o instalador em um idioma diferente daquele detectado para você, será possível usar esses links diretos.  
Para o driver x64: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
Para o driver x86: [Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added-in-1823"></a>Recursos adicionados na 18.2.3

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

### <a name="bugs-fixed-in-1822"></a>Bugs corrigidos na 18.2.2

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

### <a name="features-added-in-1821"></a>Recursos adicionados na 18.2.1

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

### <a name="features-added-in-1810"></a>Recursos adicionados na 18.1.0

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `UseFMTONLY` e para a propriedade de inicialização `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla como os metadados são recuperados ao se conectar ao [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e mais recente.<br/><br/>Para obter mais informações, consulte: [Como usar palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed-in-1810"></a>Bugs corrigidos na 18.1.0

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

### <a name="features-added-in-1802"></a>Recursos adicionados na 18.0.2

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para a palavra-chave da cadeia de conexão `MultiSubnetFailover` e para a propriedade de inicialização `SSPROP_INIT_MULTISUBNETFAILOVER`. | Para obter mais informações, consulte:<br/>&bull; &nbsp; [Suporte ao Driver do OLE DB para SQL Server para alta disponibilidade e recuperação de desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md),<br/>&bull; &nbsp; [Como usar palavras-chave de cadeia de conexão com o Driver do OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Confira também

[Driver do Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
