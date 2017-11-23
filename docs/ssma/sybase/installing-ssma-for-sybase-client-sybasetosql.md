---
title: Instalando o SSMA para Sybase cliente (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: "18"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04357499b0ac47f8fa130ceb117946cbeeba1378
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Instalando o SSMA para Sybase cliente (SybaseToSQL)
O cliente do SSMA consiste nos arquivos de programa que são usados para se conectar a um servidor de banco de dados do Sybase Adaptive Server Enterprise (ASE) e uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do Azure SQL DB, converter objetos de banco de dados ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de banco de dados de SQL do Azure, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, e, em seguida, migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQLDB do Azure.  
  
Este tópico fornece os pré-requisitos de instalação e instruções de instalação do SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos  
O SSMA é projetado para trabalhar com ASE 11.9.2 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versão 4.0 ou posterior. O .NET Framework versão 4.0 está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mídia do produto. Você também pode obter a partir de [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   O provedor do Sybase OLEDB/ADO.Net/ODBC e conectividade com o servidor de banco de dados Sybase ASE que contém os bancos de dados que você deseja migrar. Você pode instalar provedores da mídia do produto do Sybase ASE. Para obter informações sobre a conectividade, consulte [conectando para Sybase ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Acesso e permissões suficientes no computador que hospeda a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure onde você irá migrar dados e objetos de banco de dados. Para obter mais informações, consulte [se conectar ao SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Se conectar ao banco de dados SQL do Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Instalando o SSMA para Sybase cliente  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmaforsybase).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente do SSMA**  
  
1.  Clique duas vezes o SSMA para Sybase  *n* . Install.exe, onde  *n*  é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próximo**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você tenha instalado todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e, em seguida, clique em **próximo**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA for Sybase antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant para Sybase.  
  
Além dos arquivos de programa do SSMA, você também deve instalar SSMA para o pacote de extensão do Sybase em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Para obter mais informações, consulte [instalar componentes do SSMA SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Instalando componentes do SSMA SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
