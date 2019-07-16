---
title: Instalar o SSMA para cliente do MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9dcdeaff1c4782453a9fd57cc709e17ad3200d28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086821"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalar o SSMA para cliente MySQL (MySQLToSQL)
O SSMA para cliente MySQL consiste em arquivos de programa que executam as seguintes tarefas:  
  
-   Conecte-se ao banco de dados MySQL.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure.  
  
-   Converter os objetos de banco de dados MySQL para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA para cliente do MySQL.  
  
## <a name="prerequisites"></a>Pré-requisitos  
SSMA para MySQL foi projetado para trabalhar com o MySQL 4.1 ou versões posteriores e todas as edições do SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 e BD SQL do Azure.  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível na mídia de produto do SQL Server. Você também pode obtê-lo do [.NET Framework Developer Center](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Driver de ODBC do MySQL 5.1 e a conectividade com os bancos de dados MySQL que você deseja migrar. Você pode instalar o MySQL do site do MySQL. Para obter informações sobre a conectividade, consulte [conectando ao MySQL a &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do SQL Server em que será migrado dados e objetos de banco de dados. Para obter mais informações, consulte [conectando ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   No caso de projetos do SQL Azure, acesso e permissões suficientes para a instância do banco de dados do SQL Azure em que você está fazendo a migração de banco de dados objetos e dados. Para obter mais informações, consulte [conectar-se ao BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalando SSMA para cliente do MySQL  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](https://aka.ms/ssmaformysql).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes no SSMA para MySQL *n*. Install.exe, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próxima**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos antes de executar o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, marque **aceito os termos do contrato de licença**e, em seguida, clique em **próxima**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para MySQL, antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL.  
  
No computador do Windows de 64 bits, o produto foi instalado em C:\Microsoft SQL Server Migration Assistant para MySQL.  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
