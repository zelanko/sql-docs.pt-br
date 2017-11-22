---
title: Instalando o SSMA para cliente Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: "19"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: b8673a22cb3c26beeb4fe118bdc403ac62464fa8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalando o SSMA para cliente Oracle (OracleToSQL)
O cliente do SSMA consiste em arquivos de programas, executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados Oracle.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Converter objetos de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Este tópico fornece os pré-requisitos de instalação e instruções de instalação do SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos  
O SSMA é projetado para trabalhar com Oracle 9 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mídia do produto. Você também pode obter a partir de [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Cliente Oracle 9.0 ou posterior e conectividade para os bancos de dados Oracle que você deseja migrar. A versão de cliente Oracle deve ser a mesma versão ou uma versão posterior, a versão do banco de dados Oracle.  
  
    Você pode instalar o cliente Oracle da mídia do produto Oracle ou do site da Oracle. Para obter informações sobre a conectividade, consulte [se conectar ao banco de dados Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acesso e permissões suficientes no computador que hospeda a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure onde você irá migrar dados e objetos de banco de dados. Para obter mais informações, consulte [se conectar ao SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalando o SSMA para cliente Oracle  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmafororacle).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente do SSMA**  
  
1.  Clique duas vezes o SSMA para Oracle  *n* . Install.exe, onde  *n*  é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próximo**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você tenha instalado todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e, em seguida, clique em **próximo**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para Oracle antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant para Oracle.  
  
Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para o pacote de extensão do Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [instalando o SSMA componentes do SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Instalando componentes do SSMA do SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrando bancos de dados Oracle para o SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
