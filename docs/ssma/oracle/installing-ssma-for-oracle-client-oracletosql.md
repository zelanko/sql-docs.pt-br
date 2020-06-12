---
title: Instalando o SSMA para Oracle Client (OracleToSQL) | Microsoft Docs
description: Saiba mais sobre os pré-requisitos de instalação para o cliente do Assistente de Migração do SQL Server (SSMA) para Oracle e como instalá-los.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: be5f48508c44dc456c2d19e1ff1eba985b982111
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293913"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalar o cliente SSMA para Oracle (OracleToSQL)
O cliente do SSMA consiste nos arquivos de programa que executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados Oracle.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Converta objetos de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.  
  
-   Carregue os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Migre dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Pré-requisitos  
O SSMA foi projetado para funcionar com o Oracle 9 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Antes de instalar o SSMA, verifique se o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.  
  
-   A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 ou posterior. A [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4,0 está disponível na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mídia do produto. Você também pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Oracle Client 9,0 ou uma versão posterior e conectividade com os bancos de dados Oracle que você deseja migrar. A versão do cliente Oracle deve ser a mesma versão do, ou uma versão posterior à versão do banco de dados Oracle.  
  
    Você pode instalar o cliente Oracle da mídia de produto Oracle ou do site da Oracle. Para obter informações sobre conectividade, consulte [conectando-se a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o banco de dados SQL do Azure, onde você migrará os objetos de banco de dados e os mesmos. Para obter mais informações, consulte [conectando-se a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalando o cliente do SSMA para Oracle  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte a [página de download do assistente de migração do SQL Server](https://aka.ms/ssmafororacle).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação do antes de poder instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes em SSMA para Oracle *n*.Install.exe, em que *n* é o número da compilação.  
  
2.  Na página de Boas-vindas, clique em **Avançar**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Verifique se você instalou todos os pré-requisitos e execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, selecione **aceito os termos do contrato de licença**e clique em **Avançar**.  
  
4.  Na página escolher tipo de instalação, clique em **típico**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para Oracle antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft Assistente de Migração do SQL Server para Oracle.  
  
Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para Oracle Extension Pack em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [instalando componentes do SSMA em SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Instalando os componentes do SSMA em SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
