---
title: Notas sobre a versão para ODBC for SQL Server no Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-chojas
author: v-makouz
ms.author: v-chojas
manager: kenvh
ms.openlocfilehash: 76ffaac48e8af454e887fd4fd30540eed4c4b453
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173515"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>Notas sobre a Versão para ODBC para SQL Server no Windows

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo de notas sobre a versão descreve as novidades do Microsoft ODBC Driver for SQL Server no Windows.

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="175-january-2020"></a>17.5, janeiro de 2020

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| O atributo de conexão SQL_COPT_SS_SPID para recuperar o SPID sem viagens de ida e volta ao servidor | Confira [Atributos e palavras-chave da cadeia de conexão e DSN](../dsn-connection-string-attribute.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2, outubro de 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Compatibilidade com pontos de extremidade adicionais do Azure Key Vault | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Compatibilidade com a configuração da versão de classificação de dados | Veja [Classificação de Dados](../data-classification.md#bkmk-version). |
| Incluir a Biblioteca de Autenticação do Azure Active Directory (adal.dll) no instalador | Agora incluída na instalação do driver base, ela atualizará as instalações existentes da Biblioteca de Autenticação do Microsoft Active Directory para SQL Server, removendo-as da lista de aplicativos instalados no Windows. |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="174-july-2019"></a>17.4, julho 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Always Encrypted com enclaves seguros. | Confira [Uso do Always Encrypted com o driver ODBC](../using-always-encrypted-with-the-odbc-driver.md). |
| Definições keep alive do TCP configuráveis. | Confira [Conectar-se ao SQL Server](../linux-mac/connection-string-keywords-and-data-source-names-dsns.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, fevereiro de 2019

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Modo de autenticação de Identidade de Serviço Gerenciada do Azure Active Directory (atribuída pelo usuário e pelo sistema). | Veja [Usando o Azure Active Directory com o Driver ODBC](../using-azure-active-directory.md). |
| Capacidade de transmitir parâmetros de entrada em relação a colunas Always Encrypted. | Veja [Limitações do driver ODBC ao usar o Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted). |
| Transações distribuídas XA. | [Usando Transações XA](../use-xa-with-dtc.md). |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, julho de 2018

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Classificação de Dados para o Banco de Dados SQL do Azure e SQL Server. | Veja [Classificação de Dados](../data-classification.md). |
| Suporte para codificação do servidor UTF-8. | &nbsp; |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, março de 2018

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para os atributos de conexão `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS`. | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>Permite controlar a hora em que o cache local de Chaves de Criptografia de Coluna existe, bem como liberá-lo.<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>Permite que o aplicativo restrinja as operações de AE para usar somente a lista especificada de Chaves Mestras de Coluna.<br/><br/> Para obter mais informações, veja [Como usar Always Encrypted com o Windows ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Suporte a autenticação interativa do Azure Active Directory | &nbsp; |
| Correções de bugs. | Veja [Correções de bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17, fevereiro de 2018

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Suporte para Always Encrypted para a API BCP. | &nbsp; |
| Novo atributo de cadeia de conexão `UseFMTOnly`. | Faz o driver usar metadados herdados em casos especiais que exigem tabelas temporárias. |
| Suporte para a Instância Gerenciada SQL do Azure. | Versão Prévia Privada Estendida.<br/><br/>Veja a seguinte lista de [Diferenças ao usar a Instância Gerenciada (ODBC versão 17)](#diffs-managed-instance-17). |
| &nbsp; | &nbsp; |

| Dependência alterada | Detalhes |
| :------------ | :------ |
| Removido o assistente de entrada do serviço online da Microsoft | A dependência foi removida. |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> Diferenças ao usar a Instância Gerenciada (ODBC versão 17)

Esta versão do ODBC contém suporte para a Instância Gerenciada SQL do Azure (Versão Prévia Privada Estendida). Veja a seguinte lista anotada de diferenças ao usar a Instância Gerenciada.

> [!NOTE]
> Há várias diferenças ao usar a Instância Gerenciada:
>
> - Não há suporte para FILESTREAM.
> - Não há suporte para acesso ao sistema de arquivos local, mas ele é necessário para itens como tracefiles.
> - Não há suporte para criar UDT do caminho local.
> - Não há suporte para Autenticação Integrada do Windows.
> - Não há suporte para DTC.
> - A conta `sa` não está presente (a conta padrão é chamada de `cloudSA`).
> - TDS token ERROR (0xAA) retorna o nome do servidor incorreto.
> - Não há suporte para caracteres especiais no nome do banco de dados.
> - Não há suporte para ALTER DATABASE [dbname1] MODIFY NAME = [dbname2].
> - As mensagens de erro são sempre mostradas em inglês, independentemente das configurações de idioma (mesmas que as do Azure).

## <a name="131"></a>13.1

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| O ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adiciona suporte para [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md). | Esses suportes adicionais estão disponíveis ao se conectar ao Microsoft SQL Server 2016 ou a uma versão posterior. |
| Há palavras-chave e atributos de pooling de conexões, que correspondem aos suportes para Always Encrypted e Azure Active Directory. | Essas palavras-chave e atributos são descritos em [Pooling de conexões com reconhecimento de driver no ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Adiciona suporte para o Microsoft SQL Server 2016. | Retém a funcionalidade do driver ODBC versão 11. |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| Recurso adicionado | Detalhes |
| :------------ | :------ |
| Contém novos recursos. | Veja [Recursos do Microsoft ODBC Driver for SQL Server no Windows](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md). |
| Contém todos os recursos que acompanham o ODBC no Cliente Nativo do SQL Server 2012. | &nbsp; |
| &nbsp; | &nbsp; |
