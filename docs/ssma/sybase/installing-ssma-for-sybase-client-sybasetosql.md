---
title: Instalando o SSMA for SAP ASE Client (SybaseToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação do Assistente de Migração do SQL Server (SSMA) para SAP Adaptive Server Enterprise (ASE) e como instalar o.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1325e9ba882bed76ecfc1b11f8ca1c379ca74bb4
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306243"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>Instalando o SSMA for SAP ASE Client (SybaseToSQL)

O cliente do SSMA consiste nos arquivos de programa que são usados para se conectar a um servidor de banco de dados do SAP Adaptive Server Enterprise (ASE) e uma instância do ou do Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL DB, converter objetos de banco de dados do ase para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a sintaxe do BD SQL do Azure, carregar os objetos no banco de dados SQL do Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, migrá-los para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos

O SSMA foi projetado para trabalhar com o ASE 11.9.2 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:  
  
- Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.  
- A versão [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 4,0 ou posterior. A versão 4,0 do .NET Framework está disponível na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mídia do produto. Você também pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
- O provedor de OLEDB/ADO.Net/ODBC do Sybase e a conectividade com o servidor de banco de dados do Sybase ASE que contém os bancos que você deseja migrar. Você pode instalar provedores da mídia de produto do Sybase ASE. Para obter informações sobre conectividade, consulte [conectando-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
- Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure, onde você migrará os objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [conectar-se ao banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
- 4 GB de RAM recomendado.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Instalando o cliente do SSMA para Sybase

O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaforsybase).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação do antes de poder instalar o SSMA.  
  
**Para instalar o cliente SSMA**
  
1. Clique duas vezes em SSMA para Sybase *n*.Install.exe, em que *n* é o número da compilação.  
  
2. Na página de Boas-vindas, clique em **Avançar**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.  
  
3. Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e clique em **Avançar**.  
  
4. Na página escolher tipo de instalação, clique em **típico**.  
  
5. Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1. Desinstale todas as versões anteriores do SSMA para Sybase antes de instalar a nova versão.
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server for Sybase.  
  
Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para Sybase Extension Pack em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [instalando componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte Também

[Instalando os componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
