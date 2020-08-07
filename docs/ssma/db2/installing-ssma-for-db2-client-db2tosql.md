---
title: Instalando o SSMA para cliente DB2 (DB2ToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação para o cliente do Assistente de Migração do SQL Server (SSMA) para DB2 e como instalá-lo.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5b9679451c1052423cb412b85bf8dde25c4a8351
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823709"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Instalando o SSMA para cliente DB2 (DB2ToSQL)

O cliente do SSMA consiste nos arquivos de programa que executam as seguintes tarefas:

- Conecte-se a um banco de dados DB2.
- Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Converta objetos de banco de dados DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.
- Carregue os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
- Migre dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.

## <a name="prerequisites"></a>Pré-requisitos

O SSMA foi projetado para trabalhar com DB2 no z/OS versão 9,0 e 10,0, DB2 no LUW versão 9,8 e 10,1 ou versões posteriores, DB2 para i versão 7,1 ou posterior e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou versões posteriores.

Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:

- Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou versões posteriores.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- Provedor Microsoft OLE DB para DB2 versão 5 ou uma versão posterior e conectividade com os bancos de dados DB2 que você deseja migrar.
- Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure, onde você migrará os objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).
- 4 GB de RAM recomendado.

## <a name="microsoft-ole-db-provider-for-db2"></a>Microsoft OLE DB Provider for DB2

Para baixar o provedor de OLE DB para DB2 versão 6,0, vá para [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmafordb2).

Para instalar o cliente SSMA:

1. Clique duas vezes em **SSMAforDB2_*n*. msi**, em que *n* é o número da compilação.
2. Sobre o **boas-vindas** página, selecione **próxima**.

   Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.

3. Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito o contrato**e, em seguida, selecione **Avançar**.
4. Na página **escolher tipo de instalação** , selecione **típica**.
5. Na página **pronto para instalar** , você pode habilitar ou desabilitar a telemetria e as verificações de atualização automática toda vez que a ferramenta for iniciada. Clique em **Instalar** para iniciar a instalação.

> [!IMPORTANT]
> Desinstale todas as versões anteriores do SSMA para DB2 antes de instalar a nova versão.

O local de instalação padrão é `C:\Program Files\Microsoft SQL Server Migration Assistant for DB2`.

## <a name="see-also"></a>Confira também

- [Instalar os componentes do SSMA no SQL Server](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)
- [Migrar bancos de dados do DB2 para o SQL Server](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)
