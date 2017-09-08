---
title: Instalando o SSMA para cliente do MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: eafef1f4a4f16f704b76b31aa77d3c93f84d5821
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalando o SSMA para cliente do MySQL (MySQLToSQL)
O SSMA para cliente do MySQL consiste em arquivos de programas, executam as seguintes tarefas:  
  
-   Conecte-se ao banco de dados MySQL.  
  
-   Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
-   Converter os objetos de banco de dados MySQL para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
Este tópico fornece os pré-requisitos de instalação e instruções de instalação do SSMA para cliente do MySQL.  
  
## <a name="prerequisites"></a>Pré-requisitos  
SSMA para MySQL é projetado para trabalhar com o MySQL 4.1 ou versões posteriores e todas as edições do SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016 e banco de dados de SQL do Azure.  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível na mídia do produto SQL Server. Você também pode obter a partir de [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Driver ODBC para MySQL 5.1 e conectividade para os bancos de dados MySQL que você deseja migrar. Você pode instalar o MySQL do site do MySQL. Para obter informações sobre a conectividade, consulte [se conectar ao MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acesso e permissões suficientes no computador que hospeda a instância de destino do SQL Server onde você irá migrar dados e objetos de banco de dados. Para obter mais informações, consulte [se conectar ao SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   No caso de projetos do SQL Azure, acesso e permissões suficientes para a instância do banco de dados do SQL Azure em que você está fazendo a migração do banco de dados objetos e dados. Para obter mais informações, consulte [se conectar ao banco de dados de SQL do Azure &#40; MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalando o SSMA para cliente do MySQL  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmaformysql).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente do SSMA**  
  
1.  Clique duas vezes o SSMA para MySQL  *n* . Install.exe, onde  *n*  é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próximo**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos antes de executar o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e, em seguida, clique em **próximo**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para MySQL antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant para MySQL.  
  
No computador do Windows de 64 bits, o produto foi instalado no Assistente de migração C:\Microsoft SQL Server para MySQL.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

