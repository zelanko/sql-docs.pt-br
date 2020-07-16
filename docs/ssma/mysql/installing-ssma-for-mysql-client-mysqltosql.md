---
title: Instalando o cliente SSMA para MySQL (MySQLToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação para o cliente Assistente de Migração do SQL Server (SSMA) para MySQL e como instalá-lo.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7dc2cb4216386e13c57d31f121809a604e91b67d
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411604"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalando o cliente SSMA para MySQL (MySQLToSQL)

O cliente do SSMA para MySQL consiste nos arquivos de programa que executam as seguintes tarefas:

- Conecte-se a um banco de dados MySQL.  
- Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .
- Converta os objetos do banco de dados MySQL para os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] objetos ou.
- Carregue os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .
- Migre dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

Este tópico fornece os pré-requisitos de instalação e instruções para instalar o SSMA para cliente MySQL.

## <a name="prerequisites"></a>Pré-requisitos

O SSMA para MySQL foi projetado para funcionar com o MySQL 4,1 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou posterior, e [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:

- Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- Driver ODBC 5,1 do MySQL e conectividade com os bancos de dados MySQL que você deseja migrar. Você pode instalar o MySQL no site do MySQL. Para obter informações sobre conectividade, consulte [conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md).
- Acesso a e permissões suficientes no computador que hospeda a instância de destino da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual você migrará objetos de banco de dados e data. Para obter mais informações, consulte [conectando-se a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md).
- No caso de [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] projetos, acesso a e permissões suficientes para a instância do na [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] qual você migrará objetos e dados de banco de dados. Para obter mais informações, consulte [conectando-se ao banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).
- 4 GB de RAM recomendado.

## <a name="installing-ssma-for-mysql-client"></a>Instalando o SSMA para cliente MySQL

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaformysql).

Para instalar o cliente SSMA:

1. Clique duas vezes em **SSMAforMySQL_*n*. msi**, em que *n* é o número da compilação.
2. Na página de **Boas-vindas**, clique em **Avançar**.

   Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos antes de executar o programa de instalação novamente.

3. Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito o contrato**e clique em **Avançar**.
4. Na página **escolher tipo de instalação** , clique em **típico**.
5. Na página **pronto para instalar** , você pode habilitar ou desabilitar a telemetria e as verificações de atualização automática toda vez que a ferramenta for iniciada. Clique em **Instalar** para iniciar a instalação.

> [!IMPORTANT]
> Desinstale todas as versões anteriores do SSMA para MySQL antes de instalar a nova versão.

O local de instalação padrão é `C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL`.

## <a name="see-also"></a>Confira também

- [Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
