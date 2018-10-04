---
title: Instalar o SSMA para cliente do Oracle (OracleToSQL) | Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: 72df6a9da82e421dfb921501c110d363aa54a8f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781542"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalar o cliente SSMA para Oracle (OracleToSQL)
O cliente SSMA consiste em arquivos de programa que executam as seguintes tarefas:  
  
-   Conecte-se a um banco de dados Oracle.  
  
-   Conectar-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Converter objetos de banco de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe.  
  
-   Carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Este tópico fornece os pré-requisitos de instalação e as instruções para instalar o SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
O SSMA é projetado para trabalhar com Oracle 9 ou versões posteriores e todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Antes de instalar o SSMA, certifique-se de que o computador atende aos seguintes requisitos:  
  
-   Windows 7 ou versões posteriores, ou Windows Server 2008 ou versões posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 ou posterior. O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.0 está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mídia do produto. Você também pode obtê-lo do [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Cliente Oracle 9.0 ou posterior e conectividade para os bancos de dados Oracle que você deseja migrar. A versão do cliente Oracle deve ser a mesma versão ou uma versão posterior que a versão de banco de dados Oracle.  
  
    Você pode instalar o cliente Oracle de mídia do produto Oracle ou no site da Oracle. Para obter informações sobre a conectividade, consulte [conectar-se ao banco de dados Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acesso a e permissões suficientes no computador que hospeda a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure em que será migrado dados e objetos de banco de dados. Para obter mais informações, consulte [conectando ao SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB de RAM são recomendados.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalar o SSMA para cliente Oracle  
O SSMA é um download da Web. Para baixar a versão mais recente, consulte o [página de download do SQL Server Migration Assistant](http://aka.ms/ssmafororacle).  
  
Depois de baixar a versão mais recente, você deve extrair os arquivos de instalação antes de instalar o SSMA.  
  
**Para instalar o cliente SSMA**  
  
1.  Clique duas vezes no SSMA para Oracle *n*. Install.exe, onde *n* é o número de compilação.  
  
2.  Na página de boas-vinda, clique em **próxima**.  
  
    Se você não tiver os pré-requisitos instalados, será exibida uma mensagem que indica que você deve primeiro instalar os componentes necessários. Certifique-se de que você instalou todos os pré-requisitos e, em seguida, execute o programa de instalação novamente.  
  
3.  Leia o contrato de licença de usuário final. Se você concordar, marque **aceito os termos do contrato de licença**e, em seguida, clique em **próxima**.  
  
4.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
5.  Clique em **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas as versões anteriores do SSMA para Oracle antes de instalar a nova versão.  
  
O local de instalação padrão é C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle.  
  
Além dos arquivos de programa do SSMA, você também deve instalar o SSMA para o pacote de extensão do Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [instalando os componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Instalar os componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
