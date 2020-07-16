---
title: Instalando o SSMA for SAP ASE Client (SybaseToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação do Assistente de Migração do SQL Server (SSMA) para SAP Adaptive Server Enterprise (ASE) e como instalar o.
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 288b6458fc8429077472ba3ba7ad49e6d6fd7565
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411164"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>Instalando o SSMA for SAP ASE Client (SybaseToSQL)

O cliente SSMA consiste nos arquivos de programa que são usados para se conectar a um servidor de banco de dados do SAP Adaptive Server Enterprise (ASE) e uma instância do ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] , converter objetos de banco de dados do ase em ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] sintaxe, carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou e, [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] em seguida, migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.

## <a name="prerequisites"></a>Pré-requisitos

O SSMA foi projetado para trabalhar com o SAP ASE 11.9.2 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:

- Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] versão .NET Framework 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- O provedor Sybase OLE DB/ADO.Net/ODBC e a conectividade com o servidor de banco de dados do SAP ASE que contém os bancos que você deseja migrar. Você pode instalar provedores da mídia de produto SAP ASE. Para obter informações sobre conectividade, consulte [conectando-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).
- Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] onde você migrará objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [conectar-se ao banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).
- 4 GB de RAM recomendado.

## <a name="installing-the-ssma-for-sybase-client"></a>Instalando o cliente do SSMA para Sybase

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaforsybase).

Para instalar o cliente SSMA:

1. Clique duas vezes em **SSMAforSybase_*n*. msi**, em que *n* é o número da compilação.
2. Na página de Boas-vindas, clique em **Avançar**.

   Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.

3. Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito o contrato**e clique em **Avançar**.
4. Na página escolher tipo de instalação, clique em **típico**.
5. Na página **pronto para instalar** , você pode habilitar ou desabilitar a telemetria e as verificações de atualização automática toda vez que a ferramenta for iniciada. Clique em **Instalar** para iniciar a instalação.

> [!IMPORTANT]
> Desinstale todas as versões anteriores do SSMA para Sybase antes de instalar a nova versão.

O local de instalação padrão é `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase`.

Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para Sybase Extension Pack em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [instalando componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).

## <a name="see-also"></a>Confira também

- [Instalar os componentes do SSMA no SQL Server](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
- [Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
