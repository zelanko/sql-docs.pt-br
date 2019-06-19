---
title: Instalar o SSMA para cliente do Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cca10f2a54a70e91e46bb8b98e9799885b5f175
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740986"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Instalar o cliente SSMA para Sybase (SybaseToSQL)
O cliente SSMA consiste nos arquivos de programa que são usados para se conectar a um servidor de banco de dados do Sybase Adaptive Server Enterprise (ASE) e uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL DB, converter objetos de banco de dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou sintaxe de BD SQL do Azure, carregue o objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL DB, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Azure SQLDB.  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
O SSMA é projetado para trabalhar com o ASE 11.9.2 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versão 4.0 ou posterior. O .NET Framework versão 4.0 está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mídia do produto. Você também pode obtê-lo do [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   O provedor de Sybase OLEDB/ADO.Net/ODBC e conectividade com o servidor de banco de dados Sybase ASE que contém os bancos de dados que você deseja migrar. Você pode instalar provedores de mídia do produto Sybase ASE. Para obter informações sobre a conectividade, consulte [conectar-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure em que será migrado dados e objetos de banco de dados. Para obter mais informações, consulte [conectando ao SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[conectar-se ao BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Instalar o SSMA para Sybase cliente  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](https://aka.ms/ssmaforsybase).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes no SSMA para Sybase *n*. Install.exe, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próxima**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, marque **aceito os termos do contrato de licença**e, em seguida, clique em **próxima**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para Sybase antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase.  
  
Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para Sybase pacote de extensão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [instalando os componentes do SSMA no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Instalar os componentes do SSMA no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
