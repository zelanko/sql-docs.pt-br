---
title: Instalando o cliente SSMA para MySQL (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086821"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalar o SSMA para cliente MySQL (MySQLToSQL)
O cliente do SSMA para MySQL consiste nos arquivos de programa que executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados MySQL.  
  
-   Conecte-se a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância do ou SQL Azure.  
  
-   Converta os objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados MySQL para os objetos ou SQL Azure.  
  
-   Carregue os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
-   Migre dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure.  
  
Este tópico fornece os pré-requisitos de instalação e instruções para instalar o SSMA para cliente MySQL.  
  
## <a name="prerequisites"></a>Prerequisites  
O SSMA para MySQL foi projetado para funcionar com o MySQL 4,1 ou versões posteriores e todas as edições do SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 e BD SQL do Azure.  
  
Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 ou posterior. A [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 está disponível na mídia do produto SQL Server. Você também pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Driver ODBC 5,1 do MySQL e conectividade com os bancos de dados MySQL que você deseja migrar. Você pode instalar o MySQL no site do MySQL. Para obter informações sobre conectividade, consulte [conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do SQL Server em que você migrará objetos de banco de dados e data. Para obter mais informações, consulte [conectando-se a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   No caso de projetos de SQL Azure, acesso a e permissões suficientes para a instância do banco de dados SQL do Azure em que você migrará os objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se ao banco de dados SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalando SSMA para cliente do MySQL  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmaformysql).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de poder instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes em SSMA para MySQL *n*. Install. exe, em que *n* é o número de Build.  
  
2.  Na página de Boas-vindas, clique em **Avançar**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem indicando que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos antes de executar o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e clique em **Avançar**.  
  
4.  Na página escolher tipo de instalação, clique em **típico**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para MySQL antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server para MySQL.  
  
No computador Windows de 64 bits, o produto é instalado no C:\Microsoft Assistente de Migração do SQL Server para MySQL.  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
